# Décomposition Fermi — Casser le complexe en tractable

> *« Combien d'accordeurs de piano y a-t-il à Chicago ? »* — question traditionnellement attribuée à Enrico Fermi (l'attribution est d'origine anecdotique), devenue l'exemple type de la méthode.

La décomposition à la Fermi est l'art de transformer une question apparemment impossible à estimer en une suite de sous-questions individuellement plus faciles. C'est l'une des pratiques que Tetlock & Gardner (2015) associent aux meilleurs prévisionnistes (commandement 2 : décomposer les problèmes apparemment insolubles).

---

## Le principe

Face à une question dont l'estimation directe semble « impossible », on la **casse** en composantes mesurables ou estimables. Chaque sous-estimation a sa marge d'erreur ; si ces erreurs sont **indépendantes** et **sans biais systématique**, elles se compensent en partie (en échelle logarithmique, les erreurs s'additionnent en variance et non en valeur absolue). C'est une propriété statistique utile, pas une garantie : une erreur systématique commune ne se compense pas.

C'est exactement ce que fait un physicien estimant un ordre de grandeur sans calcul exact.

---

## Stratégies de décomposition

### 1. Décomposition causale (chaîne d'événements conditionnels)

Pour un événement complexe = série d'étapes :

$$P(\text{voie}) = P(E_1) \times P(E_2 | E_1) \times P(E_3 | E_1, E_2) \times ...$$

Chaque terme est conditionné à **toutes** les étapes précédentes. Ce produit donne la probabilité d'**une** voie ; s'il en existe d'autres, il faut les ajouter (stratégie 3).

**Exemple** : *"L'entreprise X va-t-elle être acquise dans les 18 mois ?"*

| Sous-événement | Probabilité estimée |
|----------------|---------------------|
| P(X présente des signes de vulnérabilité financière d'ici 18 mois) | 0.40 |
| P(un acquéreur crédible se positionne | vulnérabilité) | 0.50 |
| P(les négociations aboutissent | acquéreur positionné) | 0.60 |
| P(la régulation antitrust autorise | accord signé) | 0.80 |
| P(les actionnaires acceptent | régulation OK) | 0.85 |

Probabilité de cette voie = 0.40 × 0.50 × 0.60 × 0.80 × 0.85 ≈ **0.082** (~8 %)

⚠ **Conditionnement** : le produit n'est exact que si chaque probabilité est estimée **sachant** les étapes précédentes (ex. la probabilité que les actionnaires acceptent *sachant* que l'entreprise est vulnérable, ce qui la relève). Multiplier des probabilités estimées isolément revient à supposer l'indépendance ; en cas de corrélation positive, cela sous-estime.

⚠ **Voies omises** : une entreprise peut être acquise sans être en difficulté. 8 % est la probabilité de la voie « vulnérabilité », pas celle de l'acquisition. La probabilité totale est la somme des voies exclusives.

### 2. Décomposition temporelle

Pour une probabilité cumulée sur une période, on combine les **risques conditionnels** par sous-période hₜ = P(événement en t | pas avant) :

$$P(\text{événement avant T}) = 1 - \prod_{t=1}^{T} (1 - h_t)$$

⚠ **Correction v1.0** : la version précédente présentait ce cumul comme la **somme** des hₜ, ce qui est faux. La somme surestime toujours (dès que deux risques sont non nuls) et peut dépasser 1. Elle n'est une approximation acceptable que si tous les hₜ sont très petits.

**Exemple** : *"Probabilité d'une crise économique en France d'ici 24 mois ?"*

Décomposer par trimestre (valeurs illustratives) :
- h₁ = P(crise au trimestre 1) = 0.05
- h₂ = P(crise au trimestre 2 | pas au trimestre 1) = 0.06
- h₃ = P(crise au trimestre 3 | pas avant) = 0.07
- … (8 trimestres au total)

Sur les trois premiers trimestres : 1 − (0.95 × 0.94 × 0.93) ≈ **0.170**, alors que la somme naïve donnerait 0.18. Sur 8 trimestres avec des risques croissants, l'écart devient important.

**Utilité** : permet de capter la **non-uniformité** du risque dans le temps (un trimestre de tension monétaire est plus risqué qu'un trimestre calme).

### 3. Décomposition par cas (voies alternatives)

Pour un événement qui peut se produire **par plusieurs chemins** :

$$P(\text{événement}) = P(\text{voie A}) + P(\text{voie B}) + P(\text{voie C}) - \text{intersections}$$

La somme simple est exacte si les voies sont **mutuellement exclusives** (définies comme « la voie par laquelle l'événement se produit en premier », par exemple). Si elles peuvent se cumuler, retrancher les intersections.

**Exemple** : *"Probabilité qu'un chef d'État perde le pouvoir d'ici fin 2027 ?"*

Voies :
- Défaite électorale : P(A) = 0.20
- Démission volontaire : P(B) = 0.05
- Destitution / impeachment : P(C) = 0.03
- Crise de santé : P(D) = 0.07
- Coup d'État : P(E) = 0.02

Probabilité totale ≈ 0.37 (voies définies comme exclusives : la première cause de départ).

### 4. Décomposition par taille (estimation de magnitude)

Pour estimer une quantité (et non une probabilité) :

**Exemple** : *"Combien d'utilisateurs actifs aura le produit X dans 3 ans ?"*

= Population cible × Taux d'adoption attendu × Taux de rétention

= 500 M (taille du marché) × 5 % (adoption sur 3 ans) × 60 % (rétention à 3 ans) ≈ **15 M utilisateurs**

*(Valeurs d'entrée hypothétiques : chacune doit être sourcée ou présentée comme hypothèse.)*

---

## Heuristiques pour bien décomposer

### Heuristique 1 : "Chaque sous-question doit être plus facile que le tout"

Si une sous-question est aussi difficile à estimer que la question initiale, la décomposition est inutile. Continuer à décomposer.

### Heuristique 2 : "Trois à cinq sous-questions"

En dessous de 3 : décomposition souvent insuffisante.
Au-dessus de 5 : la propagation d'erreur devient problématique.
(Heuristique interne, pas un résultat empirique.)

### Heuristique 3 : "Chercher l'asymétrie d'information"

Quelles sous-questions ont une **base rate connue** ? Décomposer dans cette direction.

**Exemple** : pour estimer une probabilité d'acquisition, on connaît mieux la base rate "taux annuel d'acquisitions dans le secteur" que la base rate "probabilité qu'une entreprise précise soit acquise dans 18 mois".

### Heuristique 4 : "Tester par triangulation"

Si possible, **décomposer la même question de deux manières différentes** (causale ET temporelle, par exemple). Si les deux décompositions donnent des estimations très divergentes, c'est un signal qu'au moins une est mal posée.

---

## Pièges classiques

### Piège 1 : Multiplication aveugle

Multiplier 5 probabilités donne presque toujours une probabilité finale très basse. Si la multiplication donne < 1 %, **vérifier** :
- Les sous-événements sont-ils réellement nécessaires ?
- Les probabilités conditionnelles ne sont-elles pas sous-estimées ?
- Les probabilités sont-elles bien conditionnées aux étapes précédentes (une corrélation positive ignorée fait baisser le produit à tort) ?
- D'autres voies mènent-elles au même événement ?

### Piège 2 : Pseudo-décomposition

Décomposer en sous-questions qui sont en réalité **la même question** sous des angles différents. Test : si chaque sous-question est résolue par la même donnée, la décomposition est illusoire.

### Piège 3 : Décomposition sans estimation

Décomposer puis dire "je ne sais pas" pour chaque sous-question. C'est un exercice de structuration, pas de prédiction. Si on ne peut estimer aucune sous-composante, soit la question n'est pas forecastable, soit la décomposition est mauvaise.

### Piège 4 : Mélange de probabilités et de magnitudes

Si certaines sous-questions sont des probabilités et d'autres des magnitudes, **ne pas multiplier** directement. Convertir tout en une dimension homogène.

---

## Cas-type complet : prédiction électorale

**Question** : *"Probabilité que le parti X obtienne la majorité absolue à l'élection législative du JJ/MM/AAAA ?"*

### Décomposition par seuils

Plutôt que d'estimer directement, décomposer par nombre de sièges (exemple : Assemblée nationale, 577 sièges, majorité absolue à 289) :

- P(X obtient ≥ 289 sièges) = Σ P(X obtient exactement N sièges), pour N ≥ 289

(Une décomposition du type « P(premier parti) × P(mobilise sa base) × P(capte les indécis) » est à éviter : ces facteurs ne sont ni des étapes nécessaires ni des événements bien définis.)

### Décomposition par méthode sondages

P(X majorité) ≈ probabilité que la fonction de vote estimée par sondages aboutisse à ≥ 289 sièges

= f(intentions de vote actuelles, marge d'erreur sondages, simulation projection siège)

### Décomposition par base rate historique

P(X majorité) ≈ base rate × ajustements
= (cas où un parti a obtenu la majorité dans une élection comparable) × facteurs spécifiques

### Triangulation des trois décompositions

Si les trois donnent ~25 %, l'estimation ~25 % est robuste à la méthode.
Si elles divergent (15 %, 25 %, 40 %), c'est un signal d'incertitude profonde : combiner en pondérant par la fiabilité estimée de chaque méthode (la moyenne simple des probabilités est un défaut raisonnable), et noter l'incertitude.

---

## Quand ne pas décomposer

La décomposition n'est pas toujours bénéfique :

- Pour des questions **simples** avec une base rate directement disponible.
- Pour des questions **uniques sans précédent** où la décomposition introduit plus de bruit que d'information.
- Pour des questions à très **court horizon** où l'incertitude réductible est faible.

Dans ces cas, l'estimation directe par jugement structuré est suffisante.

---

## Ressource pour s'exercer

L'exercice classique de Fermi : *"Combien de pianos sont accordés à Chicago par an ?"*

Décomposition :
- Population Chicago : ~3M habitants
- Foyers : ~3M / 2.5 = 1.2M foyers
- % avec piano : ~3% = 36 000 pianos
- Fréquence d'accord : 1/an en moyenne = 36 000 accords/an
- Accords par accordeur : ~3/jour × 250 jours = 750/an
- Nombre d'accordeurs nécessaires : 36 000 / 750 = **~48 accordeurs**

*(Toutes les valeurs d'entrée sont des hypothèses d'ordre de grandeur. La version 1.0 citait une « réponse réelle (Pages Jaunes) : entre 30 et 80 » sans source ; cette vérification est retirée. Ce qui compte dans l'exercice est l'ordre de grandeur et la traçabilité des hypothèses, pas la valeur exacte.)*

Le même type de décomposition, appliqué à une question prospective, rend les hypothèses explicites et donc discutables, ce qu'une intuition globale ne permet pas.

---

## Références

- Hubbard, D. W. (2010). *How to Measure Anything* (2e éd.). Wiley.
- Tetlock, P. E., & Gardner, D. (2015). *Superforecasting*. Crown.
