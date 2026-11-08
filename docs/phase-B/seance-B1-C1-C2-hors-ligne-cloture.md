# MAQUIS CONTROL — Séance B1
## Phase B · Contradictions C1 (plusieurs appareils hors ligne) et C2 (clôture avec opérations non synchronisées)

> **Statut** : compte rendu de séance de brainstorming (analyse métier et principes de conception). Ce n'est ni l'architecture logicielle, ni le cahier des charges, ni du code.
> Les solutions sont décrites **indépendamment de toute technologie**. Le choix technique relève de la preuve de faisabilité (Phase C).
> **Chevauchement de phases** : cette séance se tient pendant la Phase A. Elle est justifiée car elle ne coûte que du temps d'analyse, et elle ne contourne pas la Porte 1 : aucune décision d'investissement n'en découle.

---

## 1. Objectif de la séance

Pour C1 et C2 : scénario réel, risques, options comparées, recommandation, décisions métier nécessaires, tests de vérification, classement du risque.

## 2. Décisions et règles déjà validées qui encadrent C1 et C2

| Règle / décision | Conséquence pour C1–C2 |
|---|---|
| Déstockage à la **remise physique confirmée**, pas à la commande | Les événements de remise sont les faits de référence pour le stock |
| Ventes, encaissements et bénéfices sont distincts | Une commande, un paiement et un mouvement de stock sont des objets séparés |
| Les serveurs peuvent encaisser **sans double comptabilisation** | Il faut savoir qui détient physiquement l'argent |
| Paiement **déclaré / vérifié / rapproché** | Un paiement saisi hors ligne est au mieux « déclaré » |
| Opérations sensibles journalisées (auteur, date, justification, approbateur) | Journal obligatoire, donc support naturel de la synchronisation |
| Pas d'auto-approbation lorsque la séparation des tâches est requise | S'applique aussi aux décisions de clôture |
| Approbation hors ligne seulement par une personne **présente et habilitée** | Pas d'approbation « à distance » sans connexion |
| **Une opération non synchronisée ne doit pas être présentée comme consolidée** | Principe central de C2 |
| Aucune perte d'opération enregistrée localement | Une opération ne quitte un appareil qu'après accusé de réception définitif |
| Identifiants uniques et idempotence | Base technique de la détection des doublons |
| Clôture compatible avec le travail après minuit | Lien direct avec C3 (traité en B2) |
| Règle de la séance A4 (Q15 validée) | Règle d'arrêt anticipé et 6 observations : **VALIDÉES** |

**Rappel explicite** : ni un routeur Wi-Fi, ni un réseau local, ni une synchronisation différée ne garantissent à eux seuls la cohérence entre appareils. Un routeur s'éteint pendant un délestage, un téléphone sort de portée, une batterie lâche. La cohérence doit venir des **règles métier et du modèle de données**, le réseau ne faisant qu'accélérer la circulation de l'information.

---

## 3. Analyse transversale : tout n'a pas le même type de conflit

La plupart des « conflits » de synchronisation disparaissent si l'on distingue trois familles de données.

| Famille | Exemples | Nature | Stratégie |
|---|---|---|---|
| **F1 — Faits** | Remise d'une boisson, paiement reçu, dépense, mouvement de stock, comptage | Quelque chose **s'est produit** dans le monde réel | **Ajout seulement** : jamais modifiés, jamais écrasés. Une erreur se corrige par un nouveau fait (contre-passation) journalisé. Deux faits saisis sur deux appareils ne se contredisent pas techniquement : ils s'additionnent. Les incohérences deviennent des **anomalies métier** à traiter (doublon, trop-perçu, stock négatif) |
| **F2 — États partagés modifiables** | Contenu d'une commande ouverte, table affectée, statut d'une commande | Plusieurs personnes peuvent vouloir le changer en même temps | **Propriété unique** : un seul appareil/utilisateur en est responsable à un instant donné. Les autres ne modifient pas hors connexion |
| **F3 — Référentiels** | Catalogue, prix, rôles, seuils, emplacements | Changent rarement, par une personne habilitée | **Versionnés** : chaque vente enregistre le prix et la version utilisés. Un appareil hors ligne travaille sur la dernière version reçue ; l'écart est signalé, jamais corrigé rétroactivement en silence |

