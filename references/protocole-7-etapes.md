# Protocole 7 étapes — Détail opératoire

Ce fichier prolonge le pipeline du SKILL.md avec les détails techniques, les cas-types et les pièges fréquents de chaque étape.

**Statut** : ce pipeline en 7 étapes est une synthèse originale inspirée des travaux du Good Judgment Project, pas un protocole officiel du GJP. Les seuils chiffrés (tests, cadences, alerte à 20 points) sont des conventions internes de ce skill.

---

## Étape 1 — Triage de la question

### Test de forecastabilité (checklist)

Pour qu'une question soit *prévisible* au sens de ce protocole (critères inspirés de la rédaction des questions de tournoi, qui exige des critères de résolution sans ambiguïté), elle doit cocher les 4 cases suivantes :

| Critère | Test |
|---------|------|
| **Horizon défini** | Une date butoir est-elle explicitement nommable ? |
| **Indicateur observable** | À la date butoir, peut-on dire "vrai" ou "faux" sans interprétation ? |
| **Résolveur identifiable** | Qui (quelle autorité, quelle source) tranchera la résolution ? |
| **Base de comparaison** | Existe-t-il au moins quelques cas historiques comparables ? |

Si ≤ 2 cases sont cochées : **refuser la question telle quelle**, demander reformulation.
Si 3 cases sont cochées : **noter "haute incertitude irréductible"**, procéder avec prudence.
Si 4 cases cochées : procéder.

### Types de question et difficulté relative

| Type | Difficulté | Exemple |
|------|-----------|---------|
| **Binaire** | Modérée | *"L'élection X aura-t-elle lieu en 2026 ?"* |
| **Multinomiale** | Élevée | *"Qui remportera l'élection X parmi {A, B, C, autre} ?"* |
| **Continue (intervalle)** | Élevée | *"Combien de sièges le parti X obtiendra-t-il ? ∈ [0-50] / [50-100] / [100+]"* |
| **Conditionnelle** | Très élevée | *"Si X se produit avant T1, P(Y avant T2) = ?"* |

Pour les questions continues, **toujours discrétiser** en 3-5 intervalles avant de procéder.

### Horizon temporel et dégradation prédictive

La précision décroît avec l'horizon. Dans *Expert Political Judgment* (Tetlock, 2005), la précision des experts se rapproche du hasard pour des prédictions à plusieurs années. Les questions du Good Judgment Project portaient pour l'essentiel sur des horizons de quelques mois à environ un an : on dispose de peu de données sur la précision des superforecasters au-delà. (La version 1.0 de ce fichier attribuait à Tetlock & Gardner des seuils précis — 18 mois, 36-48 mois — qui ne sont pas sourcés.)

**Recommandation** : pour les horizons > 12 mois, **décomposer en sous-questions à horizons plus courts** plutôt que prédire directement à l'horizon long.

---

## Étape 2 — Reformulation falsifiable

### Test du tiers ignorant

Critère validant : *"Un observateur tiers, ignorant tout du contexte, lisant uniquement la reformulation à la date butoir, peut-il déterminer sans ambiguïté si la prédiction s'est avérée ?"*

### Exemples de reformulation

| Question floue | Reformulation falsifiable |
|----------------|---------------------------|
| *"Va-t-il y avoir une crise économique en France ?"* | *"D'ici le 31/12/2026, le PIB français connaîtra-t-il deux trimestres consécutifs de croissance négative (source INSEE) ?"* |
| *"L'IA va-t-elle remplacer les développeurs ?"* | *"D'ici le 31/12/2027, le BLS américain rapportera-t-il une baisse > 10% du nombre de developer jobs (source : BLS Occupational Employment Statistics) ?"* |
| *"L'Europe va-t-elle se renforcer militairement ?"* | *"D'ici le 31/12/2026, au moins 12 États membres de l'UE auront-ils dépassé le seuil OTAN de 2% du PIB en dépenses militaires (source : OTAN annual report) ?"* |

### Antipatterns

- **Indicateurs subjectifs** : "la situation se dégrade", "le sentiment public bascule" → reformuler en métrique mesurable.
- **Dates floues** : "à moyen terme", "dans les prochaines années" → exiger une date butoir.
- **Sources non spécifiées** : "selon les experts" → nommer une source autoritative.

---

## Étape 3 — Décomposition Fermi

### Quand décomposer

- Quand la question implique plusieurs étapes conditionnelles.
- Quand l'horizon est long (> 12 mois) — décomposer temporellement.
- Quand l'estimation directe semble "impossible" — c'est précisément le signal qu'il faut décomposer.

### Stratégies de décomposition

#### Décomposition **causale** (chaîne d'événements)

*« P(X acquise dans 18 mois via la voie "difficulté") = P(X en difficulté) × P(acquéreur émerge | difficulté) × P(deal accepté | acquéreur, difficulté) »*

