# Base rates & Outside view — Méthode et sources

L'**outside view** (Kahneman & Lovallo, *Management Science*, 1993) est l'un des piliers de la prévision disciplinée (commandement 3 de Tetlock : équilibrer vue intérieure et vue extérieure). C'est aussi la plus difficile à appliquer parce qu'elle exige de **résister à la séduction du cas particulier**.

Ce fichier détaille la méthode et fournit des sources opérationnelles.

---

## Le principe : penser comme un statisticien, pas comme un narrateur

Devant un cas spécifique (une élection, un conflit, une fusion), la tentation est de l'analyser en profondeur, d'identifier ses particularités, et de prédire à partir de cette analyse. C'est l'**inside view**.

L'outside view inverse la démarche : *"Mettons de côté les spécificités. Cas comparables historiques : combien de fois ce type d'événement s'est-il produit ?"*

Les travaux sur la planification et la prévision documentent un biais systématique en faveur de la vue intérieure, qui conduit à des prévisions trop optimistes (Kahneman & Lovallo, 1993 ; Kahneman, *Thinking, Fast and Slow*, 2011, chap. 23), et la méthode de la classe de référence améliore la prévision des coûts et délais de projets (Flyvbjerg, 2006). Il n'existe pas, à notre connaissance, de chiffre général du type « l'outside view gagne dans X % des cas » ; la version 1.0 de ce fichier annonçait « 60-80 % », sans source.

---

## Étapes de l'outside view

### 1. Définir la classe de référence

C'est l'étape **la plus contestable**. Une mauvaise classe de référence rend tout le reste invalide.

**Critères de bonne classe** :

- Suffisamment **large** pour avoir un échantillon statistique (≥ 20 cas idéalement)
- Suffisamment **étroite** pour rester pertinente pour le cas présent
- **Bien documentée** (données accessibles)
- **Non-tautologique** (la classe ne préjuge pas du résultat)

### 2. Récolter les données

Sources par domaine ci-dessous.

### 3. Calculer la fréquence

