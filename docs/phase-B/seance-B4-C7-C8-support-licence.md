# MAQUIS CONTROL — Séance B4
## Phase B · Contradictions C7 (rentabilité du support) et C8 (abonnement expiré hors ligne) · Préparation de la Porte 2

> **Statut** : compte rendu de séance de brainstorming. Ni business plan, ni prévisions financières, ni code.
> **Règle chiffrée** : aucun coût réel n'est connu à ce stade. Les tableaux distinguent les **décisions validées** (prix), les **calculs arithmétiques** (volumes) et les **hypothèses de simulation** explicitement marquées. Aucune hypothèse n'est une prévision.

---

## 1. Objectif de la séance

1. Résoudre C7 et C8 selon la méthode habituelle.
2. Clôturer la revue des huit contradictions.
3. Proposer les critères de la Porte 2.

## 2. Décisions validées qui encadrent C7 et C8

| Décision validée | Lien |
|---|---|
| Installation assistée 25 000 FCFA ; abonnement 10 000 FCFA/mois, d'avance, Mobile Money | Revenus disponibles pour couvrir le support |
| Support à distance en priorité | Cadre de C7 |
| Période de grâce de 7 jours | Cadre de C8 |
| Administrateurs SaaS sans accès par défaut aux données financières détaillées | **Tension avec l'assistance à distance** (C7) |
| Fonctionnement hors ligne ; aucune perte d'opération | Cadre de C8 |
| Partenariats commerciaux après 10 clients payants | Limite la délégation du support aux partenaires |
| B1 à B3 : plusieurs appareils, anomalies visibles, rapprochements Mobile Money, inventaires, prix d'achat au catalogue | **Augmentent le besoin d'accompagnement** (C7) |
| **Validation de la séance B3** : Q24 à Q27, M27 à M42 | VALIDÉ ; M34 REPORTÉ ; M43 à vérifier |

---

## 3. C7 — Rentabilité de l'installation et du support

### 3.1 Scénario réel

Un snack avec un gérant, un caissier et trois serveurs encaisseurs souscrit.

- **Installation** : saisie d'environ une centaine de produits avec prix de vente et prix d'achat, conditionnements (casiers), emplacements, numéros Mobile Money officiels, comptes personnels et chartes pour 5 personnes, 4 appareils à configurer, formation à la commande, à l'encaissement, à la remise individuelle, à la clôture, à l'inventaire à l'aveugle.
- **Premier mois** : le gérant appelle pour un « stock négatif », un « trop-perçu », une clôture restée « provisoire », un code oublié.
- **Troisième mois** : deux serveurs sont remplacés. Les nouveaux ne sont pas formés. Le gérant appelle un samedi à 1 h 30 : « la clôture ne marche pas ».
- **Sixième mois** : les prix de la brasserie augmentent ; il faut mettre à jour tout le catalogue.

### 3.2 Risques

| Risque | Opérationnel | Financier |
|---|---|---|
| Installation plus longue que ce que couvrent 25 000 FCFA | Retard des installations suivantes | Perte sur chaque nouveau client |
| Support récurrent supérieur à la marge de l'abonnement | Fondateur saturé, délais de réponse | Clients **non rentables** ; croissance qui creuse les pertes |
| Rotation du personnel des maquis | Formation à refaire en permanence | Coût caché récurrent |
| Appels de nuit | Support impossible à tenir | Abandon de l'outil si le client reste bloqué |
| Support insuffisant | Mauvaise utilisation, données fausses | Résiliation (churn) |
| Assistance qui exige de voir les données du client | Conflit avec la règle de confidentialité | Risque de confiance et juridique |

**Classement : MAJEUR** (viabilité économique). Il peut devenir **bloquant pour la Porte 6** (passage à l'échelle) si le temps de support mesuré au pilote dépasse le plafond fixé.

### 3.3 Ce que l'on peut calculer sans inventer de coûts

**a) Volume de support selon le nombre de clients (calcul arithmétique)**

Heures de support par mois = nombre de clients × minutes par client et par mois ÷ 60.

