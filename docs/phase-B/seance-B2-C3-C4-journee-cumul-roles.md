# MAQUIS CONTROL — Séance B2
## Phase B · Contradictions C3 (journée d'exploitation après minuit) et C4 (cumul des rôles)

> **Statut** : compte rendu de séance de brainstorming (analyse métier, principes de conception). Ni architecture, ni cahier des charges, ni code.
> Chevauchement avec la Phase A : analyse documentaire uniquement, sans décision d'investissement ; la Porte 1 n'est pas contournée.

---

## 1. Objectif de la séance

Résoudre C3 et C4 selon la méthode : scénario, risques, options, recommandation, décisions métier, tests, classement.

## 2. Décisions validées qui encadrent C3 et C4

| Décision (séance B1, validée) | Lien |
|---|---|
| Ouverture de service obligatoire par appareil (M13) | Support naturel de la journée d'exploitation (C3) |
| Ordonnancement par numéro de séquence, jamais par la seule heure de l'appareil | C3 ne peut pas reposer sur l'horloge des téléphones |
| Opérations tardives rattachées à leur **journée d'origine** (Q19) | Exige une définition fiable de la journée (C3) |
| Clôture en deux temps, 5 statuts ; remise individuelle obligatoire | C3 et C4 |
| Déclaration d'appareil absent par une personne **différente** du préparateur (M11) | Que faire quand il n'y a qu'une personne ? (C4) |
| Règles non négociables : pas d'auto-approbation quand la séparation est requise ; approbation hors ligne par une personne présente et habilitée ; un absent n'approuve pas fictivement | Cadre direct de C4 |

---

## 3. Point de vigilance juridique découvert pendant la séance : la facture électronique certifiée

En vérifiant si une règle légale encadre la « journée » de caisse, une obligation fiscale importante est apparue. Elle dépasse C3 et touche tout le produit.

