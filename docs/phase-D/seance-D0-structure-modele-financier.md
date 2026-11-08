# MAQUIS CONTROL — Séance D0
## Phase D · Structure du modèle financier (sans chiffres inventés)

> **Statut** : compte rendu de séance de brainstorming. Ce n'est **ni** le business plan, **ni** des prévisions financières (livrables soumis à autorisation).
> **Règle chiffrée stricte** :
> - **Décisions validées** : 25 000 FCFA d'installation, 10 000 FCFA/mois, paliers 10 / 30 / 50 clients, réserve de 3 mois, grâce de 7 jours. Ce sont les seuls montants utilisés comme tels.
> - **Calculs arithmétiques** : conséquences directes des décisions validées.
> - **Hypothèses de simulation** : marquées *(simulation)*, utilisées uniquement pour montrer une sensibilité. **Aucune n'est une donnée ni une prévision.**
> - **Données observées** : **aucune** à ce jour. Le terrain n'a pas commencé.

---

## 1. Objectif de la séance

1. Définir la structure des revenus, des coûts et des investissements.
2. Formaliser les indicateurs demandés (MRR, ARR, marge de contribution, CAC, LTV, délai de récupération, point mort, besoin de financement, trésorerie) avec leurs formules et hypothèses.
3. Définir les scénarios prudent, central et défavorable.
4. Identifier les tensions économiques que la structure révèle déjà.
5. Établir le plan de collecte des données, phase par phase.

## 2. Décisions validées qui encadrent le modèle

| Décision | Effet sur le modèle |
|---|---|
| **Validation de C0** : Q32 à Q36 | Coût de la Phase C chiffré après consultation de 2 prestataires, libéré par lots |
| Prix 25 000 + 10 000/mois d'avance, Mobile Money, grâce 7 jours | Pas de créances clients au-delà de la grâce |
| Pilote gratuit 30 jours ; acompte P3 promis, versé à la confirmation, déduit de l'installation | Le pilote est un **coût sans revenu** ; l'acompte avance l'encaissement, il n'ajoute pas de revenu |
| Services payants (Q28) | Validés **en principe, à tester** : revenu à **zéro** dans tous les scénarios tant qu'ils ne sont pas testés |
| Encaissement sur appareils de l'établissement (B1) | Plusieurs appareils par client en mode multi-encaisseurs ; coût selon la politique d'équipement (Q4) |
| Support : référent, installation standardisée, journal du temps (B4) | Le temps de support par client est une **variable clé** du modèle |
| Investissement progressif par jalons ; réserve de 3 mois de charges | Besoin de financement calculé par jalon |
| Croissance 10 → 30 → 50 clients | Paliers de revenus (§5) |

---

## 3. Structure des revenus