| Minutes de support par client et par mois | 10 clients | 30 clients | 50 clients |
|---|---|---|---|
| 30 min | 5 h | 15 h | 25 h |
| 60 min | 10 h | 30 h | 50 h |
| 120 min | 20 h | 60 h | 100 h |
| 240 min | 40 h | 120 h | 200 h |

*Hypothèse de lecture : une personne consacre environ 120 heures productives par mois au support.* À 240 minutes par client, 50 clients exigent plus d'une personne à plein temps ; à 60 minutes, une demi-journée par jour suffit. **Le temps de support par client est la variable qui décide si le modèle passe à l'échelle.**

**b) Temps de support que l'abonnement peut financer (formule)**

Minutes finançables par client et par mois = (10 000 × part de l'abonnement allouée au support) ÷ coût horaire du support × 60.

| Coût horaire chargé du support *(hypothèse de simulation, non observée)* | Si 30 % de l'abonnement va au support (3 000 FCFA) | Si 20 % (2 000 FCFA) |
|---|---|---|
| 1 000 FCFA/h | 180 min | 120 min |
| 2 000 FCFA/h | 90 min | 60 min |
| 4 000 FCFA/h | 45 min | 30 min |

Ces valeurs illustrent la sensibilité ; elles ne sont pas des données. La part allouée au support (20 %, 30 %…) est une **décision de modèle économique** à prendre en Phase D, après avoir connu l'hébergement, les commissions et les autres charges.

**c) Seuil de rentabilité de l'installation (formule)**