⚠ Le produit est exact **si chaque probabilité est conditionnée à toutes les étapes précédentes**. Multiplier des probabilités non conditionnelles (marginales) n'est valable que si les étapes sont indépendantes ; en cas de corrélation positive, ce produit sous-estime.
⚠ Le produit ne couvre **qu'une voie**. S'il existe d'autres voies (acquisition sans difficulté financière), il faut les ajouter (décomposition par cas).

#### Décomposition **temporelle** (étapes dans le temps)

*« P(crise dans 24 mois) = 1 − Π (1 − hₜ) »*, où hₜ = P(crise au semestre t | pas de crise avant).

Équivalent : P(S1) + P(pas S1) × h₂ + P(pas S1, pas S2) × h₃ + … — chaque risque conditionnel est **pondéré par la probabilité d'arriver jusqu'à cette période**. Additionner directement les hₜ surestime le cumul (et peut dépasser 1). La version 1.0 de ce fichier contenait cette erreur.

#### Décomposition **par cas** (couverture exhaustive)

*« P(événement) = P(via voie A) + P(via voie B) + P(via voie C) »* — valable si les voies sont **mutuellement exclusives** ; sinon, retrancher les intersections.

### Limite : décomposition excessive

Au-delà de 4-5 sous-questions, la décomposition risque d'introduire plus d'erreur qu'elle n'en réduit (heuristique) : chaque sous-estimation a sa propre marge d'erreur, et les marges se propagent.

**Règle** : décomposer jusqu'à ce que chaque sous-question soit *clairement plus facile à estimer* que le tout, mais pas davantage.

---

## Étape 4 — Base rate (outside view)

### Sources de base rates par domaine

| Domaine | Sources |
|---------|---------|
| **Géopolitique** | UCDP/PRIO Armed Conflict Dataset, Polity IV, Freedom House |
| **Économique** | IMF World Economic Outlook, OECD historical data, BIS |
| **Élections** | ParlGov, IFES ElectionGuide, CLEA |
| **Marchés** | CRSP, Compustat, Bloomberg historicals |
| **M&A** | Refinitiv, Mergermarket, S&P Capital IQ |
| **Tech adoption** | Gartner, Pew Research tech surveys |
| **Maladies/épidémies** | OMS, ECDC, CDC historiques |
| **Catastrophes** | EM-DAT, NOAA, Munich Re NatCat |

Pour des questions plus inhabituelles : Google Scholar avec « base rate of X », et les questions résolues des plateformes publiques de prévision (Metaculus, Good Judgment Open), qui renseignent sur des classes de questions comparables — ce ne sont pas des taux de base au sens strict.

### Choisir la bonne classe de référence

Le piège : **trop spécifique** = pas assez de cas (échantillon trop petit) ; **trop large** = peu pertinent.

**Méthode pyramidale** :

1. Définir une classe étroite (mais réaliste).
2. Calculer base rate étroite.
3. Définir une classe large.
4. Calculer base rate large.
5. Choisir une estimation entre les deux, plus proche de la classe étroite si l'échantillon le permet.

**Exemple** : *"Cette startup va-t-elle atteindre 100M$ ARR dans 5 ans ?"*

*(Chiffres fictifs, pour illustrer la méthode.)*
- Classe étroite : startups SaaS B2B ayant levé une série B à une date comparable, secteur X → ~12 cas → taux ~17 % (2 cas sur 12 : très instable)
- Classe large : toutes les startups ayant levé une série B → ~800 cas → taux ~4 %
- Estimation : entre 4 % et 17 %, plus proche de la classe large tant que la classe étroite compte si peu de cas.

### Mise en garde : « this time is different »

Reinhart & Rogoff (*This Time Is Different: Eight Centuries of Financial Folly*, 2009) montrent, sur huit siècles de données, que les crises financières reviennent de façon récurrente et que la conviction « cette fois, c'est différent » précède souvent les crises. Leur thèse est **qualitative** : l'ouvrage ne fournit pas de pourcentage du type « faux X % du temps ». (La version 1.0 de ce fichier lui attribuait une statistique de 80 %, introuvable.)

Quand un acteur dit « this time is different », c'est un signal pour **maintenir** le poids du taux de base et exiger des raisons spécifiques, pas pour l'abandonner.

---

## Étape 5 — Inside view (ajustements disciplinés)

### Seuil d'alerte des 20 points (convention interne)

Ce seuil est une **heuristique propre à ce protocole**. Il ne provient pas de Tetlock : les Dix commandements recommandent de trouver le bon équilibre entre vue intérieure et vue extérieure, sans seuil chiffré. Il s'appuie sur un constat général (la vue intérieure tend à être surpondérée ; Kahneman & Lovallo, 1993) et sert de point de contrôle, pas d'interdiction.

**Discipline** : si votre ajustement total dépasse 20 points, **arrêter** et :
1. Redécomposer la question (étape 3) pour identifier ce qui est sous-estimé.
2. Vérifier si la classe de référence (étape 4) était bien choisie.
3. Tester avec une seconde classe.

### Facteurs typiques d'ajustement

*Magnitudes indicatives, convention interne non issue d'une étude :*

