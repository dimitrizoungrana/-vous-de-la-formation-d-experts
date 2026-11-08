# MAQUIS CONTROL — Séance A3
## Phase A · Protocole de démonstration, engagement pilote et grille de sélection des pilotes

> **Statut** : compte rendu de séance de brainstorming, version de travail (v0.1).
> Ce document **ne contient pas** de contrat : il fixe le **contenu minimal** de l'engagement pilote. La rédaction de l'acte (livrable « contrats et conditions générales ») se fera uniquement sur autorisation explicite, puis devra être validée par un juriste local.
> Aucun chiffre de ce document n'est une donnée de marché.

---

## 1. Objectif de la séance

1. Définir le protocole des ~8 démonstrations : public, support, déroulé, mesure.
2. Définir l'annonce du prix et le test des formules d'équipement.
3. Fixer le contenu minimal de l'engagement pilote P2 et des conditions de l'acompte P3.
4. Construire la grille de sélection des 3 pilotes.

## 2. Décisions validées pertinentes

| Décision | Statut |
|---|---|
| Pilote gratuit 30 jours avec engagement écrit (P2), acompte déductible en option (P3) | VALIDÉ |
| **Acompte P3 : remboursé seulement si le pilote échoue du fait de MAQUIS CONTROL (Q7 option b)** | **VALIDÉ (cette séance)** |
| Au moins 2 pilotes sur 3 avec propriétaire absent ≥ 3 soirs/semaine | VALIDÉ |
| Porte 1 : ≥ 8 démos, ≥ 5 propriétaires en N4+ au prix annoncé, 3 pilotes signés couvrant les 3 profils | VALIDÉ |
| Prix de référence : 25 000 FCFA d'installation + 10 000 FCFA/mois d'avance par Mobile Money, grâce de 7 jours | VALIDÉ (hypothèse à tester) |
| Aucun développement ni code sans autorisation | VALIDÉ |

**Points encore ouverts qui touchent cette séance** : Q3 (enquêteurs, langues), Q4 (équipement), Q8 (entité juridique), montant de l'acompte.

---

## 3. Analyse experte : trois tensions à traiter avant de démontrer

### 3.1 On démontre un produit qui n'existe pas encore

Les démos ont lieu en Phase A ; le produit sera développé en Phase E, après les Portes 2 et 3. Montrer des écrans crée une attente.

**Risques**
- Confondre fonctionnalité prévue et fonctionnalité développée (règle de qualité n° 3).
- Promettre implicitement des écrans que la Phase B ou C modifiera.
- Perdre la confiance si le produit livré ne ressemble pas à ce qui a été montré.

**Réponse** : le support est **explicitement présenté comme une maquette**, montre uniquement les parcours du cœur prévu, et la phrase « les écrans peuvent encore changer » fait partie du script.

### 3.2 Le délai entre la signature et le pilote

Un propriétaire qui signe P2 aujourd'hui commencera son pilote dans plusieurs mois (après les Portes 2, 3 et 4). Son engagement va s'éroder : changement de gérant, fermeture, perte d'intérêt.

**Conséquence sur l'acompte P3** : encaisser de l'argent plusieurs mois avant un service sans date ferme est risqué (confiance, conformité, trésorerie à isoler). **C'est un conflit de calendrier avec la décision P3**, signalé ici.

| Option | Description | Avantages | Limites |
|---|---|---|---|
| **T1** | Acompte demandé à la signature P2, en Phase A | Signal N5 immédiat | Argent détenu sans date de service ; remboursements probables si le projet est retardé ou arrêté (No-Go en Porte 2 ou 3) |
| **T2** | Acompte demandé à la **confirmation du pilote**, après la Porte 4 (MVP recetté), avec une date de démarrage ferme | Service daté, risque juridique et de confiance réduit | Pas de signal N5 en Phase A |
| **T3** | Promesse écrite d'acompte en Phase A (montant et conditions acceptés par écrit), versement à la confirmation (T2) | Mesure l'acceptation du principe dès maintenant ; versement au bon moment | Signal intermédiaire (N4 renforcé, pas N5) |

**Recommandation : T3.** La Porte 1 validée n'exige pas de N5 (elle exige N4+ et 3 pilotes signés), donc T3 ne fragilise pas le passage de la Porte 1. Le versement réel devient un critère de la **Porte 5**. → À ARBITRER (Q10).

