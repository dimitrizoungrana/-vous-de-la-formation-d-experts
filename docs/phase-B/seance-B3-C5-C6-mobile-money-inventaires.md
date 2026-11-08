# MAQUIS CONTROL — Séance B3
## Phase B · Contradictions C5 (paiements Mobile Money) et C6 (inventaires en cours de service)

> **Statut** : compte rendu de séance de brainstorming (analyse métier, principes de conception). Ni architecture, ni cahier des charges, ni code.
> Aucune donnée sur les tarifs, commissions ou interfaces techniques des opérateurs Mobile Money n'est supposée : ces points sont **à vérifier**.

---

## 1. Objectif de la séance

Résoudre C5 et C6 selon la méthode : scénario, risques, options, recommandation, décisions métier, tests, classement. Traiter aussi la limite identifiée en B1 : **seul le stock permet de détecter une vente jamais saisie**.

## 2. Décisions validées qui encadrent C5 et C6

| Décision validée | Lien |
|---|---|
| Paiement **déclaré / vérifié / rapproché** (règle non négociable) | Cadre de C5 |
| Caisse individuelle par encaisseur, remise individuelle obligatoire (B1) | Un paiement Mobile Money déclaré réduit l'argent liquide attendu de la personne qui l'a déclaré |
| Même référence Mobile Money déclarée deux fois → doublon détecté (test T3, B1) | Base de C5 |
| Clôture en deux temps ; complétude et niveau de contrôle distincts (B1, B2) | Un paiement non vérifié ne peut pas apparaître comme encaissé de façon certaine |
| Matrice de contrôle et auto-validation marquée (B2) | S'applique à la vérification Mobile Money et aux inventaires |
| Déstockage à la remise confirmée ; transferts en deux temps ; écarts traités explicitement ; inventaires quotidiens possibles (règles non négociables) | Cadre de C6 |
| Stock négatif autorisé avec alerte (B1) | C6 |
| Journée d'exploitation explicite (B2) | Rattachement des comptages |
| Faits jamais modifiés ; corrections par opérations journalisées (B1) | Ajustements d'inventaire |
| **Validation de la séance B2** : Q20 à Q23 et M14 à M26 | VALIDÉ ; vérification fiscale lancée (premiers résultats en B2 §9) |

---

## 3. C5 — Paiements Mobile Money

### 3.1 Scénarios réels

Les clients paient par Orange Money ou Moov Money en envoyant de l'argent à un numéro.

- **A — Faux SMS** : un client montre au serveur un SMS de confirmation sur **son propre** téléphone, ou une capture d'écran. Le serveur déclare « payé ». L'argent n'est jamais arrivé.
- **B — Numéro personnel** : le client paie sur le numéro personnel du serveur, « parce que c'est plus simple ». L'argent est sur le compte du serveur, pas de l'établissement.
- **C — Fausse déclaration interne** : le client paie en espèces ; le serveur déclare un paiement Mobile Money et garde les espèces.
- **D — Une référence pour deux tables** : la même transaction est déclarée pour deux additions.
- **E — Double rapprochement** : lors du pointage, une même transaction de l'opérateur est rattachée à deux paiements déclarés.
- **F — Paiement partiel** : le client envoie 4 000 FCFA au lieu de 6 000 ; le reste en espèces, ou jamais.
- **G — Propriétaire absent** : les paiements arrivent sur le téléphone du propriétaire, qui n'est pas au maquis.

### 3.2 Risques

| Risque | Opérationnel | Financier |
|---|---|---|
| Paiement déclaré mais jamais reçu (A, C) | Écart découvert tard, responsabilité floue | **Perte directe** |
| Fonds sur un numéro non officiel (B) | L'argent de l'établissement est chez un employé | Perte ou retard de remise |
| Doublons (D, E) | Encaissements surestimés | Écart masqué |
| Montant partiel (F) | Addition « soldée » à tort | Perte |
| Vérification impossible faute d'accès au compte qui reçoit (G) | Paiements qui restent « déclarés » indéfiniment | Contrôle illusoire |