Installation rentable si : 25 000 ≥ (heures d'installation et de suivi initial × coût horaire) + transport + consommables.

L'installation comprend aussi les **suivis des premiers jours** (appels à J+2, J+7). Ils doivent être comptés dans ce calcul, pas dans le support mensuel.

### 3.4 Options comparées

| Option | Principe | Avantages | Limites | Complexité |
|---|---|---|---|---|
| **S1 — Support humain illimité inclus** | Tout est compris dans l'abonnement, à toute heure | Attractif commercialement | Coût non maîtrisé ; insoutenable à 30–50 clients si le temps par client est élevé | Faible à décider, **risque élevé** |
| **S2 — Offre de support encadrée** | Inclus : assistance à distance aux heures ouvrées, accompagnement renforcé le premier mois (couvert par l'installation), formation d'un nombre défini de nouveaux employés par an. **Payant** : visite sur site, formations au-delà du quota, reprise complète du catalogue | Coût prévisible ; aligne le prix sur l'effort | **Modifie l'offre validée** (ajout de services payants) ; à tester commercialement | Moyenne |
| **S3 — Référent formé dans chaque établissement** | Un référent (gérant ou caissier) formé plus longuement assure le premier niveau : formation des nouveaux serveurs, réponses courantes | Réduit les appels ; répond à la rotation du personnel | Dépend de la stabilité du référent | Faible |
| **S4 — Support intégré au produit** | Chaque anomalie s'explique d'elle-même et propose une action ; guides en images et courtes vidéos en français et langues nationales ; **aucune situation de fermeture ne nécessite un appel** ; diagnostic technique à distance sans données financières | Réduit durablement le volume ; seule option qui passe à l'échelle | Coût de conception initial ; exige des tests d'usage | Moyenne à élevée à la conception, **faible** à l'exploitation |

### 3.5 Recommandation pour C7

**S4 + S3 comme fondations, S2 comme cadre de l'offre (à arbitrer), S1 exclu.**

**Principe 1 — Le produit ne doit jamais bloquer la nuit**
Les décisions B1–B3 vont déjà dans ce sens : le stock négatif ne bloque pas la vente, la clôture provisoire permet de partir, les anomalies sont traitées plus tard. Règle de conception : **toute anomalie survenant pendant le service ou la fermeture peut être reportée au lendemain sans perte**. Le support n'est donc jamais nécessaire la nuit.

**Principe 2 — Installation standardisée**
| Étape | Contenu | Objectif |
|---|---|---|
| Avant la visite (à distance) | Photo de la liste de prix et de produits ; saisie préparée à l'avance ; **modèles de catalogue** des boissons courantes, préparés une fois pour tous | Réduire le temps sur site |
| Visite d'installation | Appareils, comptes, chartes, numéros officiels ; formation par rôle (courte, pratique) ; formation renforcée du référent | Une visite, durée cible à mesurer |
| J+2 et J+7 | Appels de suivi | Corriger tôt les mauvaises habitudes |
| J+30 | Bilan (identique au bilan pilote) | Mesurer l'usage |
| Regroupement géographique | Installer par zones | Réduire les déplacements |

**Principe 3 — Référent obligatoire**
Déjà exigé pour les pilotes (engagement P2). Proposition : l'étendre aux clients payants. Le référent forme les nouveaux employés avec les guides intégrés.

**Principe 4 — Assistance à distance respectueuse des données**
La règle « pas d'accès par défaut aux données financières détaillées » est maintenue. Pour les cas où l'assistance a besoin de voir les données :
- **Accès d'assistance accordé par le propriétaire**, depuis son application ;
- **limité** (périmètre défini), **temporaire** (expiration automatique), **journalisé**, **visible** par le propriétaire ;
- le diagnostic technique courant (état de synchronisation, versions, erreurs) se fait **sans** données financières.

**Principe 5 — Mesurer dès le pilote**
Chaque contact de support est consigné : date, canal, durée, catégorie (formation, anomalie, appareil, réseau, paiement de l'abonnement, demande de fonctionnalité), résolu ou non. Le temps par client et par mois devient un **critère des Portes 5 et 6**.

### 3.6 Décisions métier nécessaires pour C7

| # | Décision | Proposition par défaut |
|---|---|---|
| M44 | Aucune situation de service ou de fermeture ne nécessite le support | Oui (règle de conception) |
| M45 | Horaires de l'assistance incluse | Heures ouvrées, plages à fixer ; pas d'assistance de nuit |
| M46 | Canaux | Téléphone et messagerie (WhatsApp) ; à confirmer avec les usages observés |
| M47 | Offre encadrée : services inclus / services payants (visite sur site, formations au-delà d'un quota, reprise du catalogue) | **À ARBITRER (Q28)** : modifie l'offre validée |
| M48 | Référent obligatoire pour tous les clients | Oui |
| M49 | Installation standardisée en 4 temps, modèles de catalogue, regroupement géographique | Oui |
| M50 | Accès d'assistance accordé par le propriétaire, limité, temporaire, journalisé, visible | Oui |
| M51 | Journal de support et plafond de temps par client comme critère des Portes 5 et 6 | Oui ; valeur du plafond fixée en Phase D |
| M52 | Part de l'abonnement allouée au support | À décider en Phase D (simulation §3.3) |

### 3.7 Mesures à réaliser (pilote et Phase A)

| # | Mesure | Où | Utilité |
|---|---|---|---|
| T53 | Durée réelle de l'installation par étape | Pilotes | Seuil de rentabilité de l'installation |
| T54 | Minutes de support par client et par mois, par catégorie | Pilotes | Variable clé du passage à l'échelle |
| T55 | Part des questions résolues par le référent ou les guides | Pilotes | Efficacité de S3 et S4 |
| T56 | Nombre d'incidents de nuit ayant exigé un appel | Pilotes | Doit être nul (M44) |
| T57 | Rotation du personnel (départs et arrivées en 30 jours) | Pilotes ; **question à relever en Phase A** si mentionnée | Coût récurrent de formation |
| T58 | Durée d'une mise à jour de catalogue (changement de prix fournisseur) | Pilotes | Charge récurrente |
| T59 | Un accès d'assistance expire et apparaît dans le journal du propriétaire | Preuve de faisabilité | Conformité à la règle de confidentialité |

---

## 4. C8 — Abonnement expiré et appareils hors ligne

### 4.1 Scénario réel

- Le propriétaire oublie de payer son abonnement le 1er du mois. Il est en voyage ; le gérant ne sait pas qu'il faut payer.
- Le maquis n'a pas eu internet pendant 10 jours (coupures, forfait épuisé) : les appareils ne savent pas si l'abonnement est payé.
- Un serveur découvre qu'en reculant la date du téléphone, l'application « croit » que l'abonnement est encore valable.
- La suspension tombe un samedi à 22 h, en pleine pointe.
- Le client a payé à temps, mais ses appareils, hors ligne depuis 9 jours, ne l'ont pas appris.
- Après 4 mois sans paiement, le client demande ses données pour changer d'outil.

### 4.2 Risques

| Risque | Opérationnel | Financier / juridique |
|---|---|---|
| Suspension en plein service | Service désorganisé, colère du client | Résiliation, mauvaise réputation |
| Suspension d'un client qui a payé | Faute grave de MAQUIS CONTROL | Perte de confiance |
| Perte ou blocage des données | Violation d'une règle non négociable | Risque juridique et commercial |
| Contournement par l'horloge | Usage gratuit prolongé | Perte de revenus |
| Aucune conséquence au non-paiement | Retards de paiement généralisés | Trésorerie dégradée |

**Classement : MAJEUR.** Il deviendrait **CRITIQUE** en cas de perte de données (interdit).

### 4.3 Options comparées

| Option | Principe | Avantages | Limites | Complexité |
|---|---|---|---|---|
| **L1 — Vérification en ligne à chaque démarrage** | L'application vérifie l'abonnement sur le serveur | Simple, difficile à contourner | **Incompatible avec le fonctionnement hors ligne** : suspend des clients qui ont payé | Faible, **rejetée** |
| **L2 — Licence locale signée à durée limitée** | Chaque appareil détient une licence signée valable jusqu'à la fin de la période payée + 7 jours de grâce ; renouvelée à chaque synchronisation | Fonctionne hors ligne ; contournement limité | L'horloge de l'appareil reste manipulable ; un client payé mais hors ligne longtemps peut être suspendu à tort | Moyenne |
| **L3 — Licence locale + code de réactivation hors ligne + suspension progressive** | L2, plus : un **code court signé** envoyé par SMS au propriétaire après paiement, saisi sur un appareil sans internet ; suspension par paliers, jamais en plein service ; accès aux données toujours préservé | Couvre les clients payés hors ligne ; suspension prévisible ; respect des données | Plus de règles à concevoir et à tester ; faisabilité du code court à démontrer | Moyenne à élevée |

### 4.4 Recommandation pour C8

**L3.**

**Calendrier de suspension progressive**

| Moment | État | Ce qui fonctionne | Communication |
|---|---|---|---|
| J−5, J−1, J0 | Actif | Tout | Rappels au propriétaire (application, SMS) |
| J1 à J7 | **Grâce** | Tout | Bandeau visible ; rappel quotidien au propriétaire et au gérant |
| Après J7 | **Suspendu, en fin de journée d'exploitation** | La journée en cours se termine normalement, jusqu'à sa clôture. Ensuite : **consultation et export des données** toujours possibles ; plus de nouvelle journée d'exploitation ; tableau de bord à distance suspendu | Message clair : comment payer, comment réactiver |
| Paiement reçu | **Réactivé** | Tout, immédiatement (en ligne) ou par code de réactivation (hors ligne) | Confirmation |
| Suspension prolongée | Données conservées pendant une durée fixée | Export toujours possible | Préavis avant toute suppression, à durée fixée contractuellement |

**Règles**
1. **Jamais de suspension en plein service** : la suspension prend effet à la clôture de la journée d'exploitation en cours (C3 validé).
2. **Jamais de perte de données** : les opérations déjà enregistrées sont conservées et synchronisables, même pendant la suspension.
3. **Accès du client à ses données toujours possible** (consultation et export), quelle que soit la situation de paiement.
4. **Licence propagée entre appareils** : un appareil qui a reçu la licence renouvelée la transmet aux autres lors des échanges locaux (remise individuelle, ouverture de service), sans attendre internet.
5. **Horloge** : la licence est contrôlée contre la plus récente des dates connues (date de l'appareil, dernière date reçue du serveur, date de la dernière opération). Le contournement n'est pas impossible, mais il est **détecté à la synchronisation**. Risque résiduel accepté.
6. **Pilote** : licence pilote de 30 jours ; à J+30, la décision écrite du bilan (P2) déclenche soit l'abonnement, soit la fin du pilote, avec export des données.

**Lien avec la structure juridique (Q8)** : encaisser les abonnements suppose une entité capable de recevoir les paiements et d'émettre des reçus. Q8 devient **bloquante avant le lancement commercial** (Phase G), et non seulement pour l'acompte.

### 4.5 Décisions métier nécessaires pour C8

| # | Décision | Proposition par défaut |
|---|---|---|
| M53 | Licence locale signée, valable jusqu'à fin de période + 7 jours | Oui |
| M54 | Suspension progressive, effective à la clôture de la journée en cours | Oui |
| M55 | Contenu du mode suspendu : consultation et export possibles ; pas de nouvelle journée ; tableau de bord à distance suspendu | Oui |
| M56 | Code de réactivation hors ligne envoyé au propriétaire | Oui, sous réserve de faisabilité (Phase C) |
| M57 | Durée de conservation des données après suspension, et préavis avant suppression | À fixer contractuellement, validation juridique |
| M58 | Rappels avant échéance et pendant la grâce, au propriétaire et au gérant | Oui |
| M59 | Contournement par l'horloge : détecté à la synchronisation, risque résiduel accepté | Oui |

### 4.6 Tests C8

| # | Test | Résultat attendu |
|---|---|---|
| T60 | Appareil hors ligne pendant toute la période payée + grâce, abonnement payé | Réactivé par le code hors ligne ; aucune interruption si le code est saisi pendant la grâce |
| T61 | Échéance atteinte pendant un service | Le service et la clôture se terminent normalement ; suspension ensuite |
| T62 | Mode suspendu | Consultation et export fonctionnent ; aucune donnée perdue |
| T63 | Horloge reculée pour prolonger la licence | Détecté à la synchronisation ; alerte |
| T64 | Paiement reçu en ligne | Réactivation immédiate de tous les appareils ; propagation locale aux appareils hors ligne |
| T65 | Opérations enregistrées pendant la journée de grâce puis suspension | Toutes synchronisées après réactivation, sans doublon |
| T66 | Fin de pilote sans souscription | Export remis au client ; données traitées selon l'engagement P2 |

---

## 5. Bilan des huit contradictions

| Contradiction | Classement | Principe retenu | Statut | Condition de levée |
|---|---|---|---|---|
| C1 Plusieurs appareils hors ligne | Critique | Faits non modifiables, une commande par appareil, caisses individuelles, deux modes | VALIDÉ (B1) | Tests T1–T11 |
| C2 Clôture et opérations non synchronisées | Critique | Remise individuelle, clôture en deux temps, 5 statuts | VALIDÉ (B1) | Tests T12–T18 |
| C3 Journée après minuit | Majeur | Journée explicite, services, heure de bascule en filet | VALIDÉ (B2) | Tests T19–T24 |
| C4 Cumul des rôles | Majeur / critique si mal affiché | Matrice de contrôle, trois niveaux toujours affichés | VALIDÉ (B2) | Tests T25–T33 |
| C5 Mobile Money | Critique | Vérification du côté du récepteur, rapprochement quotidien | VALIDÉ (B3) | Tests T34–T42 |
| C6 Inventaires en service | Majeur | Hors service, tournant, ciblé ; comptage à l'aveugle | VALIDÉ (B3) | Tests T43–T52 |
| C7 Rentabilité du support | Majeur | Produit qui ne bloque jamais la nuit, référent, installation standardisée, mesure | **À ARBITRER (B4)** | Mesures T53–T58 au pilote ; T59 en Phase C |
| C8 Abonnement expiré hors ligne | Majeur | Licence locale signée, code de réactivation, suspension progressive | **À ARBITRER (B4)** | Tests T60–T66 |

**Points transversaux encore ouverts**

| Point | Statut | Bloquant pour |
|---|---|---|
| Facture électronique certifiée (FEC/SECeF) | Vérification lancée, non concluante | **Porte 2** (périmètre) |
| Cadre légal des données personnelles | À vérifier | Premier entretien (Phase A) |
| Politique d'équipement (Q4) | À arbitrer après les démos | Phase D (coûts), pilote |
| Entité juridique (Q8) | À vérifier | Confirmation des pilotes (acompte) ; lancement commercial (abonnements) |
| Emballages consignés (H18, M43) | À vérifier sur le terrain | Périmètre du Module 4 |
| Caisse individuelle et remise obligatoire (M2, M9) | À vérifier sur le terrain | Validation définitive de C1–C2 |

---

## 6. Proposition de critères pour la Porte 2

La Porte 2 (résolution des contradictions métier) **ne peut être tenue qu'après la Porte 1** : la Phase B a avancé en parallèle, mais elle doit être confrontée aux faits du terrain.

| Décision | Critères proposés |
|---|---|
| **Go** | Les 8 contradictions ont des règles validées et des tests définis **et** aucune règle retenue ne viole une règle non négociable **et** les observations de la Phase A ne contredisent pas les hypothèses de fonctionnement (caisse individuelle, remise, saisie possible au moins à certaines conditions) **et** la question FEC a reçu une réponse d'une source officielle ou d'un fiscaliste **et** le cadre légal des données est clarifié |
| **Rework** | Une ou plusieurs règles contredites par le terrain (par exemple, remise individuelle impraticable) → révision ciblée de la contradiction concernée ; **ou** obligation FEC applicable aux clients cibles → révision du périmètre et du calendrier |
| **No-Go** | Une contradiction critique (C1, C2, C5) sans solution compatible avec les règles non négociables **ou** obligation réglementaire rendant le produit irréalisable dans le budget et le tarif cibles |

---

## 7. Limites

- Le modèle de support repose sur une mesure qui n'existe pas encore : les minutes par client et par mois. Les tableaux du §3.3 montrent la sensibilité, pas le résultat.
- L'offre encadrée (S2) modifie l'offre commerciale validée ; elle doit être testée auprès des clients avant d'être adoptée.
- Le code de réactivation hors ligne est un principe ; sa sécurité et son ergonomie sont à démontrer en Phase C.

---

## 8. Décisions à prendre

| # | Question | Recommandation |
|---|---|---|
| **Q28** | Offre de support encadrée (S2) : acceptez-vous d'introduire des **services payants** (visite sur site, formations au-delà d'un quota, reprise du catalogue) à côté de l'assistance incluse ? *Proposition de modification de l'offre validée.* | Oui en principe, **à tester** dans les démos et au pilote avant adoption définitive |
| **Q29** | Validez-vous les fondations du support (M44, M45, M46, M48 à M51) : produit qui ne bloque jamais la nuit, assistance aux heures ouvrées, référent obligatoire, installation standardisée, accès d'assistance accordé par le propriétaire, mesure du temps de support ? | Oui |
| **Q30** | Validez-vous le dispositif de licence (M53 à M56, M58, M59) : licence locale signée, suspension progressive à la fin de la journée en cours, consultation et export toujours possibles, code de réactivation hors ligne ? | Oui |
| **Q31** | Validez-vous les critères proposés pour la Porte 2 (§6) ? | Oui, à figer avant la synthèse de la Phase A |

---

## 9. Registre des décisions (mise à jour séance B4)

| ID | Élément | Statut |
|---|---|---|
| D-B3-01 à D-B3-07, D-B3-09 à D-B3-13, D-B3-15, D-B3-16 | Décisions de la séance B3 | **VALIDÉ** |
| D-B3-08 | Intégration opérateur Mobile Money | REPORTÉ (Phase C/D) |
| D-B3-14 | Emballages consignés | À VÉRIFIER SUR LE TERRAIN |
| D-B4-01 | Aucune situation de service ou de fermeture ne nécessite le support (M44) | À ARBITRER (Q29) |
| D-B4-02 | Assistance aux heures ouvrées, pas de nuit (M45) ; canaux téléphone et messagerie (M46) | À ARBITRER (Q29) |
| D-B4-03 | Offre encadrée avec services payants (M47) | À ARBITRER (Q28) · modification de l'offre |
| D-B4-04 | Référent obligatoire pour tous les clients (M48) | À ARBITRER (Q29) |
| D-B4-05 | Installation standardisée en 4 temps, modèles de catalogue, regroupement géographique (M49) | À ARBITRER (Q29) |
| D-B4-06 | Accès d'assistance accordé par le propriétaire, limité, temporaire, journalisé (M50) | À ARBITRER (Q29) |
| D-B4-07 | Journal de support ; plafond de temps par client critère des Portes 5 et 6 (M51) | À ARBITRER (Q29) · valeur en Phase D |
| D-B4-08 | Part de l'abonnement allouée au support (M52) | REPORTÉ (Phase D) |
| D-B4-09 | Licence locale signée + 7 jours de grâce (M53) | À ARBITRER (Q30) |
| D-B4-10 | Suspension progressive à la clôture de la journée en cours (M54) | À ARBITRER (Q30) |
| D-B4-11 | Mode suspendu : consultation et export toujours possibles (M55) | À ARBITRER (Q30) |
| D-B4-12 | Code de réactivation hors ligne (M56) | À ARBITRER (Q30) · faisabilité Phase C |
| D-B4-13 | Conservation des données après suspension et préavis de suppression (M57) | À ARBITRER · validation juridique |
| D-B4-14 | Rappels avant échéance et pendant la grâce (M58) | À ARBITRER (Q30) |
| D-B4-15 | Contournement par l'horloge : risque résiduel détecté (M59) | À ARBITRER (Q30) |
| D-B4-16 | Mesures T53 à T58 (pilote) et tests T59 à T66 (Phase C) | PROPOSÉ |
| D-B4-17 | Rotation du personnel à relever en Phase A si mentionnée | PROPOSÉ |
| D-B4-18 | Entité juridique (Q8) bloquante avant le lancement commercial | PROPOSÉ (découle de C8) |
| D-B4-19 | Critères de la Porte 2 (§6) | À ARBITRER (Q31) |
| C7 | Rentabilité du support | À ARBITRER · mesures au pilote |
| C8 | Abonnement expiré hors ligne | À ARBITRER · BLOQUANT jusqu'à réussite des tests T60–T66 |

---

## 10. Prochaine étape proposée

La revue des huit contradictions est terminée. Trois suites possibles :

| Option | Contenu | Quand |
|---|---|---|
| **C0 — Cadrage de la preuve de faisabilité (Phase C)** | Regrouper les 66 tests en un protocole ; comparer les architectures possibles (application web/PWA, Android native, appareil pivot local, backend cloud) au regard des règles B1–B4 ; estimer l'effort | Analyse documentaire possible dès maintenant ; **exécution** seulement après les Portes 1 et 2 |
| **D0 — Structure du modèle financier (Phase D)** | Postes de coûts, variables clés (temps de support, équipement, hébergement, commissions), scénarios prudent / central / défavorable, sans chiffres inventés | Utile pour savoir quelles données collecter au pilote |
| **A5 — Point d'étape de la Phase A** | Revue des 10 premières fiches réelles | Dès que le terrain a commencé |

**Recommandation** : **C0**. Les règles validées en B1–B4 sont maintenant assez précises pour comparer les architectures. Cette comparaison conditionne le budget de développement, donc le modèle financier (D0), qui en dépend.

**Rappel** : le terrain de la Phase A n'a pas encore démarré. Ses deux bloquants (Q3 et le cadre légal des entretiens) restent ouverts, et c'est le chemin critique du projet.