**Ce que disent les sources consultées** (à confirmer auprès de la Direction générale des impôts ou d'un fiscaliste) :
- La **facture normalisée** existe depuis le 1er mars 2017. Elle était réservée au régime du réel normal, et son usage a été rendu obligatoire en mars 2022 pour le réel simplifié et la contribution des micro-entreprises.
- La **facture électronique certifiée (FEC)**, émise par un système électronique certifié de facturation (**SECeF**), remplace la facture normalisée papier pour les contribuables concernés. Les sources ne sont pas d'accord sur la date d'entrée en vigueur (1er janvier 2025 selon une source, 1er juillet 2026 selon une autre).
- Un communiqué conjoint de la DGI et de la Chambre de commerce, daté du 28 août 2026, annonce un **déploiement par étapes** des systèmes de facturation : à partir du 7 septembre 2026 pour les contribuables de la Direction des grandes entreprises et les **éditeurs de logiciels** ; puis le 2 novembre 2026 et le 1er décembre 2026 pour d'autres catégories de contribuables.

**Ce que l'on ne sait pas encore**
- Si, et quand, les maquis relevant des petits régimes (micro-entreprises notamment) doivent émettre des factures électroniques certifiées pour leurs ventes.
- Si un logiciel de caisse qui émet des tickets doit lui-même être **certifié**, ou **connecté** à un système certifié, ou s'il peut rester un outil de gestion interne.
- Quelles règles s'imposent alors : numérotation, impossibilité de modifier un document, clôture journalière, transmission à l'administration.

**Pourquoi c'est important**

| Enjeu | Conséquence possible |
|---|---|
| Périmètre et coût | Une certification ou une intégration obligatoire peut changer le coût de développement et le délai de lancement |
| Positionnement | MAQUIS CONTROL peut être un **outil de contrôle interne** qui n'émet pas de factures, ou devenir un outil d'aide à la conformité. Ce choix doit être conscient |
| Confiance (H15) | La crainte « mes chiffres vont aux impôts » est déjà identifiée. La façon d'en parler en entretien et en démo doit rester honnête et prudente |
| Opportunité | Si l'obligation s'étend aux petits établissements, une solution conforme et simple pourrait devenir un argument d'achat. **Hypothèse non vérifiée** |

**Classement : MAJEUR, potentiellement BLOQUANT pour le périmètre** (pas pour la Phase A). Une vérification auprès d'une source officielle ou d'un fiscaliste local est nécessaire **avant la Porte 2**.

**Consigne pour la Phase A** : pendant les entretiens, **ne pas aborder le sujet fiscal** de soi-même (cela biaiserait H15). Noter seulement ce que disent les propriétaires spontanément, notamment s'ils ont reçu des consignes sur la facture électronique.

---

## 4. C3 — Journée d'exploitation après minuit

### 4.1 Scénario réel

Un snack-maquis ouvre à 11 h pour le déjeuner (équipe de jour), passe le relais à 17 h à l'équipe du soir, et ferme vers 3 h le samedi, vers 23 h 30 en semaine.

- Une bière servie à 0 h 40 le dimanche appartient à la soirée du **samedi**.
- La relève de 17 h implique une remise d'argent entre l'équipe de jour et l'équipe du soir.
- Un soir, la clôture est oubliée : le lendemain à 11 h, l'équipe de jour ouvre sans que la veille soit fermée.
- Le téléphone d'un serveur affiche une heure fausse (réglage, batterie retirée) ou a été reculé d'une heure.
- Une veille de fête, le service continue jusqu'à 6 h du matin.

### 4.2 Risques

| Risque | Opérationnel | Financier |
|---|---|---|
| Ventes de la nuit attribuées au lendemain | Rapports journaliers faux | Écarts fictifs sur deux journées |
| Journée non clôturée qui se prolonge | Mélange de deux journées | Contrôle impossible |
| Relève de jour/soir non tracée | On ne sait pas quelle équipe est responsable d'un manquant | Responsabilité diluée |
| Manipulation de l'heure | Déplacer une vente d'une journée à l'autre pour masquer un écart | Fraude |

**Classement : MAJEUR.**

### 4.3 Options comparées

| Option | Principe | Avantages | Limites | Complexité |
|---|---|---|---|---|
| **J1 — Jour calendaire** | La journée va de 0 h à 24 h | Trivial | Faux pour presque tous les maquis | Très faible |
| **J2 — Heure de bascule fixe** | Paramètre par établissement (ex. 6 h) : avant cette heure, l'opération appartient à la veille | Simple, prévisible, calculable hors ligne | Dépend de l'horloge de l'appareil ; échoue si le service dépasse l'heure de bascule ; ne gère ni l'oubli de clôture ni la relève | Faible |
| **J3 — Journée ouverte et fermée explicitement** | Une personne habilitée **ouvre** la journée ; chaque appareil, en ouverture de service, reçoit l'identifiant de la journée ; chaque opération porte cet identifiant ; la journée se termine à la clôture | Indépendant de l'horloge ; fiable après minuit et à 6 h du matin ; s'appuie sur M13 déjà validé | Oubli de clôture ; appareil qui ouvre son service sans contact avec les autres | Moyenne |

### 4.4 Recommandation pour C3

**J3 comme règle, J2 comme filet de sécurité.**

1. **Journée d'exploitation explicite** : ouverte par une personne habilitée, identifiée par sa date d'ouverture (« journée du samedi 14 »). Chaque opération porte l'identifiant de la journée reçu à l'ouverture de service. L'heure de l'appareil sert à l'affichage et à la détection des dérives, jamais au rattachement.
2. **Services (relèves) à l'intérieur de la journée** : une journée peut contenir plusieurs services (jour, soir). Une relève déclenche une **remise individuelle** (mécanisme K3 déjà validé) entre l'équipe sortante et l'équipe entrante. La **journée** est l'unité de clôture ; le **service** est l'unité de responsabilité de l'argent.
3. **Heure de bascule théorique** (paramètre par établissement) utilisée uniquement pour :
   - rattacher **provisoirement** les opérations d'un appareil qui n'a pas pu recevoir l'identifiant de la journée (opération marquée « hors session », déjà prévu en B1) ;
   - alerter : « journée du samedi toujours ouverte » quand elle dépasse l'heure de bascule d'un délai paramétrable.
4. **Pas de nouvelle journée sur une journée ouverte** : ouvrir une journée alors que la précédente n'est pas au moins en clôture provisoire exige une **clôture forcée** de la précédente, faite par une personne habilitée, justifiée et signalée au propriétaire.
5. **Rapports** : établis par journée d'exploitation ; le détail horaire reste disponible.

### 4.5 Décisions métier nécessaires pour C3

| # | Décision | Proposition par défaut |
|---|---|---|
| M14 | Journée ouverte et fermée explicitement, nommée par sa date d'ouverture | Oui |
| M15 | Plusieurs services par journée, avec remise individuelle à chaque relève | Oui |
| M16 | Heure de bascule théorique par établissement | Paramètre fixé à l'installation (valeur relevée en observation) |
| M17 | Qui peut ouvrir la journée ? | Gérant ou caissier désigné |
| M18 | Clôture forcée d'une journée oubliée : qui, et avec quelle trace ? | Gérant ou propriétaire, justification obligatoire, alerte au propriétaire |
| M19 | Délai avant l'alerte « journée toujours ouverte » | Paramètre ; valeur après le pilote |

### 4.6 Tests C3

| # | Test | Résultat attendu |
|---|---|---|
| T19 | Vente à 0 h 40 dans une journée ouverte la veille | Rattachée à la journée de la veille |
| T20 | Service jusqu'à 6 h 30 (au-delà de l'heure de bascule) | Toujours rattaché à la journée ouverte ; alerte « journée toujours ouverte » après le délai |
| T21 | Appareil dont l'horloge est reculée d'une heure | Rattachement correct par l'identifiant de journée ; dérive signalée |
| T22 | Appareil qui ouvre son service hors contact | Opérations « hors session », rattachées provisoirement par l'heure de bascule, signalées |
| T23 | Ouverture d'une journée alors que la précédente est ouverte | Refusée sans clôture forcée ; clôture forcée journalisée et notifiée |
| T24 | Relève jour/soir | Remise individuelle de l'équipe sortante ; écarts attribués au bon service |