**Classement : CRITIQUE** (cohérence financière ; vecteur de fraude majeur, en hausse avec l'usage du Mobile Money).

### 3.3 Principe clé : on ne vérifie que du côté de celui qui reçoit

Un SMS montré par le client ne prouve rien : il peut être faux, ancien ou concerner un autre destinataire. **Seul le compte qui reçoit l'argent fait foi.** Un paiement passe au statut « vérifié » uniquement lorsqu'une personne ayant accès au compte récepteur (ou un mécanisme relié à ce compte) a constaté sa réception.

### 3.4 Options de vérification comparées

| Option | Principe | Avantages | Limites | Coût / complexité |
|---|---|---|---|---|
| **V1 — Vérification manuelle sur le téléphone récepteur** | La personne qui détient le téléphone (ou le compte) recevant les paiements consulte ses notifications ou son historique et coche « reçu » dans l'application, avec la référence | Aucun accord avec un opérateur ; fonctionne dès le premier jour ; **le propriétaire absent peut vérifier à distance** si les paiements arrivent sur son téléphone | Dépend de la rigueur de la personne ; en cumul de rôles, auto-vérification (marquée) | Faible |
| **V2 — Lecture automatique des SMS sur le téléphone récepteur** | L'application lit les SMS de l'opérateur et rapproche automatiquement | Moins de saisie | Les règles des magasins d'applications **restreignent fortement** l'accès aux SMS (à vérifier) ; formats de SMS changeants ; usurpation de l'expéditeur possible ; données personnelles | Moyenne, **fragile** |
| **V3 — Intégration avec l'opérateur ou un agrégateur de paiement** | Le paiement est initié ou confirmé par une interface technique de l'opérateur ; la confirmation arrive automatiquement | Vérification la plus fiable ; rapprochement automatique | Contrat marchand, conditions d'accès pour les petits commerces, commissions, délais d'intégration et dépendance : **tout est à vérifier** | Élevée |
| **V4 — Rapprochement périodique avec l'historique du compte** | Chaque jour, la liste des paiements déclarés est pointée contre l'historique des transactions du compte récepteur | Rattrape les erreurs de V1 ; détecte les déclarations jamais reçues | Charge manuelle ; dépend de la disponibilité d'un historique exploitable (à vérifier selon le type de compte) | Faible à moyenne |

### 3.5 Recommandation pour C5

**Pour le MVP : V1 + V4. V3 étudiée en Phase C/D comme évolution. V2 écartée sauf preuve contraire.**

**Règle 1 — Numéros officiels de réception**
- L'établissement déclare, à l'installation, ses **numéros officiels** de réception (un par opérateur au minimum), détenus par l'établissement ou par le propriétaire.
- Un paiement reçu sur un **autre numéro** (personnel d'un employé) est enregistré comme tel. Il est traité **comme de l'argent détenu par cette personne** : il entre dans sa remise individuelle, qu'elle doit transférer sur le numéro officiel ou remettre en espèces. Il est signalé au propriétaire.

**Règle 2 — Une déclaration complète**
- Tout paiement Mobile Money déclaré comporte : opérateur, montant, **référence de la transaction**, numéro récepteur, table ou commande, auteur.
- La référence est **unique** pour l'établissement : une seconde déclaration avec la même référence est un doublon signalé (T3, validé).
- Un paiement partiel est déclaré pour son montant réel ; le solde reste dû sur l'addition.

**Règle 3 — Trois statuts, trois sens**

| Statut | Qui / quoi | Effet |
|---|---|---|
| **Déclaré** | L'encaisseur | Réduit l'argent liquide attendu de l'encaisseur, **sous sa responsabilité** tant que le paiement n'est pas vérifié |
| **Vérifié** | Une personne ayant accès au compte récepteur, différente du déclarant si possible (sinon auto-vérification marquée, matrice B2) | Le paiement est considéré comme reçu |
| **Rapproché** | Pointage contre l'historique du compte : **une transaction de l'opérateur = un seul paiement déclaré** | Le paiement est définitivement justifié |

**Règle 4 — À la clôture**
- La clôture distingue : espèces comptées, Mobile Money vérifié, Mobile Money **déclaré non vérifié**.
- Un paiement déclaré non vérifié **n'est jamais** présenté comme encaissé de façon certaine.
- Au-delà d'un délai de vérification (paramètre), un paiement non vérifié devient un **écart attribué à la caisse individuelle du déclarant**, à traiter selon la matrice de contrôle.

**Règle 5 — Le propriétaire absent comme vérificateur**
Si les paiements arrivent sur le téléphone du propriétaire, celui-ci peut **vérifier à distance** quand il est connecté : c'est une vraie vérification (pas une approbation fictive) et un argument fort pour la promesse « même à distance ».

**Règle 6 — Mouvements de trésorerie distincts des ventes**
Un retrait d'argent du compte Mobile Money, ou un transfert vers un autre compte, est un **mouvement de trésorerie**, jamais une vente ni un encaissement. Les frais éventuels des opérateurs sont des charges, enregistrées comme telles.

### 3.6 Décisions métier nécessaires pour C5

| # | Décision | Proposition par défaut |
|---|---|---|
| M27 | Numéros officiels de réception déclarés à l'installation | Oui |
| M28 | Paiement sur un numéro non officiel : traité comme argent détenu par le receveur, intégré à sa remise, signalé | Oui ; et **interdit par la charte d'utilisation** (M24), toléré techniquement car il arrivera |
| M29 | Référence de transaction obligatoire et unique | Oui ; faisabilité de la saisie à tester (longueur des références, rapidité) |
| M30 | Vérification uniquement depuis le compte récepteur, par une personne différente du déclarant quand c'est possible | Oui |
| M31 | Rapprochement quotidien avec l'historique ; une transaction opérateur = un seul paiement | Oui |
| M32 | Délai de vérification avant transformation en écart du déclarant | Paramètre ; valeur après le pilote |
| M33 | Lecture automatique des SMS (V2) | **Non**, sauf preuve de conformité et de fiabilité |
| M34 | Étude d'une intégration opérateur ou agrégateur (V3) | REPORTÉ en Phase C/D (conditions d'accès, coûts, dépendance) |

### 3.7 Points à vérifier sur le terrain (Phase A)

| Point | Où le relever |
|---|---|
| Sur quels numéros arrivent les paiements (établissement, propriétaire, gérant, serveurs) | Entretien bloc 1 (question 9), observation §6.5 |
| Qui consulte ces numéros, et comment | Entretien, observation |
| Existence d'un compte marchand, et d'un historique consultable ou exportable | Entretien (à noter si mentionné) |
| Part des paiements Mobile Money (H12) | Entretien, observation |
| Fréquence des faux SMS et des paiements « annoncés mais pas arrivés » | Entretien bloc 2 |

### 3.8 Tests C5

| # | Test | Résultat attendu |
|---|---|---|
| T34 | Paiement déclaré, jamais reçu | Reste « déclaré » ; après le délai, écart attribué au déclarant ; jamais compté comme encaissé certain |
| T35 | Vérification depuis le téléphone du client (faux SMS) | Impossible : seul le compte récepteur permet de vérifier |
| T36 | Même référence déclarée pour deux additions | Doublon signalé ; un seul paiement vérifiable |
| T37 | Paiement sur le numéro personnel d'un serveur | Enregistré comme détenu par le serveur ; inclus dans sa remise ; signalé |
| T38 | Le déclarant tente de vérifier son propre paiement alors qu'un vérificateur est disponible | Refusé |
| T39 | Une transaction opérateur rattachée à deux paiements au rapprochement | Refusé |
| T40 | Clôture avec Mobile Money non vérifié | Montant affiché séparément « à vérifier » ; niveau de contrôle correct |
| T41 | Vérification à distance par le propriétaire connecté / hors ligne | Connecté : enregistrée avec son identité ; hors ligne : impossible, le paiement reste déclaré |
| T42 | Paiement partiel | Solde restant dû sur l'addition ; pas de solde « payé » à tort |

---

## 4. C6 — Inventaires en cours de service

### 4.1 Scénario réel

Bar avec une réserve, un bar et deux réfrigérateurs. Le gérant veut compter à 20 h, pendant le service.

- Il compte le réfrigérateur 1 : 18 bouteilles d'une marque. Deux minutes plus tard, un serveur en sort 3 et confirme leur remise sur son téléphone, qui est hors ligne.
- Pendant ce temps, un transfert réserve → bar est **parti** mais pas encore **reçu**.
- Un livreur arrive avec 10 casiers pendant le comptage de la réserve.
- Le gérant connaît le stock théorique affiché : il est tenté d'« arrondir » son comptage pour qu'il corresponde.
- Le lendemain, les comptes montrent 6 bouteilles manquantes. Personne ne sait si c'est une vente non saisie, une erreur de comptage, une casse ou le transfert en cours.

### 4.2 Pourquoi C6 est plus important qu'il n'y paraît

Les séances B1 et B2 ont montré deux limites :
- **Aucune règle ne protège contre une vente jamais saisie** (B1).
- **En cumul de rôles, les contrôles sont surtout détectifs** (B2).

Dans les deux cas, le contrôle qui reste est **le rapprochement entre le stock théorique et le stock compté**. Une boisson servie sans être saisie disparaît physiquement : l'inventaire la fait apparaître comme écart. **Un inventaire fiable est donc la colonne vertébrale de la promesse « sous contrôle, même à distance ».**

### 4.3 Risques

| Risque | Opérationnel | Financier |
|---|---|---|
| Mouvements pendant le comptage | Écarts faux (positifs ou négatifs) | Fausses accusations ou pertes masquées |
| Comptage ajusté sur le théorique | Inventaire sans valeur | Pertes masquées |
| Transferts en cours oubliés | Écart fictif sur deux emplacements | Idem |
| Inventaire trop long ou trop fréquent | Abandonné par le personnel | Plus de contrôle du tout |
| Écart corrigé sans explication | Le stock « tombe juste » artificiellement | Perte masquée, journal sans valeur |

**Classement : MAJEUR**, avec un effet direct sur la valeur perçue du produit.

### 4.4 Options comparées

| Option | Principe | Avantages | Limites | Complexité |
|---|---|---|---|---|
| **I1 — Comptage hors service** | Inventaire complet à la clôture ou avant l'ouverture, quand rien ne bouge | Le plus fiable ; simple à expliquer | Fatigue à 2 h du matin ; une seule photo par jour | Faible |
| **I2 — Comptage par emplacement avec gel** | On compte un emplacement à la fois ; pendant ce temps, les mouvements **depuis ou vers cet emplacement** sont suspendus | Fiable pour la réserve (pas de service direct depuis la réserve) | Impossible de geler le bar ou un réfrigérateur en pleine pointe | Moyenne |
| **I3 — Comptage avec point de référence** | Chaque article compté reçoit un « point de comptage » ; le système compare au théorique **à ce point précis** et traite les mouvements postérieurs séparément | Permet un comptage ciblé en service | Avec des appareils hors ligne et des horloges peu fiables, les mouvements proches du point de comptage sont **ambigus** | Élevée |
| **I4 — Inventaire tournant** | Chaque jour, quelques articles clés (les plus vendus ou les plus volés) ; inventaire complet hebdomadaire | Effort quotidien réduit ; détection rapide sur les articles qui comptent | Couverture partielle chaque jour | Faible à moyenne |

### 4.5 Recommandation pour C6

**Combiner I1, I2 et I4 ; limiter I3 à des comptages ciblés, avec signalement des ambiguïtés.**

**Règle 1 — Moments de comptage**
- **Inventaire complet** : hors service, à la clôture **ou** avant l'ouverture (choix par établissement). Le comptage avant ouverture est souvent moins pénible, à condition que la réserve soit fermée la nuit.
- **Réserve** : peut être comptée à tout moment, avec **gel** des transferts depuis et vers la réserve pendant le comptage (les transferts attendent quelques minutes).
- **Inventaire tournant quotidien** : quelques articles clés, choisis par le propriétaire ou par le système (articles à forte rotation, à écarts fréquents).
- **Comptage ciblé en service** (bar, réfrigérateur) : autorisé, avec point de comptage ; les remises confirmées par d'autres appareils autour du point de comptage sont **marquées ambiguës** et l'écart correspondant est présenté comme **provisoire**.

**Règle 2 — Comptage à l'aveugle**
La personne qui compte **ne voit pas** le stock théorique. Elle saisit ce qu'elle voit. L'écart n'apparaît qu'après validation du comptage, avec une possibilité de **recompter une fois** l'article concerné.

**Règle 3 — Unités réelles**
Saisie en **casiers + bouteilles** (et autres conditionnements), avec conversion par produit configurée à l'installation. Compter « 3 casiers et 7 bouteilles » est plus rapide et plus sûr que « 67 bouteilles ».

**Règle 4 — Mouvements en cours**
- **Transfert parti mais non reçu** : la quantité est en **transit**, comptée ni au départ ni à l'arrivée. Le théorique en tient compte.
- **Livraison pendant un comptage** : sa réception est enregistrée **après** la fin du comptage de l'emplacement concerné, ou les produits livrés sont mis à part jusqu'à la fin du comptage.

**Règle 5 — Traitement des écarts**
- Aucun écart n'est corrigé automatiquement.
- Chaque écart reçoit une **catégorie** : casse, boisson offerte non saisie, erreur de comptage, transfert non enregistré, vol présumé, non expliqué.
- L'ajustement est une opération journalisée, approuvée selon la matrice B2 (par une personne différente du compteur quand c'est possible ; sinon auto-validée marquée, avec comptage surprise recommandé au propriétaire).
- L'écart est **valorisé deux fois** : au prix d'achat (perte réelle) et au prix de vente (manque à gagner). Cela suppose de connaître le **prix d'achat** de chaque boisson, nécessaire aussi pour distinguer ventes et bénéfice.