### 3.3 Le propriétaire absent est aussi absent de la démo

Le segment S3, prioritaire, est le plus difficile à réunir avec son personnel.

**Réponse** : démo en deux parties, dissociables :
- **Partie propriétaire** : au maquis, à son lieu de travail, ou par appel vidéo WhatsApp si nécessaire.
- **Partie personnel** : toujours en présentiel, au maquis, hors pointe.

---

## 4. Support de démonstration

| Option | Description | Avantages | Limites | Coût / complexité |
|---|---|---|---|---|
| **S-a** Scénario papier | Écrans dessinés sur cartes, manipulés à la main | Très rapide, aucun outil | Peu crédible ; ne teste pas l'usage tactile | Très faible |
| **S-b** Maquette cliquable sur téléphone Android | Prototype d'écrans (outil de maquettage type Figma), affiché sur un téléphone d'entrée de gamme | Crédible ; teste le tactile, la taille des boutons, la lisibilité ; **pas de code** | Ne simule ni le hors ligne ni les calculs réels | Moyen (quelques jours de conception UX) |
| **S-c** Vidéo de démonstration | Parcours filmé | Reproductible, utile pour les S3 à distance | Passif : ne teste pas la manipulation par le personnel | Moyen |
| **S-d** Démonstration d'une application existante d'un tiers | Montrer un logiciel de caisse déjà sur le marché | Rien à construire | Teste le produit d'un autre ; confusion ; risque d'éthique commerciale | — **Non recommandé** |

**Recommandation : S-b**, complété par une courte vidéo tirée de la même maquette pour les démos à distance (S-c).
- Afficher la maquette sur un **téléphone Android d'entrée de gamme**, pas sur un ordinateur : c'est la réalité d'usage.
- Personnaliser uniquement les **noms des 10 boissons principales** du prospect (relevés en entretien), pas le reste.
- La production de cette maquette est un travail de conception à autoriser (Q11).

### 4.1 Parcours à maquetter (périmètre minimal)

| # | Parcours | Utilisateur | Hypothèses testées |
|---|---|---|---|
| M1 | Tableau de bord à distance : ventes, encaissements, dépenses, crédits, état de synchronisation | Propriétaire | H10, promesse « à distance » |
| M2 | Clôture : argent attendu / compté, paiements Mobile Money **déclarés / vérifiés**, écart et justification | Propriétaire + gérant | H1, H12, C2, C5 |
| M3 | Prise de commande de 3 boissons + confirmation de remise | Serveur | H7, règle de déstockage |
| M4 | Encaissement espèces puis Mobile Money | Caissier ou serveur | H7, H12 |
| M5 | Transfert réserve → bar (départ + réception) | Gérant / magasinier | Module 4, C6 |
| M6 | Alerte : écart de stock ou annulation sensible à approuver | Propriétaire | Règles d'autorisation |

Hors maquette : paramétrage, gestion fine des droits, inventaire complet, crédits détaillés. Ils sont **mentionnés** dans les limites, pas montrés.

---

## 5. Protocole de démonstration

### 5.1 Qui reçoit une démonstration

- Propriétaires ayant atteint **au moins N2** en entretien (problème prouvé), de préférence N3.
- Couverture des segments : au moins 2 démos S3, 2 S2, 2 S4, 1 S5, et 1 démo libre (dont éventuellement S1, pour tester la frontière).
- Priorité aux candidats possibles des 3 profils pilotes.

### 5.2 Préparation (par prospect)

| Élément | Source |
|---|---|
| Le problème du prospect, **dans ses mots** | Fiche de notation, bloc 2 |
| Ses dépenses actuelles de contrôle | Bloc 3 (H3, H4) |
| Son top 3 des cartes de priorités | Bloc 4 (H11) |
| Ses 10 boissons principales | Bloc 1 |
| Le rôle des participants côté personnel | Bloc 1 |

### 5.3 Déroulé (40 minutes environ)