Base rate = (cas où le scénario s'est produit) / (cas totaux dans la classe)

### 4. Documenter la classe et les sources

Cette étape est cruciale pour la **scoreabilité** : à la résolution, on doit pouvoir auditer si la base rate était bien choisie.

### 5. Tester une classe alternative

Toujours faire l'exercice avec une **seconde** classe de référence (plus étroite ou plus large) pour voir la sensibilité de l'estimation.

---

## Sources de base rates par domaine

### Géopolitique et conflits

| Source | Couverture | Accès |
|--------|-----------|-------|
| **UCDP/PRIO Armed Conflict Dataset** | Conflits armés depuis 1946 | Libre (ucdp.uu.se) |
| **Polity IV / V Project** | Régimes politiques, transitions démocratiques | Libre (systemicpeace.org) |
| **Freedom House** | Indices de liberté politique | Libre (freedomhouse.org) |
| **V-Dem (Varieties of Democracy)** | Démocratie multi-dimensionnelle | Libre (v-dem.net) |
| **Correlates of War** | Guerres, alliances, capacités | Libre (correlatesofwar.org) |
| **MID dataset (Militarized Interstate Disputes)** | Disputes inter-étatiques | Libre |

**Ordres de grandeur à recalculer avant usage** — les valeurs de la version 1.0 n'étaient accompagnées ni de fenêtre temporelle, ni de définition opérationnelle, ni de calcul reproductible. Elles sont retirées. Pour chaque cas, voici comment établir le taux de base :
- *Transition d'un régime autoritaire vers la démocratie sur 10 ans* : V-Dem (indice de démocratie électorale) ou Polity V, avec un seuil de classification et une fenêtre explicites.
- *Escalade d'une crise interétatique en conflit armé* : jeu MID (Correlates of War) pour les niveaux d'hostilité, UCDP pour les conflits armés ; définir « crise » et « conflit » avant de compter.
- *Alternance au pouvoir lors d'une élection présidentielle* : ParlGov ou CLEA, en précisant le périmètre (démocraties retenues, période).

### Économique et financier

| Source | Couverture | Accès |
|--------|-----------|-------|
| **IMF World Economic Outlook** | Croissance, dette, inflation par pays | Libre (imf.org) |
| **World Bank Open Data** | Macro indicators globaux | Libre |
| **OECD historical data** | Stats macro pays OCDE | Libre |
| **BIS (Bank for International Settlements)** | Données bancaires/financières | Libre |
| **NBER recession dataset** | Récessions US datées | Libre |
| **Reinhart-Rogoff database** | Crises financières historiques | Libre |

**Exemples (à recalculer sur la source avant usage)** :
- *Récession américaine après inversion de la courbe des taux* : historiquement, la plupart des récessions américaines depuis les années 1960 ont été précédées d'une inversion de l'écart 10 ans – 3 mois, et la Fed de New York publie un modèle de probabilité fondé sur cet écart. Mais l'échantillon est petit (moins d'une dizaine d'épisodes) et **l'inversion de 2022-2024 n'a pas été suivie d'une récession datée** : à la date de cette révision, le NBER n'a daté aucun pic conjoncturel postérieur à février 2020. Le taux de 70-80 % annoncé dans la version 1.0 n'était pas sourcé et surestime la fiabilité du signal ; utiliser le modèle de la Fed de New York et la chronologie du NBER, avec un intervalle large.
- *Crise bancaire systémique sur une décennie* : base de données de Reinhart & Rogoff ou de Laeven & Valencia (FMI) ; préciser l'échantillon de pays et la période.

### M&A et corporate

| Source | Couverture | Accès |
|--------|-----------|-------|
| **Refinitiv (anciennement Thomson Reuters)** | M&A globaux | Payant |
| **Mergermarket** | M&A globaux | Payant |
| **SEC EDGAR** | Filings US publics | Libre (sec.gov) |
| **Compustat (via WRDS)** | Données financières corporates | Académique |

**Exemples (ordres de grandeur non sourcés dans la version 1.0, à établir sur les bases ci-dessus)** :
- *Entreprise cotée acquise sur un horizon donné* : très variable selon le secteur, la taille et la période ; calculer sur la base (ex. SEC EDGAR ou Compustat via WRDS) pour la classe pertinente.
- *Opération annoncée non finalisée* : à mesurer sur les opérations annoncées d'une période et d'une zone données (Refinitiv, Mergermarket), en distinguant les causes (régulation, prix, vote).

### Élections et politique

| Source | Couverture | Accès |
|--------|-----------|-------|
| **ParlGov** | Élections, partis, gouvernements démocratiques | Libre |
| **IFES Election Guide** | Calendrier mondial des élections | Libre |
| **CLEA (Constituency-Level Elections Archive)** | Résultats électoraux détaillés | Libre |
| **Comparative Political Data Set** | Politiques publiques | Libre |

### Technologie et adoption

| Source | Couverture | Accès |
|--------|-----------|-------|
| **Gartner Hype Cycle** (rétrospectif) | Trajectoires d'adoption tech | Payant |
| **Pew Research Internet/Tech** | Adoption tech par publics | Libre |
| **Our World in Data — Technology** | Séries historiques d'adoption | Libre |

**Exemple** : le délai d'adoption d'une technologie grand public varie de quelques mois à plusieurs décennies selon l'époque et le type de produit (séries d'Our World in Data) ; aucune médiane unique n'a de sens sans définir la classe. (La version 1.0 citait « ~7-9 ans », sans source.)

### Plateformes communautaires de forecasting

Sources spécifiques au forecasting où les questions sont déjà décomposées et probabilisées :

- **Metaculus** (metaculus.com) — questions calibrées, base rates souvent explicites
- **Good Judgment Open** (gjopen.com) — questions dans le style du GJP
- **PolyMarket** / **Manifold Markets** — prediction markets (avec biais de marché)
- **Kalshi** — prediction markets régulés

Ces plateformes ne sont pas des sources de base rates en soi, mais elles **agrègent l'expertise** sur des questions précises et permettent de comparer ses estimations à celles d'un consensus de forecasters.

---

## Pièges de l'outside view

### Piège 1 : Classe de référence biaisée par recherche

On cherche dans la mémoire les cas qui ressemblent à notre intuition, pas les cas réellement similaires (biais de disponibilité, Tversky & Kahneman, 1973).

**Contre-mesure** : forcer une définition opérationnelle de la classe **avant** de chercher les cas, pas après.

### Piège 2 : Échantillon trop petit

Une classe de 5 cas donne une base rate quasi-aléatoire. L'erreur standard est trop grande.

**Contre-mesure** : si la classe étroite a < 20 cas, élargir et accepter une estimation moins précise mais plus robuste.

### Piège 3 : Survivor bias dans les données

Les cas "morts" (entreprises faillies, mouvements disparus) sont sous-représentés dans les bases de données.

**Contre-mesure** : vérifier explicitement la couverture des cas négatifs.

### Piège 4 : Régime change

Les base rates calculées sur des données pré-2008 (par exemple) peuvent ne plus s'appliquer après un changement structurel.