| Ligne | Formule | Statut |
|---|---|---|
| **Abonnements** | Clients actifs payants × 10 000 | Prix validé ; nombre de clients **hypothèse** |
| **Installations** | Nouveaux clients payants × 25 000 (moins l'acompte déjà encaissé) | Validé |
| **Services payants** | Zéro tant que non testés (Q28) | À tester |
| **Équipement** | Selon Q4 : nul (appareils du client), marge de revente (vendus), ou coût sans revenu (inclus) | À arbitrer après les démos |
| **Encaissements effectifs** | Revenus × taux de paiement à temps ; pertes en cas de suspension | Hypothèse |

### 3.1 Question fiscale préalable : 10 000 FCFA, hors taxes ou toutes taxes comprises ?

Si la structure porteuse est assujettie à la TVA (taux normal généralement cité à **18 %** au Burkina Faso, **à confirmer**), le revenu net diffère fortement selon que le prix annoncé est hors taxes ou toutes taxes comprises.

| Si 10 000 FCFA est… | Revenu hors taxes par client et par mois |
|---|---|
| Hors taxes | 10 000 |
| Toutes taxes comprises (TVA 18 %, à confirmer) | ≈ 8 475 |

Dans les démos, le prix est annoncé sans mention de taxe : les propriétaires le comprendront **toutes taxes comprises**. **Par prudence, le modèle doit raisonner en TTC** tant que le régime fiscal de la structure n'est pas fixé. → À ARBITRER (Q37), lié à Q8 (entité juridique).

---

## 4. Structure des coûts

### 4.1 Coûts variables mensuels par client

| Poste | Formule | Source attendue |
|---|---|---|
| Frais d'encaissement Mobile Money des abonnements | % × abonnement | Conditions des opérateurs (à vérifier) |
| Hébergement et infrastructure marginale | Coût par client | Phase C (tests de charge) |
| SMS (rappels, codes de réactivation) | Nombre × coût unitaire | Fournisseur SMS (à vérifier) |
| **Support** | Minutes par client × coût horaire ÷ 60 | **Pilote** (mesure T54) |
| Licences de tiers (moteur de synchronisation, si option Y1) | Par client ou par appareil | Phase C |
| Amortissement et remplacement des appareils | Si appareils inclus (Q4) | Démos (Q4), fournisseurs |
| Stockage des sauvegardes | Par client | Phase C |

### 4.2 Coûts ponctuels par nouveau client

| Poste | Formule | Source attendue |
|---|---|---|
| Acquisition | Temps de prospection et de démo × coût horaire + déplacements | **Journal de recrutement (Phase A)**, puis lancement |
| Installation | Heures (préparation, visite, appels J+2 et J+7, bilan J+30) × coût horaire + déplacement | **Pilote** (mesure T53) |
| Appareils | Si inclus ou avancés | Q4 |

### 4.3 Coûts fixes mensuels

| Poste | Remarque |
|---|---|
| **Rémunération du fondateur** | Décision clé : le point mort se calcule **avec** et **sans** (Q38) |
| Personnel de support | À partir du palier où le volume l'exige (voir B4 §3.3) |
| Maintenance et évolution du produit | Contrat avec le prestataire technique ; **poste fixe le plus incertain** |
| Hébergement de base, outils (dépôt de code, secrets, supervision, sauvegardes indépendantes) | Phase C |
| Comptabilité, juridique, assurance | Devis |
| Téléphone, données, déplacements non affectés | Estimation |
| Audit de sécurité périodique | À prévoir avant le passage à l'échelle |

### 4.4 Investissements par jalon

| Jalon | Contenu | Source |
|---|---|---|
| Phase A | Budget du jalon (A4 §5), dont maquette | Coûts unitaires (Q12) |
| Création de l'entité et cadre juridique | Statuts, contrats, CGU, protection des données, fiscalité (FEC) | Devis |
| Phase C | Preuve de faisabilité, par lots | Consultation de 2 prestataires |
| Phase E | Développement du MVP | Estimation issue de la Phase C |
| Phase F | 3 pilotes gratuits (installation, appareils de test, support, sans revenu) | Phase A + devis |
| Réserve | 3 mois de charges d'exploitation | Calculée (§6.8) |

---

## 5. Ce que la structure révèle déjà : le plafond de revenus du plan 10 / 30 / 50

**Calcul arithmétique à partir des seules décisions validées** (abonnements, hors installations) :

| Palier | Revenu mensuel des abonnements | Si 10 000 est TTC (TVA 18 %, à confirmer) : revenu HT |
|---|---|---|
| 10 clients | 100 000 FCFA | ≈ 84 700 FCFA |
| 30 clients | 300 000 FCFA | ≈ 254 200 FCFA |
| 50 clients | 500 000 FCFA | ≈ 423 700 FCFA |

**Conséquence** : au palier de 50 clients, **tous** les coûts — rémunération du fondateur, support, maintenance du produit, hébergement, outils, comptabilité — doivent tenir dans environ **500 000 FCFA par mois au maximum, avant déduction des coûts variables**.

**Illustration du point mort** *(simulation : valeurs de marge et de coûts fixes non observées)*

Nombre de clients au point mort = coûts fixes mensuels ÷ marge de contribution par client.

| Coûts fixes mensuels *(simulation)* | Marge par client 5 000 *(simulation)* | 6 500 *(simulation)* | 8 000 *(simulation)* |
|---|---|---|---|
| 300 000 FCFA | 60 clients | 47 clients | 38 clients |
| 600 000 FCFA | 120 clients | 93 clients | 75 clients |
| 1 000 000 FCFA | 200 clients | 154 clients | 125 clients |

**Lecture** : avec ces valeurs de simulation, le palier de 50 clients n'atteint le point mort que si les coûts fixes restent très bas. Une rémunération du fondateur, un contrat de maintenance ou un employé de support peuvent repousser le point mort **au-delà de 50 clients**.

**Ce n'est pas une conclusion** : ni la marge ni les coûts fixes ne sont connus. C'est une **tension structurelle à vérifier en priorité** dès que les premiers coûts réels seront disponibles. Trois leviers existent, à étudier en Phase D **sans modifier les décisions validées à ce stade** :

| Levier | Principe | Remarque |
|---|---|---|
| Volume | Viser un nombre de clients supérieur à 50 avant d'exiger la rentabilité | Augmente le besoin de financement et le support |
| Revenu par client | Services payants (Q28, à tester) ; tarification selon le nombre d'encaisseurs ou d'appareils ; tarif multi-établissements | Le mode multi-encaisseurs coûte plus (appareils, support) pour le même prix : **subvention croisée** actuelle entre petits et grands clients |
| Coûts fixes | Produit qui limite le support (B4), maintenance au forfait réduit, mutualisation | Limité par la qualité attendue |

---

## 6. Indicateurs : définitions, formules et hypothèses

### 6.1 MRR et ARR

- **MRR** = nombre de clients actifs payants × abonnement mensuel (hors installations, hors services ponctuels).
- **ARR** = MRR × 12.
- Un client en **période de grâce** est compté dans le MRR ; un client **suspendu** ne l'est pas.
- Les pilotes gratuits ne sont pas comptés.

### 6.2 Marge de contribution par client

Marge de contribution mensuelle = abonnement (HT si assujetti) − frais d'encaissement − hébergement marginal − SMS − **support** − licences de tiers − amortissement des appareils inclus.

Elle se calcule **par type d'établissement** (§7), pas seulement en moyenne.

### 6.3 CAC

Deux versions, à ne pas confondre :

| Indicateur | Formule | Usage |
|---|---|---|
| **CAC décaissé** | Dépenses d'acquisition de la période ÷ nouveaux clients payants | Trésorerie |
| **CAC économique** | (Dépenses + temps du fondateur valorisé) ÷ nouveaux clients payants | Viabilité réelle, coût du jour où le fondateur ne vendra plus seul |

**CAC net de l'installation** = CAC + coût d'installation − 25 000.
Si l'installation coûte moins de 25 000, elle réduit le CAC net ; sinon, elle l'aggrave.

### 6.4 LTV

LTV = marge de contribution mensuelle × durée de vie moyenne d'un client.

Avec un **taux de résiliation mensuel constant** (hypothèse simplificatrice), durée de vie moyenne ≈ 1 ÷ taux de résiliation.

| Résiliation mensuelle *(simulation)* | Durée de vie moyenne |
|---|---|
| 3 % | ≈ 33 mois |
| 5 % | 20 mois |
| 10 % | 10 mois |

**Limite** : le taux de résiliation **ne peut pas être mesuré avant plusieurs mois** d'abonnements payants (Phase G). Jusque-là, toute LTV est une simulation.

### 6.5 Délai de récupération du CAC

Délai (mois) = CAC net de l'installation ÷ marge de contribution mensuelle.

### 6.6 Point mort opérationnel

Nombre de clients au point mort = coûts fixes mensuels ÷ marge de contribution moyenne par client.

Calculé **deux fois** : sans rémunération du fondateur, puis avec (Q38).

### 6.7 Trésorerie mensuelle

Structure du tableau mensuel (horizon proposé : 36 mois) :

| Ligne |
|---|
| Trésorerie d'ouverture |
| + Abonnements encaissés (avec retards et suspensions) |
| + Installations encaissées (dont acomptes reçus) |
| + Services payants (zéro tant que non testés) |
| + Apports et financements |
| − Coûts variables |
| − Coûts d'acquisition et d'installation |
| − Coûts fixes |
| − Investissements des jalons |
| − TVA reversée (si assujetti) |
| = Trésorerie de clôture |
| Réserve exigée (3 mois de charges) |
| **Écart à la réserve** |

### 6.8 Besoin de financement

Besoin de financement = |plus bas niveau de trésorerie cumulée| + réserve de 3 mois de charges d'exploitation.

**Définition à fixer** : la réserve couvre 3 mois de **coûts fixes + coûts variables au niveau de clients du moment**. Les investissements de jalons sont financés à part, libérés par jalons.

### 6.9 Sensibilités obligatoires

| Variable | Pourquoi |
|---|---|
| Taux de résiliation | Détermine la LTV |
| **Minutes de support par client** | Variable clé du passage à l'échelle (B4) |
| CAC | Coût de croissance |
| Politique d'équipement (Q4) | Peut transformer chaque client multi-encaisseurs en coût initial élevé |
| Prix effectif (HT/TTC, acceptation réelle) | Revenu par client |
| Taux de paiement à temps | Trésorerie |
| Coût de maintenance du produit | Premier coût fixe |
| Rythme d'acquisition | Durée avant le point mort, donc besoin de financement |

---

## 7. Rentabilité par type d'établissement

Le même prix couvre des réalités de coût très différentes :

| Type | Appareils | Support attendu | Installation | Risque de marge |
|---|---|---|---|---|
| Mode poste unique (profil pilote 1) | 1 | Plus faible | Plus courte | Faible |
| Multi-encaisseurs + restauration (profil 2) | Plusieurs | Plus élevé (remises, Mobile Money, rotation) | Plus longue | **Élevé** |
| Multi-emplacements (profil 3) | Plusieurs | Élevé (transferts, inventaires) | Longue | **Élevé** |

Le modèle calcule la marge **par type**, pondérée par la composition réelle du portefeuille. Les pilotes fourniront une première mesure par type (mais un seul établissement par type : signal, pas statistique).

---

## 8. Scénarios

### 8.1 Logique

Un scénario est un **jeu cohérent** de valeurs des variables de sensibilité. Les valeurs seront fixées **à partir des données collectées** (§9) ; tant qu'elles n'existent pas, elles sont marquées *(simulation)* et accompagnées de leur justification.

| Variable | Défavorable | Central | Prudent |
|---|---|---|---|
| Rythme d'acquisition | Lent | Rythme mesuré en Phase A et au lancement | Légèrement inférieur au central |
| Résiliation mensuelle | Élevée | Mesurée sur les premières cohortes | Supérieure au central |
| Minutes de support par client | Élevées | Mesurées au pilote | Supérieures au central |
| CAC | Élevé (fondateur valorisé) | Journal de recrutement + lancement | Supérieur au central |
| Équipement | Inclus, à la charge de MAQUIS CONTROL | Politique retenue (Q4) | Politique retenue, avec remplacement accru |
| Prix effectif | TTC, avec acceptation partielle (remises) | TTC au prix validé | TTC au prix validé |
| Paiement à temps | Retards fréquents, suspensions | Mesuré | Légèrement dégradé |
| Services payants | Zéro | Zéro tant que non testés | Zéro |
| Maintenance du produit | Haute | Devis retenu | Devis + marge de sécurité |

**Règle** : les décisions d'investissement (portes) se prennent sur le scénario **prudent**, et le **défavorable** sert à dimensionner la réserve et les règles d'arrêt.

### 8.2 Questions auxquelles les scénarios doivent répondre

1. À quel palier de clients atteint-on le point mort, avec et sans rémunération du fondateur ?
2. Quel est le besoin de financement total, jalon par jalon, réserve comprise ?
3. Combien de mois avant de récupérer le CAC d'un client ?
4. Quels types d'établissements sont rentables au prix actuel ?
5. Quel temps de support par client rend le modèle non viable ?

---

## 9. Plan de collecte des données

| Phase | Données à collecter | Outil existant |
|---|---|---|
| **A — Terrain** | Contacts par entretien, temps et frais par entretien et par démo (base du CAC) ; réactions au prix ; préférences d'équipement ; nombre d'encaisseurs et d'appareils par établissement ; rotation du personnel si mentionnée ; dépenses actuelles de contrôle | Journal de recrutement, fiches de notation et de démo (A2, A3) |
| **Juridique et fiscal** | Régime fiscal de la structure ; TVA ; coût de création ; impact FEC | Consultation (Q8, Q23) |
| **C — Faisabilité** | Coût réel de la preuve de faisabilité ; coût d'hébergement par client (tests de charge) ; licences éventuelles ; estimation de l'effort du MVP | Lots L1–L8, devis |
| **E — Développement** | Coût réel du MVP ; devis de maintenance | Contrat |
| **F — Pilote** | Durée d'installation par étape ; minutes de support par client et par catégorie ; incidents ; appareils ; taux de conversion des pilotes ; acceptation des services payants | Mesures T53–T58, journal de support |
| **G — Lancement** | CAC réel ; taux de paiement à temps ; **résiliation par cohorte** (au moins 3 à 6 mois) | Suivi des abonnements |

**Conséquence pour les portes** : à la Porte 6, la LTV doit reposer sur des **cohortes réelles** d'au moins plusieurs mois, pas sur une hypothèse.

---

## 10. Outil de modélisation proposé

Un classeur avec les onglets suivants (à produire **sur autorisation**, vide de toute valeur inventée) :

| Onglet | Contenu |
|---|---|
| Paramètres | Chaque variable avec **valeur, unité, source, statut** (validé / observé / simulation / manquant) et date |
| Économie unitaire | Marge de contribution, CAC, LTV, délai de récupération, **par type d'établissement** |
| Trésorerie | 36 mois, structure du §6.7 |
| Scénarios | Défavorable / central / prudent |
| Sensibilités | Tableaux à une et deux variables (résiliation × support, CAC × rythme…) |
| Jalons | Investissement et décision par porte |
| Journal des versions | Qui a changé quoi, pourquoi |

---

## 11. Risques et limites

| ID | Risque | Classe | Traitement |
|---|---|---|---|
| RD1 | **Plafond de revenus du plan 10/30/50** incompatible avec des coûts fixes réalistes | **Majeur** | Vérifier dès les premiers coûts ; leviers du §5 |
| RD2 | Prix compris TTC alors que la structure est assujettie à la TVA | Majeur | Q37 ; vérification fiscale |
| RD3 | Subvention croisée entre petits et grands établissements | Majeur | Marge par type (§7) ; étude de tarification |
| RD4 | Coût de maintenance du produit sous-estimé | Majeur | Devis dès la Phase C ; scénario prudent |
| RD5 | LTV calculée sans cohortes réelles | Majeur | Pas de décision de passage à l'échelle sur une LTV simulée |
| RD6 | Outils facturés en devises (hébergement, licences) | Modéré | Variable de change dans les paramètres |
| RD7 | Rémunération du fondateur ignorée dans le point mort | Majeur | Double calcul (Q38) |

**Limite principale** : ce document définit **comment** calculer, pas **combien**. Aucun indicateur ne peut être chiffré honnêtement avant les premiers devis et les premières mesures de terrain.

---

## 12. Décisions à prendre

| # | Question | Recommandation |
|---|---|---|
| **Q37** | Le modèle raisonne-t-il en **TTC** (10 000 FCFA = prix final payé par le client) tant que le régime fiscal n'est pas fixé ? | Oui (prudence) |
| **Q38** | Le point mort se calcule-t-il **avec et sans** rémunération du fondateur ? | Oui |
| **Q39** | Acceptez-vous que la Phase D étudie des **leviers de revenu par client** (tarification selon le nombre d'encaisseurs ou d'appareils, multi-établissements, services payants), **sans modifier le prix validé** avant les données de terrain ? | Oui |
| **Q40** | Autorisez-vous la production du **classeur de modélisation vide** (structure et formules, sans valeur inventée) ? | Oui, quand les premiers coûts unitaires (Q12) seront disponibles |
| **Q41** | Validez-vous les définitions (§6), les scénarios (§8, décisions sur le scénario prudent) et le plan de collecte (§9) ? | Oui |

---

## 13. Registre des décisions (mise à jour séance D0)

| ID | Élément | Statut |
|---|---|---|
| D-C0-01 à D-C0-15 | Décisions de la séance C0 | **VALIDÉ** (D-C0-08 REPORTÉ ; D-C0-09 et D-C0-16 À VÉRIFIER) |
| D-D0-01 | Structure des revenus, coûts et investissements (§3, §4) | PROPOSÉ |
| D-D0-02 | Raisonnement en TTC tant que le régime fiscal n'est pas fixé | À ARBITRER (Q37) |
| D-D0-03 | Point mort avec et sans rémunération du fondateur | À ARBITRER (Q38) |
| D-D0-04 | Plafond de revenus du plan 10/30/50 identifié comme tension majeure | PROPOSÉ (signalement, aucune décision validée modifiée) |
| D-D0-05 | Étude des leviers de revenu par client en Phase D | À ARBITRER (Q39) |
| D-D0-06 | Définitions des indicateurs (§6), CAC décaissé et économique | À ARBITRER (Q41) |
| D-D0-07 | Marge calculée par type d'établissement | À ARBITRER (Q41) |
| D-D0-08 | Trois scénarios ; décisions sur le prudent, réserve dimensionnée sur le défavorable | À ARBITRER (Q41) |
| D-D0-09 | Plan de collecte des données par phase | À ARBITRER (Q41) |
| D-D0-10 | Définition de la réserve : coûts fixes + variables au niveau de clients du moment ; jalons financés à part | PROPOSÉ |
| D-D0-11 | Classeur de modélisation vide | À ARBITRER (Q40) · sur autorisation |
| D-D0-12 | Services payants à zéro dans tous les scénarios tant que non testés | PROPOSÉ |
| D-D0-13 | Pas de décision de passage à l'échelle sur une LTV simulée | PROPOSÉ |
| D-D0-14 | Régime fiscal et TVA de la structure porteuse | À VÉRIFIER (lié à Q8) |

---

## 14. Prochaine étape proposée

Toutes les phases d'analyse (A à D) ont maintenant leur cadre. Le projet arrive au point où **seules des données réelles** peuvent faire avancer les décisions.

**Recommandation : revenir au chemin critique.**

| Priorité | Action | Bloque |
|---|---|---|
| 1 | Répondre à **Q3** (enquêteurs, langues, enregistrement) | Démarrage de S0 |
| 2 | Vérifier le **cadre légal des données personnelles** (entretiens, hébergement) | Premier entretien ; choix de l'hébergeur |
| 3 | Fournir les **coûts unitaires** (Q12) et la **date de démarrage** (Q14) | Budget de la Phase A ; calendrier |
| 4 | Lancer les **vérifications fiscales et juridiques** (FEC, TVA, entité) | Portes 2 et 6 |
| 5 | Autoriser la **maquette** (Q11) et fixer le **montant de l'acompte** (Q9) | Démos (S5) |

Séances de brainstorming utiles ensuite :
- **A5 — Point d'étape** après les 10 premiers entretiens (fiches réelles).
- **Consolidation du registre des décisions et des risques** (A1 à D0), sur autorisation.