| Étape | Durée | Contenu | Ce que l'on mesure |
|---|---|---|---|
| **1. Rappel du problème** | 3 min | « La dernière fois, vous m'avez expliqué que… [incident, dans ses mots]. C'est toujours d'actualité ? » | Le problème est-il confirmé, aggravé, oublié ? |
| **2. Avertissement** | 1 min | « Ce que je vais vous montrer est une **maquette** : le logiciel est en préparation, les écrans peuvent encore changer. » | — |
| **3. Partie propriétaire** | 10 min | M1 → M2 → M6, racontés comme une soirée où il est absent : « Il est 23 h, vous êtes chez vous… » | Questions spontanées ; moment où il se penche vers l'écran ; ce qu'il demande à revoir |
| **4. Partie personnel** | 10 min | Donner le téléphone au gérant ou au serveur. Tâches M3, M4, M5 **sans aide**. L'enquêteur se tait. | Réussite seul (oui / avec aide / échec), temps par tâche, erreurs, commentaires |
| **5. Limites** | 2 min | Ce que l'outil ne fera pas au début (ex. : ingrédients des repas non suivis) ; fonctionnement hors ligne présenté comme objectif, pas comme acquis | Réactions aux limites |
| **6. Prix et équipement** | 6 min | Cf. §5.4 | Première réaction mot pour mot, objections |
| **7. Demande d'engagement** | 5 min | Cf. §5.5 | Niveau atteint |
| **8. Clôture** | 3 min | Rappel confidentialité, prochaine étape datée | — |

> **Règle** : le propriétaire et le personnel ne sont pas mis en concurrence. Si le serveur échoue, c'est la maquette qui est en cause : « Merci, ça nous montre ce qu'il faut simplifier. »

### 5.4 Annonce du prix et test de l'équipement

**Script du prix** (énoncé comme un fait, puis silence) :
> « L'installation coûte 25 000 francs. Elle comprend la mise en place et la formation de votre équipe. Ensuite, c'est 10 000 francs par mois, payés d'avance par Mobile Money. L'assistance se fait à distance, par téléphone. »

Puis **se taire** et noter la première réaction mot pour mot.

**Relances, sans négocier**
- « Par rapport à ce que vous dépensez aujourd'hui pour contrôler [rappel du bloc 3], comment vous voyez ce prix ? »
- « Qu'est-ce qui devrait être vrai pour que ce soit un bon prix pour vous ? »
- **Ne jamais** proposer de remise, ni de prix spécial, ni de mois gratuits supplémentaires pendant la Phase A : cela détruirait la mesure de H5.

**Équipement (Q4 encore ouverte → test de préférence, sans prix)**
> « Pour l'appareil, qu'est-ce qui vous arrangerait le mieux : utiliser un téléphone que vous avez déjà, en acheter un adapté, ou qu'il soit fourni avec l'abonnement ? »

On note la préférence et la raison. **Aucun prix d'appareil n'est annoncé** tant que la politique d'équipement n'est pas arbitrée. Les réponses alimentent Q4.

### 5.5 Demande d'engagement (dans l'ordre, arrêt au premier refus)

| Niveau visé | Demande |
|---|---|
| **N4** | « Nous allons choisir trois maquis pour tester gratuitement pendant 30 jours. Voulez-vous être candidat ? Cela demande [obligations P2, §6.1]. Après le test, le prix est celui que je viens de vous donner. » → signature de l'engagement P2 |
| **N4 renforcé (T3)** | Si accepté : présentation des conditions de l'acompte (§6.2) et signature de la promesse d'acompte, **sans versement à ce stade** si T3 est retenu |
| **N4** (alternative) | Si refus du pilote : « Connaissez-vous un autre propriétaire à qui ce serait utile ? Pourriez-vous me le présenter ? » |
| — | Si refus total : « Qu'est-ce qui vous fait hésiter ? » — noter mot pour mot, ne pas argumenter |

### 5.6 Objections : les noter, ne pas les combattre

Catalogue à **compter**, pas à présumer (une ligne par objection, avec citation) :

| Code | Objection type |
|---|---|
| OB-1 | « Mon personnel ne saura pas s'en servir » |
| OB-2 | « C'est trop cher » / « Je dois voir » |
| OB-3 | « Internet ou le courant coupent tout le temps » |
| OB-4 | Crainte sur les données (impôts, fuite, personnel) |
| OB-5 | « Mon cahier me suffit » |
| OB-6 | « Je dois en parler à un associé ou à la famille » |
| OB-7 | « Je n'ai pas de téléphone adapté » |
| OB-8 | Autre |