**Ce qui est exclu** : la règle « la dernière modification gagne » pour toute donnée financière. Elle efface silencieusement une saisie, ce qui viole les règles de conservation et de traçabilité.

### 3.1 Deux faiblesses à traiter dès la conception

| Faiblesse | Scénario | Principe de réponse |
|---|---|---|
| **L'heure des téléphones n'est pas fiable** | Un téléphone mal réglé, ou volontairement reculé d'une heure, change l'ordre apparent des opérations et la journée de rattachement | Ne jamais ordonner ni rattacher sur la seule heure de l'appareil : **numéro de séquence par appareil**, heure de réception par le système, et détection des dérives d'horloge |
| **Une opération peut disparaître avant synchronisation** | Un serveur efface les données de l'application, ou la désinstalle, avant que ses ventes ne soient transmises | Chaque appareil numérote ses opérations sans trou (1, 2, 3…). **Un trou dans la séquence est détecté** et devient une alerte pour le propriétaire. On ne peut pas empêcher l'effacement, mais on peut le rendre visible |

---

## 4. C1 — Plusieurs appareils hors ligne

### 4.1 Scénario réel

Samedi, 22 h 40, maquis avec un caissier (tablette au comptoir) et deux serveurs (téléphones). Délestage : le routeur s'éteint, le réseau mobile est saturé.

1. Le serveur A a ouvert la commande de la table 5 : 4 bières.
2. Le client de la table 5 appelle le serveur B, qui ajoute 2 bières sur **son** téléphone et confirme leur remise.
3. Au moment de partir, un client paie 6 000 FCFA en espèces au serveur A ; son ami paie la même addition par Orange Money au caissier, en montrant un SMS.
4. Il ne reste que 3 bouteilles d'une marque dans le frigo du bar. Les deux serveurs confirment chacun la remise de 2 bouteilles.
5. Le gérant, sur la tablette, annule une bière de la table 5 « jamais servie », alors que le serveur B l'a déjà remise.

Au retour du réseau, les quatre appareils synchronisent.

### 4.2 Risques

| Risque | Opérationnel | Financier |
|---|---|---|
| Commande modifiée à deux endroits | Addition fausse, dispute avec le client | Vente sous-estimée ou surestimée |
| Double paiement de la même addition | Le client a payé deux fois, ou l'un des paiements est fictif | Encaissements surestimés, écart de caisse faux |
| Stock négatif | Inventaire faux | Perte masquée ou fausse alerte de vol |
| Annulation après remise | Boisson consommée réintégrée au stock | **Fraude classique** : on annule une vente servie et on garde l'argent |
| Fusion silencieuse | Le propriétaire voit des chiffres « propres » mais faux | Perte de confiance, donc résiliation |

**Classement : CRITIQUE** (cohérence financière et conservation des transactions).

### 4.3 Options comparées

