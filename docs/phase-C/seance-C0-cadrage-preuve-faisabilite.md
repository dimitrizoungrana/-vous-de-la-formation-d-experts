# MAQUIS CONTROL — Séance C0
## Phase C · Cadrage de la preuve de faisabilité technique

> **Statut** : compte rendu de séance de brainstorming. Ce n'est ni l'étude de faisabilité technique, ni l'architecture logicielle, ni du code.
> **Exécution** : la preuve de faisabilité implique d'écrire du code. Elle ne commencera qu'après les Portes 1 et 2 **et** sur autorisation explicite du fondateur, avec un cadre contractuel signé (§9).
> Les technologies citées sont des **exemples de catégories à évaluer**, pas des choix.

---

## 1. Objectif de la séance

1. Définir ce que la preuve de faisabilité doit prouver, et ce qu'elle ne doit pas faire.
2. Regrouper les 66 tests et mesures issus de B1–B4 en lots, et compléter les tests manquants.
3. Comparer les architectures possibles au regard des règles validées.
4. Définir les conditions de test, l'effort relatif, la gouvernance et les critères de la Porte 3.

## 2. Décisions validées qui encadrent la Phase C

| Décision | Conséquence technique |
|---|---|
| **Validation de B4** : Q28 (en principe, à tester), Q29, Q30, Q31 | Les 8 contradictions ont des règles validées ; critères de la Porte 2 figés |
| Faits en ajout seul, une commande par appareil, caisses individuelles (B1) | Modèle de données **plus simple à synchroniser** qu'un modèle où tout est modifiable |
| Séquence par appareil, détection des trous, pas d'ordonnancement sur l'heure (B1) | Exigence du moteur de synchronisation |
| Remise individuelle par contact local sans internet (B1, T16) | **Communication locale entre appareils** : principale incertitude technique |
| Encaissement sur appareils de l'établissement (B1) | Gestion des appareils possible (enrôlement, verrouillage) |
| Journée explicite, services, heure de bascule (B2) | Identifiant de journée diffusé aux appareils |
| Matrice de contrôle, approbation locale par une personne présente (B2) | Authentification hors ligne de plusieurs utilisateurs sur un même appareil |
| Vérification Mobile Money côté récepteur, pas de lecture des SMS (B3) | Aucune intégration opérateur dans la preuve de faisabilité |
| Comptage à l'aveugle, transit, ambiguïtés (B3) | Logique métier, faible risque technique |
| Accès d'assistance accordé par le propriétaire (B4) | Contrôle d'accès fin et journalisé côté serveur |
| Licence locale signée, code de réactivation hors ligne, propagation locale (B4) | Cryptographie légère sur appareil ; communication locale |
| Isolation des établissements ; administrateurs sans accès par défaut ; sauvegardes restaurables (règles non négociables) | Exigences de la plateforme |
| Développement hybride ; propriété du code par la structure porteuse | Cadre contractuel avant tout développement (§9) |

---

## 3. Ce que la preuve de faisabilité doit prouver — et ne pas faire

| Elle DOIT | Elle NE DOIT PAS |
|---|---|
| Lever les **incertitudes techniques** qui pourraient rendre les règles validées irréalisables | Construire le MVP |
| Tester sur des **appareils Android d'entrée de gamme réels**, en conditions dégradées | Soigner l'interface au-delà du nécessaire pour les tests |
| Comparer au moins deux options là où l'incertitude est forte | Tester ce qui relève de la logique métier sans risque technique (ce sera la recette du MVP, Porte 4) |
| Produire des **mesures** (durées, taux de réussite, pertes, doublons) | Devenir silencieusement la base du produit sans revue |
| Documenter les résultats et les échecs | Utiliser des données réelles de clients |

**Principe : le code de la preuve de faisabilité est jetable par défaut.** Il appartient à la structure porteuse, mais sa réutilisation pour le MVP exige une **décision explicite**, après revue de sa qualité.

---

## 4. Tri des tests : ce qui va dans la preuve de faisabilité

### 4.1 Critère de tri

Un test entre dans la preuve de faisabilité s'il comporte une **incertitude technique** (synchronisation, communication locale, stockage, sécurité, performance, plateforme). Les tests de pure logique métier sont **reportés à la recette du MVP** (Porte 4), où ils restent obligatoires.