Réponse autorisée : une question de compréhension (« Qu'est-ce qui vous fait dire ça ? »). Pas de contre-argument pendant la Phase A : l'objectif est de mesurer, pas de convaincre.

### 5.7 Après la démonstration (dans les 24 heures)

- Mettre à jour la fiche de notation (niveau atteint, preuves).
- Remplir la **fiche démo** : réactions au prix (citation), préférence d'équipement, résultats des tâches M3–M5 (réussite, temps, erreurs), objections codées, parcours qui ont suscité le plus de questions.
- Consigner toute demande de fonctionnalité **sans engagement** ; elle sera évaluée plus tard sur sa justification économique.

---

## 6. Engagement pilote : contenu minimal (pas le contrat)

### 6.1 Engagement P2 (pilote gratuit avec engagement écrit)

| Rubrique | Contenu minimal |
|---|---|
| Parties | Structure porteuse de MAQUIS CONTROL ; propriétaire (décideur) ; établissement |
| Objet | Pilote gratuit de 30 jours, **date de démarrage indicative** (fenêtre), confirmée par écrit au moins 2 semaines avant |
| Engagements du propriétaire | Désigner un référent ; permettre l'installation et la formation ; utilisation par le personnel pendant 30 jours ; point hebdomadaire court ; **bilan à J+30 avec décision écrite** (souscrire ou non) |
| Contrôles existants | **Le propriétaire conserve ses contrôles habituels (cahier, comptages) en parallèle pendant le pilote.** Cela limite le risque financier et permet de comparer les résultats |
| Prix après pilote | 25 000 FCFA d'installation + 10 000 FCFA/mois d'avance, Mobile Money, grâce de 7 jours : **écrits et reconnus** |
| Engagements de MAQUIS CONTROL | Installation, formation, assistance à distance ; confidentialité ; **pas d'accès par défaut des administrateurs aux données financières détaillées** ; sauvegardes |
| Données | Propriété du client ; usage anonymisé pour l'évaluation du pilote, avec accord ; restitution ou suppression si non-souscription |
| Équipement pendant le pilote | À préciser selon Q4 |
| Sortie | Chaque partie peut arrêter le pilote ; conséquences sur les données précisées |
| Absence d'obligation d'achat | Explicite : le propriétaire peut ne pas souscrire à J+30 |

### 6.2 Conditions de l'acompte P3 (option b validée)

L'option b n'est applicable que si « l'échec du fait de MAQUIS CONTROL » est défini **objectivement**. Sans définition, chaque non-souscription deviendrait un litige.

| Rubrique | Contenu minimal proposé |
|---|---|
| Montant | Partiel par rapport aux 25 000 FCFA d'installation — **à arbitrer (Q9)** |
| Versement | Mobile Money, **reçu écrit** émis par l'entité porteuse (Q8) ; moment selon Q10 |
| Imputation | Déduit des frais d'installation en cas de souscription |
| **Remboursé intégralement si** | (1) le pilote ne démarre pas avant la date limite fixée dans l'engagement ; (2) une anomalie **critique** (perte de transactions, incohérence financière, fuite de données) n'est pas corrigée dans un délai fixé ; (3) le service est indisponible au-delà d'un seuil fixé ; (4) MAQUIS CONTROL arrête le projet |
| **Conservé si** | Le propriétaire décide de ne pas souscrire pour d'autres raisons, ou ne respecte pas ses engagements P2 (pas de référent, pas d'utilisation) |
| Délai de remboursement | À fixer, court et écrit |
| Traçabilité | Registre des acomptes reçus et remboursés, séparé de la trésorerie d'exploitation |

**Limites** : ces conditions sont une base de travail. Leur conformité (droit de la consommation, nature commerciale du client, encaissement) doit être validée par un juriste local avant tout versement.

---

## 7. Grille de sélection des 3 pilotes

### 7.1 Critères éliminatoires

Un candidat est écarté si **un seul** critère n'est pas rempli :

| # | Critère |
|---|---|
| E1 | Engagement P2 signé par le propriétaire décideur (N4) |
| E2 | Correspond à l'un des 3 profils pilotes |
| E3 | Un référent identifié sur place, qui a participé à la démo |
| E4 | Accepte de garder ses contrôles habituels en parallèle |
| E5 | Établissement stable : pas de fermeture, cession ou conflit d'associés annoncés |
| E6 | Accessible depuis Ouagadougou pour l'installation et les visites d'observation |
| E7 | Pas de lien familial ou amical proche avec le fondateur |
| E8 | Aucune hostilité ouverte du gérant au projet |

### 7.2 Critères pondérés (sur 100)