| Option | Principe | Avantages | Limites | Coût / complexité |
|---|---|---|---|---|
| **O1 — Appareils autonomes, fusion par le serveur central à la reconnexion** | Chaque appareil travaille seul ; tout se fusionne dans le cloud au retour du réseau | Pas d'équipement supplémentaire ; simple à déployer | Divergence pendant des heures ; conflits découverts **après le départ des clients** ; aucune visibilité croisée pendant la coupure | Moyenne à la conception, **élevée** à l'exploitation (beaucoup d'anomalies à traiter après coup) |
| **O2 — Appareil pivot local** | Un appareil désigné (la tablette de caisse) fait autorité dans l'établissement ; les autres se synchronisent avec lui par un réseau local quand il existe ; le pivot se synchronise avec le cloud | Cohérence quasi immédiate **tant que le réseau local fonctionne** ; visibilité croisée en salle | Le réseau local tombe aussi (délestage) ; le pivot devient un point unique de panne et de vol ; ce qui n'existe que sur le pivot peut être perdu ; plus de support | Élevée : deux niveaux de synchronisation, configuration sur site, assistance accrue |
| **O3 — Poste unique d'encaissement** | Seul un appareil enregistre les opérations financières ; les serveurs ne font que prendre des commandes, ou utilisent le papier | Aucun conflit financier possible ; le plus simple | Contredit le profil pilote 2 (serveurs encaisseurs) ; goulot d'étranglement à la caisse en pointe | Faible |
| **O4 — Faits en ajout seul + propriété unique + caisses individuelles** | Les faits (F1) ne sont jamais écrasés ; chaque commande appartient à un appareil ; **chaque personne qui encaisse a sa propre caisse** et la remet à la fermeture ; le réseau local, quand il existe, sert à accélérer sans être nécessaire | Fonctionne réseau coupé ; reflète la réalité (le serveur garde l'argent en poche puis le remet) ; conflits rares et **visibles** ; s'appuie sur le journal déjà obligatoire | Modèle plus exigeant à concevoir ; transférer une commande entre serveurs exige une connexion ou un geste explicite ; rapports à calculer à partir des faits | Moyenne à élevée à la conception, **modérée** à l'exploitation |

### 4.4 Recommandation pour C1

**Retenir O4 comme principe**, avec deux compléments :

1. **Modes de fonctionnement configurables par établissement** :
   - **Mode poste unique** (O3) pour les établissements à caisse centralisée (profil pilote 1) ;
   - **Mode multi-encaisseurs** (O4) pour les serveurs qui encaissent (profil pilote 2) et les établissements multi-emplacements (profil 3).
2. **Réseau local facultatif** : s'il existe, il accélère la circulation des faits et donne une visibilité croisée en salle. **Rien ne dépend de lui** pour la cohérence.

**Règles du mode dégradé** (appareil sans contact avec les autres) :

| Un appareil hors ligne PEUT | Un appareil hors ligne NE PEUT PAS |
|---|---|
| Ouvrir une nouvelle commande, qui lui appartient | Modifier ou annuler une commande appartenant à un autre appareil |
| Ajouter des lignes à **ses** commandes | Transférer une commande vers un autre serveur |
| Confirmer la remise de boissons de **ses** commandes | Changer un prix ou le catalogue |
| Enregistrer un paiement **dans sa propre caisse** | Faire approuver une opération sensible par une personne absente |
| Enregistrer une dépense, si son rôle l'y autorise | Présenter ses chiffres comme consolidés |
| Obtenir une approbation d'une personne **présente** qui s'identifie sur l'appareil | |

**Traitement du scénario 4.1 avec O4**

| Événement | Résultat |
|---|---|
| Serveur B ajoute 2 bières sur la commande de A | **Refusé** hors connexion : B ouvre une commande séparée pour la table 5 (« table 5 — B »). L'addition de la table regroupe les deux commandes quand les appareils se retrouvent, ou elle est présentée séparément |
| Double paiement de la même addition | Les deux paiements sont **conservés**. À la synchronisation : anomalie « **trop-perçu** » sur la table 5, rattachée aux deux caisses. Le paiement Orange Money reste « déclaré » tant qu'il n'est pas vérifié (lien avec C5) |
| Stock à −1 | Les deux remises sont conservées. Alerte « stock négatif » : il y a une erreur de comptage ou un transfert non enregistré. **La vente n'est jamais bloquée** : la bouteille était physiquement là |
| Annulation par le gérant d'une bière déjà remise | Les deux faits sont concurrents. À la synchronisation : **conflit « annulation après remise »**. Aucune réintégration automatique en stock ; approbation et justification exigées |

### 4.5 Décisions métier nécessaires pour C1

| # | Décision | Proposition par défaut | Statut |
|---|---|---|---|
| M1 | Modes poste unique / multi-encaisseurs, configurés par établissement | Oui | À ARBITRER (Q16) |
| M2 | Chaque personne qui encaisse a sa propre caisse et la remet à la fermeture | Oui | À VÉRIFIER SUR LE TERRAIN (grille d'observation, flux de l'argent) |
| M3 | Traitement d'un trop-perçu : rendu au client, pourboire déclaré, ou avoir ? | Rendu ou avoir, **jamais** absorbé en silence | À ARBITRER |
| M4 | Stock négatif autorisé avec alerte, ou vente bloquée ? | Autorisé avec alerte | PROPOSÉ |
| M5 | Vente avec un prix périmé (appareil hors ligne) | Le prix utilisé est conservé ; alerte au gérant ; pas de correction rétroactive automatique | PROPOSÉ |
| M6 | Qui peut transférer une commande entre serveurs, et à quelle condition ? | Le gérant, avec les deux appareils connectés ou en présence des deux serveurs | À ARBITRER |
| M7 | **Encaissement uniquement sur des appareils appartenant à l'établissement**, ou aussi sur les téléphones personnels du personnel ? | Encaissement sur appareils de l'établissement ; prise de commande éventuellement sur téléphone personnel | À ARBITRER (Q18, lié à Q4) |

> **Pourquoi M7 est structurant** : sur un téléphone personnel, l'employé peut désinstaller l'application, effacer ses données ou partir avec l'appareil. La détection des trous de séquence rend l'effacement visible, mais ne récupère pas les opérations perdues.

---

## 5. C2 — Clôture avec opérations non synchronisées

### 5.1 Scénario réel

Dimanche, 1 h 30. Le caissier prépare la clôture sur la tablette ; le gérant doit la valider avant de partir.

- Le téléphone du serveur B est éteint depuis 23 h (batterie vide). Il contient 6 commandes, dont 2 paiements Orange Money déclarés.
- Le serveur B a 15 000 FCFA en poche.
- Le gérant valide la clôture. Le propriétaire, chez lui, voit « clôture validée, écart 0 ».
- Lundi midi, le téléphone de B est rechargé et synchronise.

Variante frauduleuse : B garde volontairement son téléphone éteint, ne remet pas l'argent, puis efface l'application.

### 5.2 Risques

| Risque | Opérationnel | Financier |
|---|---|---|
| Clôture définitive incomplète | Le propriétaire croit à des chiffres faux | Ventes et encaissements sous-estimés |
| Opérations tardives versées dans le jour suivant | Deux journées fausses au lieu d'une | Écarts fictifs, accusations injustes du personnel |
| Clôture bloquée par un appareil absent | Le personnel ne peut pas partir à 2 h | Contournement : on n'utilise plus l'outil |
| Vecteur de fraude (appareil éteint, données effacées) | Argent non remis | **Perte directe** que l'outil prétend empêcher |

**Classement : CRITIQUE** (cohérence financière ; règle « non synchronisé ≠ consolidé »).

### 5.3 Options comparées

| Option | Principe | Avantages | Limites | Coût / complexité |
|---|---|---|---|---|
| **K1 — Clôture bloquante** | Pas de clôture tant que tous les appareils n'ont pas synchronisé | Cohérence parfaite | Un téléphone mort bloque tout ; inapplicable à 2 h du matin ; contournements | Faible à concevoir, **inacceptable** à l'usage |
| **K2 — Clôture en deux temps** | **Clôture provisoire** la nuit (comptage physique, écart provisoire) ; **clôture consolidée** automatiquement quand tous les appareils de la journée ont transmis toutes leurs opérations, ou par décision journalisée déclarant un appareil absent | Respecte la règle « non synchronisé ≠ consolidé » ; ne bloque pas le personnel | Le propriétaire doit comprendre deux statuts ; il faut savoir **quels appareils** ont travaillé dans la journée | Moyenne |
| **K3 — Remise individuelle obligatoire** | Chaque personne qui a encaissé fait sa **remise de caisse** auprès du caissier avant de partir : son appareil transmet ses opérations à l'appareil de clôture (par contact local) et l'argent est compté en sa présence | Fait coïncider la remise physique de l'argent et la remise des données ; rend la fraude visible sur le moment | Ne résout pas l'appareil en panne ; demande une discipline de fermeture | Moyenne |

### 5.4 Recommandation pour C2

**Combiner K3 et K2.**

**Pendant la journée**
- **Ouverture de service** : chaque appareil qui va servir se déclare en début de service (registre des appareils du jour). Une opération provenant d'un appareil non déclaré est marquée « hors session » et signalée.

**À la fermeture**
1. **Remise individuelle (K3)** : chaque encaisseur remet son argent **et** ses opérations. Le caissier voit, pour chaque personne : ventes, encaissements par moyen de paiement, argent attendu, argent remis, écart.
2. **Clôture provisoire (K2)** préparée par le caissier, validée par le gérant (pas d'auto-validation quand la séparation est requise).
3. Si un appareil n'a pas pu remettre ses opérations : la remise d'argent est enregistrée comme **déclarée**, et la clôture affiche **« provisoire — appareil manquant : téléphone de B »**.

**Après la fermeture**
4. Quand toutes les opérations des appareils du jour sont reçues **jusqu'à leur dernier numéro de séquence**, la clôture passe automatiquement en **« consolidée »**.
5. Les opérations arrivées en retard sont **rattachées à leur journée d'exploitation d'origine** (jamais versées dans le lendemain), sous forme d'**ajustement post-clôture journalisé** et signalé au propriétaire.
6. Au-delà d'un **délai limite** (M10), une alerte « appareil non synchronisé » remonte au propriétaire.
7. Une personne habilitée, **différente de celle qui a préparé la clôture**, peut déclarer un appareil « absent » avec justification : la clôture devient **« consolidée avec réserve »**. Les opérations reçues ensuite restent traitées en ajustement.

**Ce que voit le propriétaire**

| Statut | Signification |
|---|---|
| **En cours** | La journée n'est pas fermée |
| **Provisoire** | Comptage fait ; des opérations peuvent encore arriver (liste des appareils manquants) |
| **Consolidée** | Toutes les opérations de tous les appareils du jour sont reçues |
| **Consolidée avec réserve** | Un appareil a été déclaré absent par une personne habilitée, avec justification |
| **Ajustée** | Des opérations tardives ont modifié la journée après consolidation (historique visible) |

**Traitement du scénario 5.1** : la clôture de 1 h 30 apparaît « provisoire — téléphone de B manquant ; remise de B : déclarée 15 000 FCFA ». Lundi midi, les 6 commandes arrivent, sont rattachées au samedi, la journée passe « consolidée », et le propriétaire voit l'écart réel. Dans la variante frauduleuse, le téléphone de B ne synchronise jamais : alerte au délai limite, puis clôture « consolidée avec réserve » décidée par une personne habilitée. Si B efface l'application après avoir synchronisé une partie, le trou de séquence est signalé.

### 5.5 Décisions métier nécessaires pour C2

| # | Décision | Proposition par défaut | Statut |
|---|---|---|---|
| M8 | Clôture en deux temps (provisoire / consolidée) et 5 statuts visibles par le propriétaire | Oui | À ARBITRER (Q17) |
| M9 | Remise individuelle obligatoire avant le départ de chaque encaisseur | Oui | À ARBITRER (Q17) · À VÉRIFIER SUR LE TERRAIN |
| M10 | Délai limite avant alerte pour un appareil non synchronisé | Court (de l'ordre de la journée suivante) ; valeur à fixer après le pilote | PROPOSÉ |
| M11 | Qui peut déclarer un appareil absent ? | Gérant ou propriétaire, **différent** du préparateur de la clôture ; justification obligatoire | PROPOSÉ |
| M12 | Opérations tardives : rattachées au jour d'origine avec ajustement journalisé, ou comptées le jour de réception ? | Jour d'origine | À ARBITRER (Q19) |
| M13 | Ouverture de service obligatoire pour chaque appareil | Oui | PROPOSÉ |

---

## 6. Tests à réaliser en preuve de faisabilité (Phase C)

Chaque test a un **résultat attendu** vérifiable. Un test échoué sur C1 ou C2 est une anomalie critique (interdiction de lancement, règle de la Porte 4).

### 6.1 Tests C1

| # | Test | Résultat attendu |
|---|---|---|
| T1 | Deux appareils hors ligne tentent de modifier la même commande | L'appareil non propriétaire est refusé et guidé vers une commande séparée |
| T2 | Deux appareils hors ligne enregistrent le paiement intégral de la même addition | Les deux paiements sont conservés ; anomalie « trop-perçu » à la synchronisation |
| T3 | La même référence Mobile Money est déclarée sur deux appareils | Doublon détecté ; un seul paiement peut être vérifié |
| T4 | La même opération est renvoyée 3 fois (coupures pendant l'envoi) | Enregistrée une seule fois |
| T5 | Deux appareils confirment la remise des dernières bouteilles | Stock négatif + alerte ; aucune remise perdue |
| T6 | Annulation et remise concurrentes de la même ligne | Conflit signalé ; aucune réintégration automatique en stock |
| T7 | Prix modifié pendant qu'un appareil est hors ligne | La vente garde le prix utilisé ; alerte à la synchronisation |
| T8 | Horloge d'un appareil reculée d'un jour | Ordre des opérations préservé par la séquence ; dérive signalée |
| T9 | Données de l'application effacées avant synchronisation complète | Trou de séquence détecté ; alerte au propriétaire |
| T10 | 3 appareils, 24 h hors ligne, ~300 opérations | Synchronisation complète, sans perte ni doublon ; durée mesurée |
| T11 | Perte de l'appareil pivot (si réseau local utilisé) avant envoi au cloud | Aucune perte des opérations créées sur les autres appareils ; les opérations créées sur le pivot sont **aussi** détenues par au moins un autre appareil |

### 6.2 Tests C2

| # | Test | Résultat attendu |
|---|---|---|
| T12 | Clôture avec un appareil éteint | Statut « provisoire », appareil manquant nommé, remise d'argent « déclarée » |
| T13 | L'appareil synchronise après la clôture | Opérations rattachées au bon jour ; passage en « consolidée » ; ajustement journalisé ; propriétaire notifié |
| T14 | Déclaration d'un appareil absent | Refusée si c'est le préparateur ; justification obligatoire ; statut « consolidée avec réserve » |
| T15 | Opérations d'un appareil non déclaré en ouverture de service | Marquées « hors session » et signalées |
| T16 | Remise individuelle sans internet | Les opérations passent de l'appareil du serveur à l'appareil de clôture par contact local |
| T17 | Délai limite dépassé | Alerte au propriétaire |
| T18 | Le tableau de bord affiche une journée incomplète | Jamais présentée comme « consolidée » |

---

## 7. Coût et maintenance à long terme

| Point | Analyse |
|---|---|
| Le moteur de synchronisation est le composant le plus coûteux du produit | Il concentre la complexité, les anomalies et le support. À 10 000 FCFA/mois, chaque appel d'assistance lié à la synchronisation pèse sur la marge (lien avec C7) |
| Construire ou s'appuyer sur l'existant | La Phase C devra comparer un **mécanisme de synchronisation éprouvé** et un développement spécifique. Un développement spécifique non maîtrisé est un risque de dépendance à une seule personne |
| Appareil pivot (O2) | Ajoute de la configuration sur site et du support ; ne le retenir que s'il apporte une valeur mesurée en pilote |
| Journal des faits | Il est déjà exigé par les règles d'audit : le modèle O4 réutilise une obligation existante au lieu d'en ajouter une |
| Simplicité d'usage | Les statuts de clôture et les anomalies doivent être compréhensibles par un gérant peu familier du numérique : libellés courts, couleurs, une action proposée par anomalie |

**Option de séquencement** (à décider plus tard, pas maintenant) : commencer les pilotes par le profil à caisse centralisée (mode poste unique, risque plus faible), puis le profil multi-encaisseurs. Cela ne retire pas le mode multi-encaisseurs du périmètre ; cela ordonne les risques.

---

## 8. Limites de cette analyse

- Les principes ci-dessus réduisent les conflits ; ils ne les suppriment pas. Il restera des anomalies à traiter par une personne : leur **fréquence réelle** n'est connue qu'au pilote.
- La remise individuelle (K3) suppose une discipline de fermeture qui reste à observer sur le terrain.
- Le contact local entre appareils (T16) est un objectif. Sa faisabilité sur des téléphones d'entrée de gamme est à démontrer en Phase C.
- Aucune solution ne protège contre un employé qui **ne saisit pas** une vente. Ce risque relève du contrôle par le stock (comptage, rapprochement), traité en B3 avec C6.

---

## 9. Décisions à prendre

| # | Question | Recommandation |
|---|---|---|
| **Q16** | Validez-vous le principe des **faits en ajout seul + propriété unique des commandes + caisses individuelles**, avec deux modes configurables (poste unique / multi-encaisseurs) ? | Oui |
| **Q17** | Validez-vous la **clôture en deux temps** avec 5 statuts, et la **remise individuelle obligatoire** avant le départ de chaque encaisseur ? | Oui |
| **Q18** | Encaissement réservé aux **appareils de l'établissement** (téléphones personnels limités à la prise de commande) ? Cette question complète Q4 | Oui, sous réserve des préférences notées en démo |
| **Q19** | Opérations tardives rattachées à **leur journée d'origine**, en ajustement journalisé ? | Oui |

Les autres décisions métier (M3, M4, M5, M6, M10, M11, M13) ont des valeurs par défaut proposées ; elles seront confirmées après les observations de fermeture.

---

## 10. Registre des décisions (mise à jour séance B1)

| ID | Élément | Statut |
|---|---|---|
| D-A4-04 | 6 établissements observés | **VALIDÉ** (Q15) |
| D-A4-11 | Règle d'arrêt anticipé | **VALIDÉ** (Q15) |
| D-B1-01 | Trois familles de données (faits / états partagés / référentiels) | **VALIDÉ** |
| D-B1-02 | Interdiction de « la dernière modification gagne » pour les données financières | **VALIDÉ** |
| D-B1-03 | Séquence par appareil, pas d'ordonnancement sur l'heure de l'appareil | **VALIDÉ** |
| D-B1-04 | Détection des trous de séquence et alerte au propriétaire | **VALIDÉ** |
| D-B1-05 | Modèle O4 + modes poste unique / multi-encaisseurs | **VALIDÉ** (Q16) |
| D-B1-06 | Réseau local facultatif, jamais nécessaire à la cohérence | **VALIDÉ** |
| D-B1-07 | Règles du mode dégradé (§4.4) | **VALIDÉ** |
| D-B1-08 | Caisse individuelle par encaisseur (M2) | **VALIDÉ** en principe · À VÉRIFIER SUR LE TERRAIN |
| D-B1-09 | Traitement du trop-perçu (M3) | **VALIDÉ** : rendu au client ou avoir, jamais absorbé en silence |
| D-B1-10 | Stock négatif autorisé avec alerte (M4) | **VALIDÉ** |
| D-B1-11 | Prix utilisé conservé, alerte si périmé (M5) | **VALIDÉ** |
| D-B1-12 | Transfert de commande entre serveurs (M6) | **VALIDÉ** : le gérant, appareils connectés ou en présence des deux serveurs |
| D-B1-13 | Encaissement sur appareils de l'établissement (M7) | **VALIDÉ** (Q18) · impact équipement à chiffrer (Q4) |
| D-B1-14 | Clôture en deux temps, 5 statuts (M8) | **VALIDÉ** (Q17) |
| D-B1-15 | Remise individuelle obligatoire (M9) | **VALIDÉ** (Q17) · À VÉRIFIER SUR LE TERRAIN |
| D-B1-16 | Délai limite d'alerte (M10) | **VALIDÉ** en principe · valeur fixée après pilote |
| D-B1-17 | Déclaration d'appareil absent par une personne différente du préparateur (M11) | **VALIDÉ** |
| D-B1-18 | Opérations tardives rattachées au jour d'origine (M12) | **VALIDÉ** (Q19) |
| D-B1-19 | Ouverture de service obligatoire par appareil (M13) | **VALIDÉ** |
| D-B1-20 | Tests T1 à T18 inscrits au plan de la preuve de faisabilité | **VALIDÉ** |
| D-B1-21 | Séquencement des pilotes (poste unique d'abord) | REPORTÉ (décision en Phase E) |
| C1 | Plusieurs appareils hors ligne | **BLOQUANT** jusqu'à réussite des tests T1–T11 |
| C2 | Clôture et opérations non synchronisées | **BLOQUANT** jusqu'à réussite des tests T12–T18 |

---

## 11. Validation (fin de séance)

Le fondateur a validé l'ensemble des recommandations de la séance : Q16, Q17, Q18, Q19 et les valeurs par défaut des décisions métier M3 à M13. Le registre du §10 est mis à jour.

**Ce que la validation ne change pas**
- C1 et C2 restent **BLOQUANTS** tant que les tests T1 à T18 n'ont pas réussi en preuve de faisabilité : on a validé une conception, pas un résultat.
- M2 (caisse individuelle) et M9 (remise individuelle obligatoire) restent **à vérifier sur le terrain** pendant les observations de fermeture.
- Le séquencement des pilotes reste **REPORTÉ**.

**Conséquences à suivre**

| Conséquence | Explication | Où elle sera traitée |
|---|---|---|
| **Coût d'équipement accru en mode multi-encaisseurs** | Avec Q18, chaque personne qui encaisse utilise un appareil de l'établissement. Un snack avec 3 serveurs encaisseurs et un caissier a besoin de 4 appareils. La politique d'équipement (Q4) et le modèle financier doivent en tenir compte | Q4 (après les démos), Phase D |
| **L'avoir est une dette envers le client** | Un trop-perçu transformé en avoir doit être identifié et suivi comme un crédit inversé (bénéficiaire, montant, utilisation) | Séance B3 ou B4, avec les règles de crédit |
| **La remise individuelle doit rester rapide** | À 2 h du matin, une remise trop longue sera contournée. Sa durée réelle est à mesurer pendant les observations et à tester en maquette | Observations Phase A ; Phase C |

---

## 12. Prochaine étape proposée

**Séance B2 — C3 (journée d'exploitation après minuit) et C4 (cumul des rôles)**.
- C3 est directement lié à C2 : le rattachement des opérations tardives à « leur journée d'origine » suppose une définition fiable de la journée d'exploitation.
- C4 conditionne la règle « pas d'auto-validation » utilisée dans toute la clôture : que faire quand le gérant est aussi le caissier ?

Les séances suivantes : **B3** (C5 Mobile Money et C6 inventaires en service), **B4** (C7 rentabilité du support et C8 licence hors ligne).