### 4.2 Lots de la preuve de faisabilité

| Lot | Thème | Tests repris de B1–B4 | Incertitude principale | Effort relatif |
|---|---|---|---|---|
| **L1** | Synchronisation et cohérence multi-appareils | T1, T2, T3, T4, T5, T6, T7, T8, T9, T10 | Absence de perte et de doublon après de longues coupures ; détection des trous de séquence ; volume (≈ 300 opérations, 3 appareils, 24 h) | **Élevé** |
| **L2** | Communication locale sans internet | T11, T16, T64 (propagation de licence) | Échange fiable entre téléphones d'entrée de gamme, sans routeur ni internet | **Élevé** (plus forte incertitude) |
| **L3** | Clôture et journée d'exploitation | T12, T13, T14, T15, T17, T18, T19, T20, T21, T22, T23 | Rattachement des opérations tardives ; statuts corrects avec appareils absents ; horloge faussée | Moyen |
| **L4** | Authentification et approbation locales | T25, T27, T29, T30, T32 + nouveaux T67–T69 | Plusieurs utilisateurs sur un appareil, hors ligne, sans auto-approbation possible | Moyen |
| **L5** | Licence hors ligne | T60, T61, T62, T63, T65 | Licence signée, code de réactivation court et sûr, suspension en fin de journée | Moyen |
| **L6** | Plateforme : isolation, sauvegarde, appareils | Nouveaux T70–T78 | Isolation entre établissements ; restauration réelle ; perte et remplacement d'un appareil ; stockage durable ; performance | **Élevé** |
| **L7** | Accès d'assistance | T59 | Accès limité, temporaire, journalisé, visible par le propriétaire | Faible |
| **L8** | Cas métier à risque technique | T36 (doublon Mobile Money entre appareils), T44 (comptage ambigu hors ligne), T45 (transit) | Comportement en synchronisation tardive | Faible à moyen |

### 4.3 Tests reportés à la recette du MVP (Porte 4)

T24, T26, T28, T31, T33, T34, T35, T37 à T43, T46 à T52, T66. Ils restent **obligatoires** avant le pilote ; ils ne présentent pas d'incertitude technique justifiant de les tester plus tôt.

Les mesures T53 à T58 (support, installation, rotation du personnel) se font **au pilote** (Porte 5).

### 4.4 Tests manquants à ajouter

La consigne de référence (§8 du prompt maître) demandait aussi : authentification et approbation locale, isolation entre établissements, sauvegarde et restauration, perte ou remplacement d'un appareil. Ils n'étaient pas encore formalisés.

| # | Test | Résultat attendu |
|---|---|---|
| T67 | Connexion hors ligne avec code personnel ; mauvais code répété | Accès refusé ; blocage temporaire après plusieurs échecs ; tentative journalisée |
| T68 | Approbation locale : l'approbateur saisit son propre code sur l'appareil de l'auteur | Approbation enregistrée au nom de l'approbateur ; refusée si approbateur = auteur |
| T69 | Retrait des droits d'un employé licencié pendant qu'un appareil est hors ligne | Retrait appliqué dès la synchronisation ; opérations faites entre-temps signalées |
| T70 | Utilisateur de l'établissement A tente d'accéder aux données de B (application et serveur) | Impossible, à tous les niveaux |
| T71 | Administrateur SaaS sans accès d'assistance accordé tente de lire des données financières détaillées | Impossible ; tentative journalisée |
| T72 | Restauration complète d'un établissement à partir d'une sauvegarde | Données identiques ; durée de restauration mesurée |
| T73 | Sauvegarde indépendante du fournisseur d'hébergement principal | Copie exploitable hors du fournisseur principal |
| T74 | Perte d'un appareil avant synchronisation complète | Perte limitée aux opérations non transmises ; ces opérations sont **identifiées** (trou de séquence) ; l'appareil perdu est révoqué |
| T75 | Remplacement d'un appareil | Nouvel appareil enrôlé en quelques minutes ; données de l'établissement récupérées ; ancien appareil révoqué |
| T76 | Stockage local : effacement par le système, mémoire pleine, mise à jour de l'application | Aucune perte d'opération non transmise |
| T77 | Données locales sur un appareil volé | Illisibles sans authentification (chiffrement local) |
| T78 | Performance sur appareil d'entrée de gamme : saisie d'une commande, ouverture de l'application, clôture avec 300 opérations | Durées sous les seuils fixés après la Phase A (chronométrage des commandes, A2 §6.3) |