---

## 5. C4 — Cumul des rôles

### 5.1 Scénarios réels

- **A — Le gérant fait tout** : le propriétaire est absent, et le gérant est à la fois caissier, magasinier et responsable de la fermeture. Il prépare et valide la clôture, réceptionne les livraisons, approuve ses propres annulations et ses dépenses.
- **B — La propriétaire est à la caisse** (segment S1) : elle valide elle-même. Le risque de contrôle est faible, puisqu'elle porte elle-même le risque.
- **C — Après minuit, une seule personne reste** : une annulation sensible arrive, il n'y a personne pour l'approuver.
- **D — Codes partagés** : pour « aller plus vite », le gérant donne son code au caissier, qui approuve désormais ses propres opérations sous le nom du gérant.

**Observation importante** : le scénario A correspond exactement aux segments S2 et S3, c'est-à-dire au **cœur de cible**. C4 n'est pas un cas limite ; c'est la situation normale de nombreux clients visés.

### 5.2 Risques

| Risque | Opérationnel | Financier |
|---|---|---|
| Auto-validation présentée comme une validation indépendante | Le propriétaire croit à un contrôle qui n'existe pas | **Fausse assurance** : pire qu'une absence d'outil |
| Blocage des opérations faute d'approbateur | Service ralenti, outil contourné | Abandon de l'outil |
| Partage des codes | Les traces d'audit désignent la mauvaise personne | Fraude non attribuable ; conflits avec le personnel |
| Concentration des pouvoirs chez le gérant | Annulations fictives, dépenses inventées, réceptions sous-déclarées | Pertes directes |

**Classement : MAJEUR** pour le cumul lui-même ; **CRITIQUE** si l'outil présente une auto-validation comme indépendante (atteinte à la fiabilité financière et à la promesse commerciale).

### 5.3 Options comparées

| Option | Principe | Avantages | Limites | Complexité |
|---|---|---|---|---|
| **R1 — Séparation stricte** | Toute opération sensible exige deux personnes différentes, sinon elle est bloquée | Contrôle préventif maximal | Inapplicable dans un petit maquis ; pousse au partage des codes (scénario D) | Faible à concevoir, **contre-productif** à l'usage |
| **R2 — Approbation a posteriori par le propriétaire à distance** | La personne seule exécute ; l'opération est « en attente d'approbation » ; le propriétaire approuve ou rejette depuis son téléphone **quand il est connecté** | Approbation réelle (pas fictive), compatible avec la règle sur les absents ; met le propriétaire dans la boucle | C'est un contrôle **de détection**, pas de prévention : la boisson est déjà annulée ; dépend de la disponibilité du propriétaire | Moyenne |
| **R3 — Contrôles compensatoires** | Quand la séparation est impossible : auto-validation autorisée mais **marquée**, justification obligatoire, pièce jointe (photo du bon de livraison, du reçu), plafonds, alertes, statistiques par personne, comptages surprises, rapprochement stock/argent | Ne bloque pas l'activité ; rend les risques visibles | Ne prévient pas la fraude ; demande au propriétaire de regarder les alertes | Moyenne |

