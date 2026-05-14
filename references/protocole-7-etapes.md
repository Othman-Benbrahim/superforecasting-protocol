# Protocole 7 étapes — Détail opératoire

Ce fichier prolonge le pipeline du SKILL.md avec les détails techniques, les cas-types et les pièges fréquents de chaque étape.

---

## Étape 1 — Triage de la question

### Test de forecastabilité (checklist)

Pour qu'une question soit *forecastable* selon les critères du Good Judgment Project, elle doit cocher les 4 cases suivantes :

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

Tetlock & Gardner (2015) documentent que la précision des forecasters se dégrade fortement au-delà de 18 mois et devient à peine meilleure que le hasard au-delà de 36-48 mois (selon les domaines).

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

*"P(X est acquise dans 18 mois) = P(X en difficulté) × P(acquéreur émerge | difficulté) × P(deal accepté | acquéreur)"*

⚠ Si les sous-événements sont **indépendants**, multiplier directement.
⚠ S'ils sont **corrélés**, ajuster (l'estimation directe peut être supérieure au produit).

#### Décomposition **temporelle** (étapes dans le temps)

*"P(crise dans 24 mois) = P(crise dans premier semestre) + P(crise dans deuxième semestre | pas dans premier) + ..."*

#### Décomposition **par cas** (couverture exhaustive)

*"P(événement) = P(via voie A) + P(via voie B) + P(via voie C)"*

### Limite : décomposition excessive

Au-delà de 4-5 sous-questions, la décomposition introduit plus d'erreur qu'elle n'en réduit. Chaque sous-estimation a sa propre marge d'erreur, et les marges se propagent.

**Règle** : décomposer jusqu'à ce que chaque sous-question soit *clairement plus facile à estimer* que le tout, mais pas davantage.

---

## Étape 4 — Base rate (outside view)

### Sources de base rates par domaine

| Domaine | Sources |
|---------|---------|
| **Géopolitique** | UCDP/PRIO Armed Conflict Dataset, Polity IV, Freedom House |
| **Économique** | IMF World Economic Outlook, OECD historical data, BIS |
| **Élections** | EUNDS election database, ParlGov, IFES |
| **Marchés** | CRSP, Compustat, Bloomberg historicals |
| **M&A** | Refinitiv, Mergermarket, S&P Capital IQ |
| **Tech adoption** | Gartner, Pew Research tech surveys |
| **Maladies/épidémies** | OMS, ECDC, CDC historiques |
| **Catastrophes** | EM-DAT, NOAA, Munich Re NatCat |

Pour des questions plus exotiques : Google Scholar avec "base rate of X" + recherche sur Metaculus (plateforme publique de forecasting où les bases rates sont souvent estimées).

### Choisir la bonne classe de référence

Le piège : **trop spécifique** = pas assez de cas (échantillon trop petit) ; **trop large** = peu pertinent.

**Méthode pyramidale** :

1. Définir une classe étroite (mais réaliste).
2. Calculer base rate étroite.
3. Définir une classe large.
4. Calculer base rate large.
5. Choisir une estimation entre les deux, plus proche de la classe étroite si l'échantillon le permet.

**Exemple** : *"Cette startup va-t-elle atteindre 100M$ ARR dans 5 ans ?"*

- Classe étroite : startups SaaS B2B, séries B levées en 2024, secteur X → ~12 cas → base rate ~17%
- Classe large : toute startup ayant levé en série B en 2024 → ~800 cas → base rate ~4%
- Estimation : entre 4% et 17%, probablement vers 8-12% selon facteurs spécifiques.

### Mise en garde : "this time is different"

L'idée que le cas présent est qualitativement différent du tableau historique est **statistiquement fausse 80% du temps** (Reinhart & Rogoff, *This Time Is Different*, 2009). C'est le biais inside view dans toute sa force.

Quand un acteur dit "this time is different", c'est un signal pour **augmenter** le poids de la base rate, pas le diminuer.

---

## Étape 5 — Inside view (ajustements disciplinés)

### Règle des 20 points

Tetlock observe que les ajustements inside view qui déplacent la probabilité de plus de 20 points par rapport à la base rate sont **systématiquement biaisés** vers le scénario narratif séduisant.

**Discipline** : si votre ajustement total dépasse 20 points, **arrêter** et :
1. Redécomposer la question (étape 3) pour identifier ce qui est sous-estimé.
2. Vérifier si la classe de référence (étape 4) était bien choisie.
3. Tester avec une seconde classe.

### Facteurs typiques d'ajustement

| Facteur | Direction typique | Magnitude |
|---------|-------------------|-----------|
| Contexte structurellement comparable à un précédent récent | ↑ ou ↓ | ±10 pts |
| Signal d'engagement irréversible des acteurs principaux | ↑ | ±5 pts |
| Absence d'incitations pour réaliser le scénario | ↓ | ±10 pts |
| Conjoncture économique défavorable | ↓ (pour beaucoup) | ±5-10 pts |
| Pression réglementaire/politique active | dépend | ±5-15 pts |

Ne **jamais** ajuster pour : "j'ai un bon feeling", "tout le monde le dit", "c'est l'évidence". Ces ne sont pas des facteurs — ce sont des biais.

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

Ce n'est pas MECE — c'est une seule prédiction (détérioration) sur trois niveaux d'intensité. Si vous voulez probabiliser l'intensité, faites de l'intensité la question principale.

### Probabilités granulaires

Les forecasters disciplinés du GJP utilisent des incréments de 5%. Pas de "30% ou 35%, je ne sais pas trop" — choisir 30% ou 35% explicitement.

**Pourquoi** : la calibration empirique montre que les incréments de 5% capturent l'essentiel de la discrimination utile. En dessous (incréments de 1%) = fausse précision. Au-dessus (incréments de 25%) = perte d'information.

Exception : pour les événements à très basse probabilité (< 5%), utiliser des incréments de 1% (1%, 2%, 3%, 5%, 7%, 10%).

---

## Étape 7 — Indicateurs et cadence

### Qualité des indicateurs

Un bon indicateur est :
- **observable publiquement** (pas besoin d'accès privilégié)
- **précédent dans le temps** (apparaît avant la résolution)
- **discriminant** (corrélé à un scénario, pas neutre)
- **non-ambigu** (pas d'interprétation requise)

**Test** : si l'indicateur apparaît, la probabilité du scénario auquel il est associé doit augmenter d'au moins 10 points. Sinon, ce n'est pas un bon indicateur.

### Cadence de révision

| Horizon prédiction | Cadence recommandée |
|--------------------|---------------------|
| 1-3 mois | Hebdomadaire ou bi-hebdomadaire |
| 3-12 mois | Mensuelle |
| 12-24 mois | Bimensuelle ou trimestrielle |
| 24-36 mois | Trimestrielle |

À chaque révision : invoquer `bayesian-updater` avec les nouvelles informations disponibles depuis la dernière révision.

---

## Notes finales

Le protocole est **coûteux**. Une fiche complète prend 30-60 minutes pour un analyste exercé, et davantage pour un débutant. C'est précisément ce coût qui distingue la discipline prédictive de l'opinion. Le rendement n'apparaît qu'à l'échelle : sur 50-100 prédictions disciplinées avec scoring, l'analyste apprend ses propres patterns de biais et s'améliore. C'est le rôle du `calibration-engine`.