**Contre-mesure** : limiter la fenêtre temporelle aux régimes comparables au présent.

### Piège 5 : Refus de l'outside view

L'analyste expert « sait » que son cas est différent. C'est souvent faux. Dans *Expert Political Judgment*, Tetlock observe que la spécialisation n'améliore guère la précision au-delà d'un niveau de culture générale, et que les experts au style de pensée « hérisson » (une grande idée appliquée partout) sont les moins précis.

**Contre-mesure** : commencer **toujours** par l'outside view, même quand on a une intuition forte. Si l'inside view diverge fortement, suspecter un biais.

---

## Cas-type : la mécanique d'une estimation (chiffres fictifs)

*Ce cas illustre la méthode ; les effectifs sont fictifs et doivent être remplacés par un comptage réel sur une source documentée. La version 1.0 présentait des effectifs contradictoires, une conversion décennie → 24 mois erronée et une cote de marché datée invérifiable.*

**Question** : *« Probabilité qu'un événement institutionnel majeur défini à l'avance (ex. : départ anticipé du chef de l'État, quelle qu'en soit la cause) survienne dans le pays P d'ici 24 mois ? »*

### 1. Définir la classe et l'événement avant de compter
- Classe étroite : démocraties de l'OCDE, 1970-2025, unité d'observation = pays-année.
- Événement : défini par un critère vérifiable (ex. fin de mandat avant le terme constitutionnel).

### 2. Compter (valeurs fictives)
- 10 pays × 55 ans = 550 pays-années ; 11 événements → taux annuel ≈ 11/550 = **2 %**.

### 3. Convertir à l'horizon de la question
- Sur 24 mois : 1 − (1 − 0.02)² ≈ **4 %** (et non 2 × 2 % par simple addition — l'écart est faible ici, mais grandit avec le taux et l'horizon).
- Si l'on part d'un taux par décennie (ex. 10 %) : taux annuel = 1 − 0.90^(1/10) ≈ 1.05 %, donc sur 24 mois ≈ 2.1 %, et non « 10 % ÷ 5 ».

### 4. Classe alternative
- Toutes démocraties depuis 1945 : recompter. Si le taux diffère fortement, retenir une valeur intermédiaire et le noter.

### 5. Ajustements (inside view)
- Lister les facteurs spécifiques au pays P et à la période, chacun avec son sens et sa magnitude, et vérifier le seuil d'alerte interne de 20 points.

### 6. Comparaison avec des agrégats externes
- Une cote de marché prédictif ou une prévision agrégée (Metaculus, Good Judgment Open) peut servir de **point de comparaison**, consultée à la date de l'estimation et citée avec cette date. Une convergence n'est pas une validation : les marchés ont leurs propres biais (liquidité, biais de favori-outsider).

---

## Quand l'outside view est faible ou indisponible

Pour les questions **uniques** (ex. "L'IA atteindra-t-elle l'AGI d'ici 2030 ?"), il n'y a pas de base rate au sens classique. Dans ce cas :

1. **Décomposer** en sous-questions ayant chacune un cadre comparable.
2. **Construire des classes de référence proxies** : "Cas où une technologie a évolué de X% d'une capacité à Y% en N ans" (graphes loi de Moore, scaling laws).
3. **Documenter l'incertitude profonde** : noter explicitement que l'estimation est davantage une opinion structurée qu'une base rate.

Ne **jamais** prétendre à une base rate quand il n'y en a pas. C'est de la fausse rigueur — pire que pas de rigueur du tout.

---

## Note finale

Maîtriser l'outside view demande de la pratique : définir une classe avant de chercher, trouver la donnée, la convertir correctement à l'horizon, puis résister à la tentation de l'abandonner. C'est une compétence qui se travaille et se vérifie au scoring (`calibration-engine`).

---

## Références

- Flyvbjerg, B. (2006). From Nobel Prize to project management: Getting risks right. *Project Management Journal*, 37(3), 5-15.
- Kahneman, D., & Lovallo, D. (1993). Timid choices and bold forecasts. *Management Science*, 39(1), 17-31.
- Kahneman, D. (2011). *Thinking, Fast and Slow*, chap. 23. Farrar, Straus and Giroux.
- Reinhart, C. M., & Rogoff, K. S. (2009). *This Time Is Different*. Princeton University Press.
- Tetlock, P. E. (2005). *Expert Political Judgment*. Princeton University Press.
- Federal Reserve Bank of New York — The Yield Curve as a Leading Indicator : https://www.newyorkfed.org/research/capital_markets/ycfaq
- NBER — Business Cycle Dating : https://www.nber.org/research/business-cycle-dating