### 5.4 Recommandation pour C4

**Une matrice de contrôle par opération**, qui combine R1, R2 et R3 selon la sensibilité de l'opération et la présence réelle d'une seconde personne habilitée.

**Principe 1 — Trois niveaux de contrôle, toujours affichés**

| Niveau | Signification | Affichage pour le propriétaire |
|---|---|---|
| **Approuvé indépendamment** | Une personne habilitée, différente de l'auteur, a approuvé (sur place ou à distance) | Approuvé par [nom] |
| **Auto-validé** | L'auteur a validé lui-même, faute d'approbateur disponible | **Auto-validé — à revoir**, avec la justification |
| **En attente** | Approbation a posteriori demandée au propriétaire | En attente de votre décision |

Une auto-validation **n'est jamais** présentée comme une approbation indépendante.

**Principe 2 — Matrice proposée**

| Opération | Avec une seconde personne habilitée | En cumul de rôles |
|---|---|---|
| Annulation **avant** remise | Journalisée, sans approbation | Idem |
| Annulation **après** remise (boisson consommée) | Approbation préalable par une autre personne | Auto-validation marquée + justification + **alerte immédiate** au propriétaire ; jamais de retour automatique en stock |
| Boisson offerte, geste commercial | Approbation au-delà d'un seuil | Plafond journalier ; au-delà, en attente du propriétaire |
| Dépense au-dessus du seuil | Approbation préalable | Photo du justificatif obligatoire ; en attente du propriétaire |
| Crédit client | Autorisation, identification du débiteur, échéance | Plafond par client ; au-delà, en attente du propriétaire |
| Réception de livraison | Contrôle par une seconde personne | **Photo du bon de livraison** obligatoire (pièce externe) ; comparaison automatique avec la commande au fournisseur si elle existe |
| Transfert entre emplacements | Départ et réception par deux personnes | Autorisé par la même personne, marqué ; vérifié par les inventaires |
| Écart de transfert ou d'inventaire | Approbation par une autre personne | En attente du propriétaire |
| Inventaire | Comptage et validation par deux personnes | Auto-validé marqué ; **comptages surprises** par le propriétaire recommandés |
| Clôture | Préparation et validation par deux personnes | Clôture « auto-validée » ; validation a posteriori par le propriétaire |
| Déclaration d'un appareil absent | Personne différente du préparateur (validé) | Uniquement par le propriétaire ; sinon la clôture reste provisoire |
| Modification de prix, des rôles, des seuils | Propriétaire (ou gérant délégué pour les prix) | Propriétaire uniquement |

**Principe 3 — Deux dimensions distinctes pour la clôture**
Les 5 statuts validés en B1 décrivent la **complétude** (toutes les opérations sont-elles reçues ?). Le niveau de contrôle décrit la **validation** (qui a validé ?). Ce sont deux informations différentes, affichées côte à côte : par exemple « Consolidée · Auto-validée ». **Les 5 statuts validés ne sont pas modifiés.**

**Principe 4 — Le propriétaire est l'approbateur ultime**
- Un **propriétaire unique** peut valider ses propres opérations (il porte lui-même le risque). L'opération reste marquée « validée par le propriétaire ».
- Avec **plusieurs associés**, chacun approuve les opérations de l'autre ; l'auto-validation d'un associé est marquée.