| Facteur | Direction typique | Magnitude |
|---------|-------------------|-----------|
| Contexte structurellement comparable à un précédent récent | ↑ ou ↓ | ±10 pts |
| Signal d'engagement irréversible des acteurs principaux | ↑ | ±5 pts |
| Absence d'incitations pour réaliser le scénario | ↓ | ±10 pts |
| Conjoncture économique défavorable | ↓ (pour beaucoup) | ±5-10 pts |
| Pression réglementaire/politique active | dépend | ±5-15 pts |

Ne **jamais** ajuster pour : « j'ai un bon feeling », « tout le monde le dit », « c'est l'évidence ». Ce ne sont pas des facteurs — ce sont des biais.

---

## Étape 6 — Scénarios MECE

### Construire un set MECE

#### Stratégie binaire (le plus simple)

Question : *"X va-t-il se produire d'ici T ?"*
- S1 = X se produit (P)
- S2 = X ne se produit pas (1-P)

Trivialement MECE.

#### Stratégie multinomiale par voie

Question : *"Comment X va-t-il se résoudre d'ici T ?"*
- S1 = Résolution par voie A
- S2 = Résolution par voie B
- S3 = Résolution par voie C
- S4 = Pas de résolution avant T

À vérifier : les voies A, B, C sont-elles exclusives ? Si oui → MECE. Sinon → reformuler.

#### Stratégie par intensité (à éviter)

❌ S1 = légère détérioration, S2 = détérioration modérée, S3 = détérioration sévère.

Ce n'est pas exhaustif — il manque l'amélioration et la stabilité. Si vous voulez probabiliser l'intensité, faites de l'intensité la question principale et couvrez toute l'échelle (y compris « pas de détérioration »).

### Probabilités granulaires

Choisir un nombre explicite : pas de « 30 % ou 35 %, je ne sais pas trop ».

**Ce que dit la recherche** : dans les données du GJP, arrondir les prévisions à des catégories plus grossières (par exemple les expressions verbales d'incertitude) dégrade systématiquement la précision ; les meilleurs prévisionnistes distinguent en moyenne une dizaine de niveaux de probabilité ou davantage (Friedman et al., 2018). Les prévisionnistes y utilisent spontanément beaucoup de multiples de 10 % et de 5 %, mais rien ne montre qu'un pas de 5 % soit un optimum.

**Règle pratique du skill** : des pas de 5 % conviennent dans la zone 10-90 % ; en dessous de 10 % et au-dessus de 90 %, utiliser des pas plus fins (1 %, 2 %, 3 %, 5 %, 7 % ; 93 %, 95 %, 97 %, 98 %, 99 %), car un facteur 2 entre 1 % et 2 % est une différence importante. Une précision plus fine est admise si l'analyse la justifie.

---

## Étape 7 — Indicateurs et cadence

### Qualité des indicateurs

Un bon indicateur est :
- **observable publiquement** (pas besoin d'accès privilégié)
- **précédent dans le temps** (apparaît avant la résolution)
- **discriminant** (corrélé à un scénario, pas neutre)
- **non-ambigu** (pas d'interprétation requise)

**Test (convention interne)** : si l'indicateur apparaît, la probabilité du scénario auquel il est associé devrait bouger d'au moins 10 points (en termes bayésiens, son BF doit être nettement différent de 1). Sinon, ce n'est pas un indicateur discriminant.

### Cadence de révision

*Convention interne :*

| Horizon prédiction | Cadence recommandée |
|--------------------|---------------------|
| 1-3 mois | Hebdomadaire ou bi-hebdomadaire |
| 3-12 mois | Mensuelle |
| 12-24 mois | Bimensuelle ou trimestrielle |
| 24-36 mois | Trimestrielle |

À chaque révision : invoquer `bayesian-updater` avec les nouvelles informations disponibles depuis la dernière révision.

---

## Notes finales

Le protocole est **coûteux** : une fiche complète demande un travail de recherche réel (classe de référence, sources), de l'ordre de plusieurs dizaines de minutes pour un analyste exercé. Le rendement n'apparaît qu'à l'échelle : il faut un nombre suffisant de prédictions scorées (au moins 30 pour une lecture de calibration, voir `calibration-engine`) pour que l'analyste apprenne ses propres patterns de biais.

---

## Références

- Friedman, J. A., Baker, J. D., Mellers, B. A., Tetlock, P. E., & Zeckhauser, R. (2018). The value of precision in probability assessment. *International Studies Quarterly*, 62(2), 410-422.
- Kahneman, D., & Lovallo, D. (1993). Timid choices and bold forecasts. *Management Science*, 39(1), 17-31.
- Reinhart, C. M., & Rogoff, K. S. (2009). *This Time Is Different: Eight Centuries of Financial Folly*. Princeton University Press.
- Tetlock, P. E. (2005). *Expert Political Judgment*. Princeton University Press.
- Tetlock, P. E., & Gardner, D. (2015). *Superforecasting*. Crown.
