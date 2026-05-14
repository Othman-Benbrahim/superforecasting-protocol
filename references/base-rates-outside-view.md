# Base rates & Outside view — Méthode et sources

L'**outside view** (Kahneman, Lovallo, *Management Science*, 1993) est la pierre angulaire du superforecasting. C'est aussi la plus difficile à appliquer parce qu'elle exige de **résister à la séduction du cas particulier**.

Ce fichier détaille la méthode et fournit des sources opérationnelles.

---

## Le principe : penser comme un statisticien, pas comme un narrateur

Devant un cas spécifique (une élection, un conflit, une fusion), la tentation est de l'analyser en profondeur, d'identifier ses particularités, et de prédire à partir de cette analyse. C'est l'**inside view**.

L'outside view inverse la démarche : *"Mettons de côté les spécificités. Cas comparables historiques : combien de fois ce type d'événement s'est-il produit ?"*

L'évidence empirique (Kahneman, *Thinking, Fast and Slow*, chap. 23-24 ; Tetlock, *Expert Political Judgment*, 2005) montre que l'outside view bat l'inside view en précision dans 60-80% des cas, surtout sur les horizons longs.

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

**Exemples de base rates utiles** :
- Probabilité qu'un État autoritaire devienne démocratique dans une décennie donnée : ~5-8% (V-Dem)
- Probabilité qu'une crise diplomatique s'escalade en conflit armé : ~3-5% (MID)
- Probabilité qu'une élection présidentielle dans un pays démocratique change le parti au pouvoir : ~35-45%

### Économique et financier

| Source | Couverture | Accès |
|--------|-----------|-------|
| **IMF World Economic Outlook** | Croissance, dette, inflation par pays | Libre (imf.org) |
| **World Bank Open Data** | Macro indicators globaux | Libre |
| **OECD historical data** | Stats macro pays OCDE | Libre |
| **BIS (Bank for International Settlements)** | Données bancaires/financières | Libre |
| **NBER recession dataset** | Récessions US datées | Libre |
| **Reinhart-Rogoff database** | Crises financières historiques | Libre |

**Exemples** :
- Probabilité qu'une récession US se produise dans une fenêtre de 24 mois après inversion de la courbe des taux : ~70-80% (sur données 1955-2024)
- Probabilité d'une crise bancaire dans une décennie donnée (post-1970) : ~20-25% (Reinhart-Rogoff)

### M&A et corporate

| Source | Couverture | Accès |
|--------|-----------|-------|
| **Refinitiv (anciennement Thomson Reuters)** | M&A globaux | Payant |
| **Mergermarket** | M&A globaux | Payant |
| **SEC EDGAR** | Filings US publics | Libre (sec.gov) |
| **Compustat (via WRDS)** | Données financières corporates | Académique |

**Exemples** :
- Probabilité qu'une entreprise listée soit acquise sur 5 ans : ~7-10% (varie par secteur)
- Probabilité qu'une fusion annoncée échoue : ~10-15% (par régulation, prix, vote actionnaires)

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

**Exemple** : Time to 100M users pour une nouvelle technologie consumer : ~7-9 ans en médiane historique (variance énorme).

### Plateformes communautaires de forecasting

Sources spécifiques au forecasting où les questions sont déjà décomposées et probabilisées :

- **Metaculus** (metaculus.com) — questions calibrées, base rates souvent explicites
- **Good Judgment Open** (goodjudgment.com) — questions GJP-style
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

L'analyste expert "sait" que son cas est différent. C'est presque toujours faux. Tetlock documente que les *spécialistes* sont les plus mauvais à appliquer l'outside view — leur expertise les attache à l'inside view.

**Contre-mesure** : commencer **toujours** par l'outside view, même quand on a une intuition forte. Si l'inside view diverge fortement, suspecter un biais.

---

## Cas-type : application complète

**Question** : *"Probabilité qu'une crise constitutionnelle majeure (impeachment, dissolution, démission forcée du chef d'État) se produise aux États-Unis d'ici fin 2027 ?"*

### Classe étroite
- Démocraties OCDE depuis 1970
- Cas de crise constitutionnelle majeure par décennie

→ ~3-5 cas pour 8-12 démocraties × 5 décennies = ~50 décennies-démocratie observées, ~5-8 crises → base rate par décennie ~10-15%, soit ~3-5% pour une fenêtre de 24 mois.

### Classe large
- Toutes démocraties post-1945
- Cas de crise comparable

→ base rate similaire (~3-5% sur 24 mois).

### Estimation outside view : ~3-5%

### Inside view (ajustements)

- Polarisation actuelle forte : +2 pts
- Précédents récents (2019-2021) : +3 pts (les chocs récents augmentent la probabilité de réactivation des mécanismes utilisés)
- Stabilité institutionnelle US historique : -2 pts

**Total ajustement** : +3 pts → Estimation finale : ~6-8%

### Comparaison avec marchés

PolyMarket "Trump impeached/removed by 2027" : ~7% en mai 2026 (à vérifier en temps réel).

Convergence : marqueur d'estimation raisonnable.

---

## Quand l'outside view est faible ou indisponible

Pour les questions **uniques** (ex. "L'IA atteindra-t-elle l'AGI d'ici 2030 ?"), il n'y a pas de base rate au sens classique. Dans ce cas :

1. **Décomposer** en sous-questions ayant chacune un cadre comparable.
2. **Construire des classes de référence proxies** : "Cas où une technologie a évolué de X% d'une capacité à Y% en N ans" (graphes loi de Moore, scaling laws).
3. **Documenter l'incertitude profonde** : noter explicitement que l'estimation est davantage une opinion structurée qu'une base rate.

Ne **jamais** prétendre à une base rate quand il n'y en a pas. C'est de la fausse rigueur — pire que pas de rigueur du tout.

---

## Note finale

Maîtriser l'outside view prend des années. Les superforecasters du GJP rapportent que c'est leur compétence la plus longue à acquérir et la plus payante. Investissez le temps. C'est ici que se joue le rendement réel de la discipline prédictive.