---

## 5. Comparaison des architectures envisageables

### 5.1 Les briques à choisir

| Brique | Rôle |
|---|---|
| **Application en établissement** | Commandes, encaissements, stock, clôture, hors ligne |
| **Accès propriétaire** | Tableau de bord à distance, approbations, vérification Mobile Money |
| **Synchronisation** | Transport des faits, accusés de réception, idempotence |
| **Communication locale** | Échanges entre appareils sans internet (remise, licence, appareil pivot éventuel) |
| **Serveur en ligne** | Consolidation, isolation, sauvegardes, licences, accès d'assistance |

### 5.2 Application en établissement

| Option | Avantages | Limites au regard des règles validées | Coût / maintenance |
|---|---|---|---|
| **A1 — Application web installable (PWA)** | Une seule base de code ; mise à jour simple ; pas de magasin d'applications | **Stockage local pouvant être effacé** par le navigateur ou l'utilisateur (risque pour « aucune perte ») ; **communication locale sans internet très limitée** (difficile pour T16, T64) ; synchronisation en arrière-plan restreinte ; gestion des appareils limitée | Faible à moyen |
| **A2 — Application Android native** | Accès complet aux capacités du téléphone : stockage durable, communication de proximité (Bluetooth, Wi-Fi direct, interfaces de connexion de proximité), tâches en arrière-plan, gestion des appareils de l'établissement | Base de code propre à Android ; compétences spécifiques | Moyen à élevé |
| **A3 — Application multiplateforme compilée** (catégorie : frameworks multiplateformes) | Une base de code pour Android et, si besoin, d'autres plateformes ; accès à la plupart des capacités natives | Dépendance au framework ; certaines fonctions de proximité exigent du code natif | Moyen |

**Lecture** : la communication locale (L2) et la durabilité du stockage (T76) sont des exigences issues de décisions validées. Elles **défavorisent fortement A1** pour les appareils de l'établissement. A2 et A3 sont à départager en preuve de faisabilité.

### 5.3 Accès propriétaire

Le propriétaire est le plus souvent **connecté** quand il consulte (il est à distance). Ses besoins hors ligne sont faibles.

| Option | Avantages | Limites |
|---|---|---|
| **P-a — Même application que l'établissement, avec un rôle propriétaire** | Une seule application à maintenir ; vérification Mobile Money depuis le même téléphone que celui qui reçoit les paiements | Application plus lourde |
| **P-b — Application web pour le propriétaire** | Accès depuis n'importe quel téléphone ou ordinateur | Deux interfaces à maintenir |

À trancher en Phase E. Sans incertitude technique majeure : **hors preuve de faisabilité**.

### 5.4 Synchronisation