**Règle 6 — Emballages consignés (selon H18)**
Si les observations confirment que les casiers et bouteilles vides sont un enjeu de contrôle, ils sont comptés **au même moment** que les boissons pleines. Pour une consommation sur place, une bouteille vendue laisse une bouteille vide : le comptage des vides est un **contrôle indépendant** des ventes saisies. *Hypothèse à vérifier sur le terrain avant tout ajout au périmètre.*

### 4.6 Décisions métier nécessaires pour C6

| # | Décision | Proposition par défaut |
|---|---|---|
| M35 | Inventaire complet hors service (clôture ou avant ouverture, au choix de l'établissement) | Oui |
| M36 | Gel des transferts de la réserve pendant son comptage | Oui |
| M37 | Inventaire tournant quotidien des articles clés + inventaire complet hebdomadaire | Oui ; fréquence ajustable après pilote |
| M38 | Comptage ciblé en service autorisé, avec ambiguïtés signalées et écart provisoire | Oui |
| M39 | Comptage à l'aveugle avec un recomptage autorisé | Oui |
| M40 | Saisie en conditionnements réels (casiers + bouteilles) | Oui |
| M41 | Catégories d'écart, aucun ajustement automatique, approbation selon la matrice B2 | Oui |
| M42 | Valorisation des écarts au prix d'achat et au prix de vente ; prix d'achat renseigné dans le catalogue | Oui |
| M43 | Comptage des emballages consignés | À VÉRIFIER SUR LE TERRAIN (H18) avant décision |

### 4.7 Tests C6

| # | Test | Résultat attendu |
|---|---|---|
| T43 | Comptage à l'aveugle | Le théorique n'est jamais affiché avant la validation du comptage |
| T44 | Remise confirmée hors ligne par un autre appareil juste après le comptage d'un réfrigérateur | Mouvement marqué ambigu ; écart provisoire ; consolidé après synchronisation |
| T45 | Transfert parti non reçu pendant l'inventaire | Quantité en transit ; aucun écart fictif au départ ou à l'arrivée |
| T46 | Livraison pendant le comptage de la réserve | Réception enregistrée après le comptage ; pas de double comptage |
| T47 | Transfert demandé depuis la réserve en cours de comptage | Mis en attente jusqu'à la fin du comptage |
| T48 | Ajustement d'écart par la personne qui a compté, un approbateur étant présent | Refusé |
| T49 | Ajustement en cumul de rôles | Auto-validé marqué ; visible par le propriétaire |
| T50 | Saisie « 3 casiers + 7 bouteilles » | Conversion correcte selon le conditionnement du produit |
| T51 | Écart valorisé | Deux valeurs affichées (prix d'achat, prix de vente) |
| T52 | Inventaire tournant | Les articles proposés couvrent les articles à forte rotation ou à écarts récents |

---

## 5. Coût, maintenance et rentabilité

| Point | Analyse |
|---|---|
| V1 + V4 n'exigent aucun accord avec un opérateur | Démarrage possible sans dépendance externe ni commission supplémentaire |
| V3 (intégration opérateur) | Fiabilité supérieure, mais coûts, contrats et maintenance à évaluer en Phase D au regard du tarif de 10 000 FCFA/mois |
| Charge de rapprochement manuel | Si elle est trop lourde, elle sera abandonnée. Elle doit tenir en quelques minutes par jour : à mesurer au pilote |
| Inventaires | Le temps de comptage est le principal coût caché pour le client. Comptage en conditionnements réels et inventaire tournant le réduisent |
| Prix d'achat dans le catalogue | Donnée supplémentaire à saisir et à maintenir ; indispensable pour le bénéfice et la valorisation des écarts |

---

## 6. Limites

- La vérification Mobile Money reste **manuelle** dans le MVP : sa qualité dépend de la personne qui détient le téléphone récepteur.
- En cumul de rôles, le gérant peut déclarer, vérifier et rapprocher seul (marqué comme tel). Le contrôle repose alors sur le propriétaire.
- L'inventaire détecte une perte ; il n'en identifie pas toujours la cause ni la personne.
- Les comptages ciblés en service resteront imparfaits tant que des appareils sont hors ligne.

---

## 7. Décisions à prendre

| # | Question | Recommandation |
|---|---|---|
| **Q24** | Validez-vous le dispositif Mobile Money : vérification du côté du récepteur (V1) + rapprochement quotidien (V4), numéros officiels, référence unique, paiement non vérifié sous la responsabilité du déclarant (M27 à M32) ? | Oui |
| **Q25** | Validez-vous l'exclusion de la lecture automatique des SMS (M33) et le report de l'étude d'intégration opérateur en Phase C/D (M34) ? | Oui |
| **Q26** | Validez-vous le dispositif d'inventaire : hors service + réserve gelée + tournant quotidien + ciblé en service, comptage à l'aveugle, écarts catégorisés et approuvés, valorisation double (M35 à M42) ? | Oui |
| **Q27** | Le prix d'achat de chaque boisson devient une donnée obligatoire du catalogue (M42). Validez-vous cet ajout au Module 1 ? | Oui (nécessaire pour distinguer vente et bénéfice) |

---

## 8. Registre des décisions (mise à jour séance B3)

| ID | Élément | Statut |
|---|---|---|
| D-B2-01 à D-B2-15, D-B2-17 | Décisions de la séance B2 | **VALIDÉ** |
| D-B2-16 | Facture électronique certifiée | VÉRIFICATION LANCÉE · premiers résultats non concluants (B2 §9) |
| D-B3-01 | Vérification uniquement du côté du compte récepteur | **VALIDÉ** (Q24) |
| D-B3-02 | Numéros officiels ; paiement sur numéro non officiel = argent détenu par le receveur (M27, M28) | **VALIDÉ** (Q24) |
| D-B3-03 | Référence unique obligatoire ; paiement partiel déclaré pour son montant réel (M29) | **VALIDÉ** (Q24) · saisie à tester |
| D-B3-04 | Statuts déclaré / vérifié / rapproché et leurs effets (M30, M31) | **VALIDÉ** (Q24) |
| D-B3-05 | Paiement non vérifié au-delà du délai = écart du déclarant (M32) | **VALIDÉ** (Q24) · délai après pilote |
| D-B3-06 | Retraits et transferts Mobile Money = trésorerie, jamais ventes | **VALIDÉ** |
| D-B3-07 | Pas de lecture automatique des SMS (M33) | **VALIDÉ** (Q25) |
| D-B3-08 | Étude d'intégration opérateur ou agrégateur (M34) | **REPORTÉ** en Phase C/D (Q25) |
| D-B3-09 | Dispositif d'inventaire (M35 à M38) | **VALIDÉ** (Q26) |
| D-B3-10 | Comptage à l'aveugle, un recomptage (M39) | **VALIDÉ** (Q26) |
| D-B3-11 | Saisie en conditionnements réels (M40) | **VALIDÉ** (Q26) |
| D-B3-12 | Écarts catégorisés, jamais corrigés automatiquement (M41) | **VALIDÉ** (Q26) |
| D-B3-13 | Valorisation double ; prix d'achat obligatoire au catalogue (M42) | **VALIDÉ** (Q26, Q27) |
| D-B3-14 | Emballages consignés (M43) | À VÉRIFIER SUR LE TERRAIN (H18) |
| D-B3-15 | Points Mobile Money à relever en Phase A (§3.7) | **VALIDÉ** |
| D-B3-16 | Tests T34 à T52 ajoutés au plan de la preuve de faisabilité | **VALIDÉ** |
| C5 | Paiements Mobile Money | **BLOQUANT** jusqu'à réussite des tests T34–T42 |
| C6 | Inventaires en cours de service | **BLOQUANT** jusqu'à réussite des tests T43–T52 |

---

## 9. Validation (fin de séance)

Le fondateur a validé l'ensemble : Q24 à Q27 et les valeurs par défaut M27 à M42. M34 (intégration opérateur) est reporté en Phase C/D ; M43 (emballages consignés) reste à vérifier sur le terrain. C5 et C6 restent **BLOQUANTS** jusqu'à la réussite des tests T34 à T52.

**Conséquence à suivre** : le prix d'achat devient une donnée obligatoire du catalogue (Module 1). Sa saisie et sa mise à jour (variations de prix des fournisseurs) ajoutent une charge à l'installation et au support (C7).

---

## 10. Prochaine étape proposée

**Séance B4 — C7 (rentabilité du support) et C8 (abonnement expiré hors ligne).**
- C7 : combien coûtent réellement l'installation assistée et l'assistance à distance, au regard des décisions B1 à B3 (plusieurs appareils, anomalies à expliquer, inventaires, rapprochements), et comment les tenir dans un abonnement de 10 000 FCFA/mois.
- C8 : comment appliquer une licence, la période de grâce de 7 jours et une suspension sur des appareils hors ligne, **sans jamais perdre ni bloquer l'accès du client à ses données**.

B4 clôturera la revue des huit contradictions et préparera la Porte 2.