| Critère | Poids | Ce que l'on note |
|---|---|---|
| Douleur prouvée | 20 | Force des preuves N2 (incident récent, montant, action) |
| Représentativité de la cible commerciale | 20 | Propriétaire absent, nombre de personnes qui manipulent argent et stock |
| Niveau d'engagement | 15 | N4, N4 renforcé (promesse d'acompte), recommandations faites |
| Disponibilité du référent et du propriétaire | 10 | Pour les points hebdomadaires et le bilan J+30 |
| Volume d'activité | 10 | Assez de transactions pour éprouver le système |
| Représentativité des conditions techniques | 10 | **On cherche des conditions réelles, pas faciles** : coupures, réseau faible |
| Résultats de la partie personnel en démo | 10 | Tâches M3–M5 réussies ou presque |
| Potentiel de référence | 5 | Influence auprès d'autres propriétaires |

### 7.3 Contraintes de portefeuille (sur les 3 pilotes ensemble)

| Contrainte | Statut |
|---|---|
| Les 3 profils pilotes couverts (caisse centralisée / serveurs encaisseurs + restauration / multi-emplacements) | VALIDÉ |
| ≥ 2 pilotes avec propriétaire absent ≥ 3 soirs/semaine | VALIDÉ |
| ≥ 1 établissement qui ferme après minuit (C3) | PROPOSÉ |
| ≥ 1 établissement avec coupures fréquentes ou réseau faible (Module 9) | PROPOSÉ |
| ≥ 1 établissement avec paiements Mobile Money fréquents (C5) | PROPOSÉ |
| ≥ 1 établissement qui pratique le crédit client | PROPOSÉ |
| **2 établissements de réserve** classés, pour compenser l'érosion entre la Phase A et la Phase F | PROPOSÉ |

**Règle** : on choisit la combinaison de 3 qui satisfait les contraintes avec le meilleur score total, pas forcément les 3 meilleurs scores individuels.

### 7.4 Reconfirmation

À la Porte 4 (MVP recetté), chaque pilote et chaque réserve est recontacté : confirmation de la date, du référent, et versement de l'acompte si T3 est retenu. Un pilote qui ne reconfirme pas est remplacé par la première réserve compatible avec les contraintes.

---

## 8. Risques et contradictions

| ID | Risque | Classe | Traitement |
|---|---|---|---|
| RA12 | Maquette perçue comme un produit fini | Majeur | Avertissement scripté ; ne montrer que le cœur prévu |
| RA13 | Érosion des engagements entre la Phase A et la Phase F | Majeur | Réserves ; reconfirmation à la Porte 4 ; contact régulier sans sur-promesse |
| RA14 | Acompte encaissé sans date de service | **Majeur** | Option T3 recommandée |
| RA15 | Définition floue de « l'échec du fait de MAQUIS CONTROL » | Majeur | Cas de remboursement objectifs (§6.2) |
| RA16 | Biais de sélection : pilotes trop faciles | Majeur | Contraintes de portefeuille sur les conditions techniques |
| RA17 | Négociation improvisée pendant les démos qui fausse H5 | Majeur | Interdiction de remise en Phase A |
| RA18 | Demandes de fonctionnalités prises pour des engagements | Modéré | Consignées, pas promises ; évaluées sur justification économique |

---

## 9. Recommandation argumentée

1. **Maquette cliquable sur téléphone Android** (6 parcours), présentée comme une maquette, avec une vidéo dérivée pour les propriétaires absents.
2. **Démo en deux parties** : le propriétaire voit la promesse, le personnel manipule seul. Le résultat de la partie personnel est la meilleure preuve disponible avant le pilote pour le risque critique RA2.
3. **Prix énoncé comme un fait, sans négociation**, et équipement testé comme une préférence sans prix.
4. **Calendrier de l'acompte en T3** : promesse écrite en Phase A, versement à la confirmation du pilote. Cela respecte la décision P3/option b et supprime le risque de détenir de l'argent sans date de service.
5. **Sélection en deux temps** : critères éliminatoires, puis score sous contraintes de portefeuille, avec 2 réserves.

**Limites** : une maquette ne prouve ni la faisabilité hors ligne ni la tenue en pointe réelle. Elle mesure la compréhension et l'intention, pas l'usage. L'usage sera mesuré au pilote (Porte 5).

---

## 10. Décisions à prendre