| Option | Avantages | Limites |
|---|---|---|
| **Y1 — Moteur de synchronisation existant** (catégories : bases locales avec réplication intégrée ; moteurs de synchronisation adossés à une base relationnelle) | Gain de temps ; mécanismes éprouvés | **Dépendance à un éditeur** : un service commercial de synchronisation mobile largement utilisé (MongoDB Atlas Device Sync) a été annoncé en fin de vie par son éditeur en 2024. Coûts d'usage à vérifier. Modèle imposé, pas toujours adapté aux règles métier |
| **Y2 — Synchronisation spécifique par file d'envoi** (« boîte d'envoi » sur chaque appareil, accusé de réception, clé d'idempotence par opération) | Les décisions de B1 la rendent **beaucoup plus simple** qu'une synchronisation générique : les faits ne sont jamais modifiés (simple ajout), les commandes ont un seul propriétaire (pas de fusion), les référentiels viennent du serveur (lecture seule sur l'appareil) ; aucune dépendance externe | Code à écrire et à maintenir ; **risque de dépendance à une seule personne** si mal documenté |

**Lecture** : le modèle validé en B1 réduit fortement la complexité de Y2. Les deux options doivent être prototypées sur L1 et comparées sur : absence de perte, doublons, effort, coût d'exploitation, réversibilité.

### 5.5 Communication locale

| Option | Avantages | Limites |
|---|---|---|
| **K-a — Réseau local (routeur ou point d'accès d'un appareil)** | Débit élevé | Le routeur s'éteint pendant les délestages ; le point d'accès consomme la batterie |
| **K-b — Liaison directe entre téléphones (Bluetooth, Wi-Fi direct, connexions de proximité)** | Pas d'équipement ; fonctionne pendant un délestage | Fiabilité variable selon les modèles d'entrée de gamme : **à mesurer** |
| **K-c — Codes visuels (QR) affichés et scannés** | Aucun réseau ; universel | Adapté à de petits volumes (récapitulatif de remise, licence), pas à des centaines d'opérations |

**Lecture** : tester K-b en premier, K-c comme solution de repli pour la licence et le récapitulatif de remise, K-a comme accélérateur facultatif (décision B1 : le réseau local n'est jamais nécessaire à la cohérence).

### 5.6 Serveur en ligne

| Option | Avantages | Limites |
|---|---|---|
| **B-a — Plateforme gérée (base de données et services d'authentification fournis)** | Mise en route rapide ; exploitation réduite | Dépendance ; contrôle fin de l'isolation et des accès d'administration à vérifier ; coût à l'usage |
| **B-b — Serveur applicatif spécifique sur une base de données gérée** | Maîtrise des règles d'isolation, d'accès d'assistance, de journalisation | Plus d'exploitation |

**Isolation des établissements** : trois approches à comparer en L6 : séparation par ligne avec contrôle d'accès au niveau de la base ; un schéma par établissement ; une base par établissement. Critères : sûreté de l'isolation, coût, simplicité des sauvegardes et restaurations par établissement.

**Localisation des données** : la loi burkinabè sur les données personnelles peut encadrer l'hébergement ou le transfert des données hors du pays. **À VÉRIFIER** avant le choix de l'hébergeur (lié au point juridique D-A1-17).

### 5.7 Hypothèse d'architecture à tester (non décidée)

> Application **Android** (native ou multiplateforme) sur les appareils de l'établissement + **synchronisation par file d'envoi** (comparée à un moteur existant) + **liaison directe entre téléphones** pour la remise et la licence (repli par QR) + **serveur spécifique sur base gérée** avec isolation testée + accès propriétaire à trancher en Phase E.

Cette hypothèse découle des règles validées. Elle sera confirmée ou infirmée par la preuve de faisabilité, pas par cette séance.

---

## 6. Conditions de test

| Condition | Mise en œuvre |
|---|---|
| Appareils | 3 à 4 téléphones ou tablettes Android **d'entrée de gamme**, représentatifs de ceux observés en Phase A (modèles relevés pendant les entretiens et observations) |
| Réseau | Mode avion, coupures répétées, débit dégradé, coupures pendant l'envoi |
| Énergie | Batterie faible, extinction brutale, redémarrage |
| Horloge | Heure faussée, changement de fuseau, redémarrage sans réseau |
| Durée | Coupures de 1 h, 24 h, 72 h |
| Volume | Scénario de soirée chargée : au moins 300 opérations sur 3 appareils |
| Scénarios | Rejoués à partir des **scénarios réels** de B1–B4 (table 5, téléphone de B éteint, clôture à 1 h 30, etc.) |
| Données | **Données fictives uniquement** |
| Essai en conditions réelles (facultatif) | Après les tests en atelier : une soirée simulée dans un établissement volontaire, hors service réel, avec son accord |

---

## 7. Effort, durée et budget

Aucun coût de développeur n'est connu. L'effort est donné en **taille relative** ; il sera chiffré par les prestataires consultés.

| Lot | Taille relative | Dépendances |
|---|---|---|
| L1 Synchronisation | Élevée | Choix A2/A3 (petit prototype préalable) |
| L2 Communication locale | Élevée | Appareils réels |
| L3 Clôture et journée | Moyenne | L1 |
| L4 Authentification locale | Moyenne | — |
| L5 Licence | Moyenne | L2 (propagation) |
| L6 Plateforme | Élevée | Choix du serveur |
| L7 Accès d'assistance | Faible | L6 |
| L8 Cas métier techniques | Faible à moyenne | L1 |

**Ordre recommandé** : L2 et L1 d'abord (les plus incertains, ceux qui peuvent remettre en cause des décisions validées), puis L6, puis le reste. **Règle d'arrêt anticipé** : si L2 échoue sur les appareils d'entrée de gamme, on s'arrête pour arbitrer avant de financer les autres lots (§8).

**Budget plafond de la Phase C** : à fixer après consultation d'au moins deux prestataires, **libéré par lots** (L1–L2 d'abord), conformément à la règle d'investissement progressif.

---

## 8. Critères de la Porte 3 (proposés)

| Décision | Critères |
|---|---|
| **Go** | Tous les tests des lots L1, L3, L4, L5, L6 réussis **et** aucune perte d'opération ni doublon non détecté dans aucun test **et** isolation (T70, T71) et restauration (T72, T73) prouvées **et** L2 réussi, **ou** solution de repli acceptée **et** performances (T78) sous les seuils **et** architecture retenue documentée, avec estimation de l'effort du MVP |
| **Rework** | L2 échoue sur appareils d'entrée de gamme → **réouverture explicite de décisions B1/B4** (remise individuelle sans internet, propagation de licence) avec repli par QR ou exigence de connectivité locale ; **ou** performances insuffisantes → révision des appareils cibles (impact sur Q4 et les coûts) ; **ou** une option de synchronisation échoue → poursuite avec l'autre |
| **No-Go** | Aucune architecture ne garantit l'absence de perte d'opérations hors ligne **ou** l'isolation des établissements **ou** une restauration fiable, dans un budget compatible avec le tarif de 10 000 FCFA/mois |

Une anomalie critique non résolue (sécurité, cohérence financière, isolation, conservation des transactions) **interdit** le passage à la Phase E.

---

## 9. Gouvernance, propriété intellectuelle et indépendance (avant tout code)

| Exigence | Mise en œuvre |
|---|---|
| Contrat signé **avant** le premier jour de travail | Cession des droits sur tous les livrables (code, documents, maquettes) à la structure porteuse ; confidentialité ; interdiction de réutiliser les données ou le code pour un tiers. **Rédaction sur autorisation, validation juridique** |
| Dépôt de code | Sur un compte appartenant à la structure porteuse ; le prestataire y a un accès révocable |
| Comptes d'administration | Hébergement, magasin d'applications, noms de domaine, clés de signature : **au nom de la structure**, jamais au nom du prestataire |
| Secrets | Gestionnaire de secrets contrôlé par la structure ; aucun secret dans le code ; rotation à la fin de chaque mission |
| Documentation | Livrable obligatoire de chaque lot : décisions techniques, résultats des tests, procédure d'installation de l'environnement |
| Reprise par un autre développeur | Critère d'acceptation : un développeur tiers doit pouvoir relancer les tests à partir de la documentation |
| Revue indépendante | Revue des résultats de la preuve de faisabilité par un second profil technique avant la Porte 3 (même logique que le regard extérieur de la Porte 1) |
| Sauvegardes indépendantes | Testées dans L6 (T73) |

**Profil recherché** : développeur senior ayant déjà livré une application mobile **hors ligne** synchronisée, avec expérience de sécurité des données. La disponibilité de ce profil à Ouagadougou, et son coût, sont **à vérifier**.

---

## 10. Limites

- Une preuve de faisabilité réussie ne garantit pas un produit fiable : elle montre que les règles sont **réalisables**. La fiabilité se prouve à la recette du MVP et au pilote.
- Les appareils testés ne représentent pas tous les modèles des clients ; la politique d'équipement (Q4) réduira cette variabilité.
- L'effort réel ne sera connu qu'après consultation des prestataires.

---

## 11. Décisions à prendre

| # | Question | Recommandation |
|---|---|---|
| **Q32** | Validez-vous le **tri des tests** : preuve de faisabilité limitée aux incertitudes techniques (L1–L8), logique métier reportée à la recette du MVP, et ajout des tests T67 à T78 ? | Oui |
| **Q33** | Validez-vous l'**hypothèse d'architecture à tester** (§5.7), avec comparaison de deux options de synchronisation, et l'abandon de la PWA seule pour les appareils de l'établissement ? | Oui |
| **Q34** | Validez-vous l'**ordre des lots** (L2 et L1 d'abord) et la **règle d'arrêt** en cas d'échec de L2 ? | Oui |
| **Q35** | Validez-vous les **exigences de gouvernance** (§9) comme conditions préalables à toute mission, et le principe du **code jetable par défaut** ? | Oui |
| **Q36** | Validez-vous les **critères de la Porte 3** (§8) ? | Oui, à figer avant le début de la Phase C |

---

## 12. Registre des décisions (mise à jour séance C0)

| ID | Élément | Statut |
|---|---|---|
| D-B4-01 à D-B4-19 | Décisions de la séance B4 | **VALIDÉ** (D-B4-03 en principe, à tester ; D-B4-08 REPORTÉ ; D-B4-13 en principe, durées contractuelles) |
| C1–C8 | Huit contradictions | **VALIDÉ** (règles) · BLOQUANT jusqu'à réussite des tests ; C7 jusqu'aux mesures du pilote |
| Porte 2 | Critères (B4 §6) | **VALIDÉ** |
| D-C0-01 | Code de la preuve de faisabilité jetable par défaut ; réutilisation sur décision explicite | **VALIDÉ** (Q35) |
| D-C0-02 | Tri des tests : technique en Phase C, logique métier à la recette du MVP | **VALIDÉ** (Q32) |
| D-C0-03 | Tests T67 à T78 (authentification, isolation, sauvegarde, appareils, performance) | **VALIDÉ** (Q32) |
| D-C0-04 | Hypothèse d'architecture à tester (§5.7) ; PWA seule écartée pour l'établissement | **VALIDÉ** comme hypothèse à tester (Q33) |
| D-C0-05 | Comparaison de deux options de synchronisation (moteur existant / file d'envoi spécifique) | **VALIDÉ** (Q33) |
| D-C0-06 | Communication locale : liaison directe d'abord, QR en repli, réseau local facultatif | **VALIDÉ** (Q33) |
| D-C0-07 | Trois approches d'isolation comparées en L6 | **VALIDÉ** |
| D-C0-08 | Accès propriétaire (même application ou web) | REPORTÉ (Phase E) |
| D-C0-09 | Localisation de l'hébergement au regard de la loi sur les données | À VÉRIFIER (lié à D-A1-17) |
| D-C0-10 | Ordre des lots et règle d'arrêt sur L2 | **VALIDÉ** (Q34) |
| D-C0-11 | Conditions de test (appareils d'entrée de gamme, coupures, horloge, volume, données fictives) | **VALIDÉ** |
| D-C0-12 | Budget de la Phase C : après consultation d'au moins 2 prestataires, libéré par lots | **VALIDÉ** |
| D-C0-13 | Exigences de gouvernance et de propriété intellectuelle avant toute mission | **VALIDÉ** (Q35) · contrats sur autorisation, validation juridique |
| D-C0-14 | Revue technique indépendante avant la Porte 3 | **VALIDÉ** |
| D-C0-15 | Critères de la Porte 3 | **VALIDÉ** (Q36) |
| D-C0-16 | Disponibilité et coût du profil technique à Ouagadougou | À VÉRIFIER |
| D-C0-17 | Exécution de la Phase C : après Portes 1 et 2, sur autorisation explicite | **VALIDÉ** (règle absolue du projet) |

---

## 13. Validation (fin de séance)

Le fondateur a validé l'ensemble : Q32 à Q36. Le tri des tests, les tests T67 à T78, l'hypothèse d'architecture **à tester**, l'ordre des lots avec la règle d'arrêt sur L2, les exigences de gouvernance, le code jetable par défaut et les critères de la Porte 3 sont figés. L'exécution reste conditionnée aux Portes 1 et 2 et à une autorisation explicite.

---

## 14. Prochaine étape proposée

| Option | Contenu |
|---|---|
| **D0 — Structure du modèle financier** | Postes de coûts et de revenus, variables clés (temps de support, équipement, hébergement, commissions, coût de la Phase C et du MVP), scénarios prudent / central / défavorable, **sans chiffres inventés** ; liste des données à collecter en Phase A, en Phase C et au pilote |
| **Consolidation** | Registre unique des décisions et des risques, regroupant A1 à C0 (livrable « registre des décisions » : **sur votre autorisation**) |
| **Retour au terrain** | Lever Q3 et le cadre légal, puis démarrer S0 |

**Recommandation** : **D0**, car c'est la dernière pièce d'analyse qui manque avant de pouvoir juger la viabilité d'ensemble. Ensuite, la priorité absolue redevient le **terrain de la Phase A**, toujours bloqué par Q3 et le cadre légal des entretiens.