**Principe 5 — Identité personnelle et charte d'utilisation**
- Un compte et un code **personnels** par personne ; aucun compte partagé.
- Une **charte d'utilisation** signée par chaque employé à l'installation : le code est personnel, son partage est une faute. *Document à rédiger sur autorisation et à faire valider juridiquement (droit du travail).*
- Le partage de codes ne peut pas être empêché techniquement sur des appareils d'entrée de gamme. Il est **découragé** (charte), **rendu coûteux** (chaque approbation exige le code de l'approbateur au moment même) et **surveillé** (statistiques d'approbations par personne). C'est un **risque résiduel accepté**, à expliquer au propriétaire.

**Principe 6 — Honnêteté commerciale**
Dans un établissement où une seule personne fait tout, l'outil **ne remplace pas une deuxième personne** : il rend les opérations **visibles** et **attribuables**, et il appuie le contrôle par le stock. Le discours commercial doit le dire. Promettre plus créerait une déception, donc des résiliations.

### 5.5 Décisions métier nécessaires pour C4

| # | Décision | Proposition par défaut |
|---|---|---|
| M20 | Trois niveaux de contrôle (indépendant / auto-validé / en attente), toujours affichés | Oui |
| M21 | Matrice de contrôle par opération (§5.4) | Oui, seuils et plafonds paramétrables, valeurs par défaut fixées avec les pilotes |
| M22 | Complétude et niveau de contrôle affichés comme deux informations distinctes | Oui |
| M23 | Le propriétaire unique peut valider ses propres opérations ; les associés s'approuvent mutuellement | Oui |
| M24 | Comptes personnels et charte d'utilisation signée par le personnel | Oui (rédaction sur autorisation, validation juridique) |
| M25 | Photo obligatoire du bon de livraison et des justificatifs de dépense en cumul de rôles | Oui, sous réserve de la qualité des appareils (lien Q4) |
| M26 | Discours commercial : « l'outil rend visible, il ne remplace pas une deuxième personne » | Oui, à intégrer au script de démo |

### 5.6 Tests C4

| # | Test | Résultat attendu |
|---|---|---|
| T25 | Une personne prépare puis tente de valider sa propre clôture alors qu'un approbateur est configuré | Refusé |
| T26 | Même situation en cumul déclaré | Clôture « auto-validée », visible comme telle par le propriétaire |
| T27 | Annulation après remise, une seule personne présente, hors ligne | Auto-validation marquée + justification ; alerte transmise au propriétaire dès la synchronisation ; pas de retour en stock |
| T28 | Dépense au-dessus du seuil en cumul | En attente du propriétaire ; impossible à consolider comme approuvée sans sa décision |
| T29 | Approbation par le propriétaire à distance, connecté | Approbation enregistrée avec son identité et l'heure de réception |
| T30 | Tentative d'approbation « à distance » par un propriétaire **hors ligne** | Impossible ; l'opération reste en attente |
| T31 | Réception de livraison sans photo du bon en cumul | Refusée ou marquée incomplète selon la configuration |
| T32 | Tableau de bord du propriétaire | Aucune auto-validation n'apparaît comme approbation indépendante |
| T33 | Fréquence anormale d'annulations ou d'auto-validations par une personne | Signalée au propriétaire |

---

## 6. Limites de cette analyse

- En cumul de rôles, les contrôles sont surtout **détectifs** : ils signalent après coup. Leur efficacité dépend du fait que le propriétaire lise les alertes. La fréquence réelle de lecture sera mesurée au pilote (H10).
- Le partage des codes reste un risque résiduel.
- La photo des justificatifs suppose un appareil avec un appareil photo correct et un éclairage suffisant (à vérifier en observation).
- Le sujet de la facture électronique certifiée peut modifier certaines règles (numérotation, immutabilité, clôture journalière). Les principes de B1–B2 vont dans le même sens (faits non modifiables, journal), ce qui limite le risque de remise en cause.

---

## 7. Décisions à prendre

| # | Question | Recommandation |
|---|---|---|
| **Q20** | Validez-vous la **journée d'exploitation explicite** avec services et relèves, et l'heure de bascule comme filet de sécurité (M14 à M19) ? | Oui |
| **Q21** | Validez-vous la **matrice de contrôle par opération** avec trois niveaux de contrôle toujours affichés (M20 à M23, M25) ? | Oui |
| **Q22** | Validez-vous les **comptes personnels avec charte d'utilisation** et le discours commercial honnête sur le cumul de rôles (M24, M26) ? | Oui |
| **Q23** | Faut-il lancer **maintenant** une vérification fiscale (DGI ou fiscaliste) sur la facture électronique certifiée et son application aux maquis et aux logiciels de caisse ? | Oui, avant la Porte 2 ; budget à prévoir dans la ligne « consultation juridique » de la Phase A ou en Phase B |

---

## 8. Registre des décisions (mise à jour séance B2)

| ID | Élément | Statut |
|---|---|---|
| D-B2-01 | Journée d'exploitation explicite, nommée par sa date d'ouverture (M14) | À ARBITRER (Q20) |
| D-B2-02 | Services et relèves avec remise individuelle (M15) | À ARBITRER (Q20) |
| D-B2-03 | Heure de bascule théorique, filet de sécurité (M16) | À ARBITRER (Q20) · valeur À VÉRIFIER SUR LE TERRAIN |
| D-B2-04 | Ouverture de journée par gérant ou caissier désigné (M17) | PROPOSÉ |
| D-B2-05 | Clôture forcée d'une journée oubliée, justifiée et notifiée (M18) | PROPOSÉ |
| D-B2-06 | Délai d'alerte « journée toujours ouverte » (M19) | PROPOSÉ · valeur après pilote |
| D-B2-07 | Trois niveaux de contrôle toujours affichés (M20) | À ARBITRER (Q21) |
| D-B2-08 | Matrice de contrôle par opération (M21) | À ARBITRER (Q21) · seuils avec les pilotes |
| D-B2-09 | Complétude et niveau de contrôle distincts ; 5 statuts B1 inchangés (M22) | À ARBITRER (Q21) |
| D-B2-10 | Propriétaire unique auto-validant ; associés mutuellement (M23) | À ARBITRER (Q21) |
| D-B2-11 | Comptes personnels + charte d'utilisation (M24) | À ARBITRER (Q22) · rédaction sur autorisation, validation juridique |
| D-B2-12 | Photo des justificatifs en cumul (M25) | À ARBITRER (Q21) · lié à Q4 |
| D-B2-13 | Discours commercial honnête sur le cumul (M26) | À ARBITRER (Q22) · à intégrer au script de démo A3 |
| D-B2-14 | Partage de codes : risque résiduel accepté et surveillé | PROPOSÉ |
| D-B2-15 | Tests T19 à T33 ajoutés au plan de la preuve de faisabilité | PROPOSÉ |
| D-B2-16 | **Facture électronique certifiée (FEC / SECeF) : applicabilité aux maquis et aux logiciels de caisse** | **À VÉRIFIER (Q23) · MAJEUR, potentiellement BLOQUANT pour le périmètre avant la Porte 2** |
| D-B2-17 | Ne pas aborder le sujet fiscal de soi-même pendant les entretiens ; noter les mentions spontanées | PROPOSÉ |
| C3 | Journée d'exploitation après minuit | BLOQUANT jusqu'à réussite des tests T19–T24 |
| C4 | Cumul des rôles | BLOQUANT jusqu'à réussite des tests T25–T33 |

---

## 9. Prochaine étape proposée

**Séance B3 — C5 (paiements Mobile Money) et C6 (inventaires en cours de service).**
- C5 : comment passer de « paiement déclaré » à « paiement vérifié » puis « rapproché », sur quel numéro les fonds arrivent, qui peut vérifier, et comment éviter les fausses déclarations et les doubles rapprochements.
- C6 : comment compter pendant que le service continue, et comment le stock devient le contrôle principal contre les ventes jamais saisies (limite identifiée en B1).

---

## Sources consultées (point juridique §3)

- [Burkina24 — Communiqué : facture électronique certifiée, mise en vente des systèmes de facturation à partir du 7 septembre 2026](https://burkina24.com/2026/09/02/communique-facture-electronique-certifiee-la-mise-en-vente-des-systemes-de-facturation-demarre-le-7-septembre-2026-au-burkina-faso-2/)
- [Le360 Afrique — La facture normalisée étendue au réel simplifié et aux micro-entreprises (2022)](https://afrique.le360.ma/autres-pays/economie/2022/04/03/37531-burkina-faso-la-facture-normalisee-etendue-aux-contribuables-du-regime-reel-simplifie-et-aux)
- [DGI Burkina Faso — Fisc Infos, premier trimestre 2022](https://dgi.bf/wp-content/uploads/2023/10/FISC-INFOS-DU-PREMIER-TRIMESTRE-2022.pdf)
- [Lookuptax — FEC / SECeF e-invoicing Burkina Faso](https://lookuptax.com/docs/einvoicing/fec-secef-einvoicing-burkina-faso)
- [Benin Web TV — Entrée en vigueur de la facturation électronique au Burkina Faso](https://beninwebtv.bj/entree-en-vigueur-de-la-facturation-electronique-au-burkina-faso-en-juillet-2026/)

Ces sources sont des articles de presse et des synthèses ; elles ne remplacent pas les textes officiels (Code général des impôts, lois de finances, communiqués de la DGI).