| # | Question | Options | Recommandation |
|---|---|---|---|
| **Q9** | Montant de l'acompte P3 (partiel sur 25 000 FCFA) | Choix libre ; ce n'est pas une donnée de marché | Un montant unique pour tous, assez élevé pour filtrer, sans dépasser la moitié des frais d'installation |
| **Q10** | Moment de l'acompte | T1 à la signature / T2 à la confirmation / **T3** promesse puis versement à la confirmation | **T3** |
| **Q11** | Support de démo : autorisez-vous la conception d'une maquette cliquable (6 parcours, sans code) ? Qui la réalise ? | Oui, en interne / Oui, avec un designer / Non, scénario papier | Oui, maquette cliquable |
| **Q4** | Politique d'équipement | Décision après les démos, sur la base des préférences notées | Différer, tester en démo |
| **Q3** | Enquêteurs, langues, enregistrement | — | Toujours ouverte ; nécessaire avant le premier entretien |
| **Q8** | Entité capable d'encaisser et d'émettre un reçu | — | Toujours ouverte ; **bloquante pour l'acompte**, pas pour P2 |

---

## 11. Registre des décisions (mise à jour séance A3)

| ID | Élément | Statut |
|---|---|---|
| D-A2-10 | Acompte P3 : remboursé seulement si le pilote échoue du fait de MAQUIS CONTROL | **VALIDÉ** (option b) |
| D-A3-01 | Montant de l'acompte | À ARBITRER (Q9) |
| D-A3-02 | Moment de l'acompte (T3 recommandé) | À ARBITRER (Q10) |
| D-A3-03 | Cas objectifs de remboursement et de conservation de l'acompte | PROPOSÉ · validation juridique requise |
| D-A3-04 | Support de démo : maquette cliquable Android, 6 parcours, + vidéo pour démos à distance | À ARBITRER (Q11) |
| D-A3-05 | Démo en deux parties (propriétaire / personnel), 40 min | PROPOSÉ |
| D-A3-06 | Avertissement « maquette » obligatoire dans le script | PROPOSÉ |
| D-A3-07 | Prix énoncé comme un fait, aucune remise en Phase A | PROPOSÉ |
| D-A3-08 | Équipement testé comme préférence, sans prix | PROPOSÉ |
| D-A3-09 | Catalogue d'objections OB-1 à OB-8, comptées et non combattues | PROPOSÉ |
| D-A3-10 | Contenu minimal de l'engagement P2, dont maintien des contrôles existants en parallèle | PROPOSÉ · rédaction sur autorisation, validation juridique |
| D-A3-11 | Grille de sélection : 8 critères éliminatoires + score sur 100 | PROPOSÉ |
| D-A3-12 | Contraintes de portefeuille supplémentaires (après minuit, réseau faible, Mobile Money, crédit) | PROPOSÉ |
| D-A3-13 | 2 établissements de réserve et reconfirmation à la Porte 4 | PROPOSÉ |
| D-A3-14 | Versement effectif de l'acompte comme critère de la Porte 5 | PROPOSÉ (si T3 retenu) |
| D-A1-12 | Politique d'équipement | À ARBITRER après les démos (Q4) |
| D-A2-09 | Enquêteurs, langues, enregistrement | À ARBITRER (Q3) |
| D-A2-11 | Entité juridique capable d'encaisser | À VÉRIFIER (Q8) · BLOQUANT pour l'acompte |
| D-A1-17 | Cadre légal des données personnelles | À VÉRIFIER · BLOQUANT avant le premier entretien |
| D-A1-13 / D-A1-14 | Saisie par le personnel ; hébergement des données | À VÉRIFIER SUR LE TERRAIN · potentiellement BLOQUANTS |

---

## 12. Prochaine étape proposée

La Phase A dispose maintenant de tous ses outils. Deux suites possibles, au choix :

- **Séance A4 — Plan d'exécution de la Phase A** : calendrier sur ~6 semaines, budget plafond du jalon, rôles, rituels hebdomadaires de synthèse, et modèle de synthèse finale pour la décision de la Porte 1.
- **Démarrer la Phase B en parallèle** (contradictions C1 à C8), puisque les entretiens apporteront des faits utiles à C3, C5 et C6. Le chevauchement est justifié tant que la Porte 1 n'est pas contournée.

Recommandation : **A4 d'abord**. Le terrain est le chemin critique, et le budget plafond du jalon n'est pas encore fixé.
