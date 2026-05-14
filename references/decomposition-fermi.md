# Décomposition Fermi — Casser le complexe en tractable

> *"Combien d'accordeurs de piano y a-t-il à Chicago ?"* — Enrico Fermi, posant la question qui a donné son nom à la méthode.

La décomposition Fermi est l'art de transformer une question apparemment impossible à estimer en une suite de sous-questions individuellement plus faciles. C'est la technique opérationnelle qui permet aux superforecasters de battre les experts sur des sujets où ils n'ont pas d'expertise sectorielle.

---

## Le principe

Face à une question dont l'estimation directe semble "impossible", on la **casse** en composantes mesurables ou estimables. Chaque sous-estimation a sa marge d'erreur, mais — c'est le théorème — quand les erreurs sont **non-corrélées** et **non-systématiques**, elles tendent à **se compenser**. L'estimation finale est plus précise que ne le serait une estimation directe biaisée.

C'est exactement ce que fait un physicien estimant un ordre de grandeur sans calcul exact.

---

## Stratégies de décomposition

### 1. Décomposition causale (chaîne d'événements conditionnels)

Pour un événement complexe = série d'étapes :

$$P(\text{événement}) = P(E_1) \times P(E_2 | E_1) \times P(E_3 | E_2) \times ...$$

**Exemple** : *"L'entreprise X va-t-elle être acquise dans les 18 mois ?"*

| Sous-événement | Probabilité estimée |
|----------------|---------------------|
| P(X présente des signes de vulnérabilité financière d'ici 18 mois) | 0.40 |
| P(un acquéreur crédible se positionne | vulnérabilité) | 0.50 |
| P(les négociations aboutissent | acquéreur positionné) | 0.60 |
| P(la régulation antitrust autorise | accord signé) | 0.80 |
| P(les actionnaires acceptent | régulation OK) | 0.85 |

Probabilité finale = 0.40 × 0.50 × 0.60 × 0.80 × 0.85 ≈ **0.082** (~8%)

⚠ **Attention aux corrélations cachées** : si plusieurs sous-événements sont *liés* (ex. la vulnérabilité financière augmente la probabilité que les actionnaires acceptent une offre basse), la multiplication directe sous-estime. Dans ce cas, ajuster vers le haut.

### 2. Décomposition temporelle

Pour une probabilité cumulée sur une période = somme des probabilités par sous-période :

$$P(\text{événement avant T}) = \sum_{t=1}^{T} P(\text{événement à t} | \text{pas à t-1, t-2, ...})$$

**Exemple** : *"Probabilité d'une crise économique en France d'ici 24 mois ?"*

Décomposer par trimestre :
- P(crise au T1 2026) = 0.05
- P(crise au T2 2026 | pas au T1) = 0.06
- P(crise au T3 2026 | pas au T1, T2) = 0.07
- ... (8 trimestres au total)

Somme cumulée ≈ probabilité totale sur 24 mois.

**Utilité** : permet de capter la **non-uniformité** du risque dans le temps (un trimestre de tension monétaire est plus risqué qu'un trimestre calme).

### 3. Décomposition par cas (voies alternatives)

Pour un événement qui peut se produire **par plusieurs chemins indépendants** :

$$P(\text{événement}) = P(\text{voie A}) + P(\text{voie B}) + P(\text{voie C}) - \text{ajustements pour intersections}$$

**Exemple** : *"Probabilité qu'un chef d'État perde le pouvoir d'ici fin 2027 ?"*

Voies :
- Défaite électorale : P(A) = 0.20
- Démission volontaire : P(B) = 0.05
- Destitution / impeachment : P(C) = 0.03
- Crise de santé : P(D) = 0.07
- Coup d'État : P(E) = 0.02

Probabilité totale ≈ 0.37 (en supposant exclusivité approximative).

### 4. Décomposition par taille (estimation de magnitude)

Pour estimer une quantité (et non une probabilité) :

**Exemple** : *"Combien d'utilisateurs actifs aura le produit X dans 3 ans ?"*

= Population cible × Taux d'adoption attendu × Taux de rétention

= 500M (taille marché) × 5% (adoption optimiste sur 3 ans pour ce type de produit) × 60% (rétention typique SaaS B2C année 3) ≈ **15M utilisateurs**

---

## Heuristiques pour bien décomposer

### Heuristique 1 : "Chaque sous-question doit être plus facile que le tout"

Si une sous-question est aussi difficile à estimer que la question initiale, la décomposition est inutile. Continuer à décomposer.

### Heuristique 2 : "Trois à cinq sous-questions"

En dessous de 3 : décomposition insuffisante.
Au-dessus de 5 : la propagation d'erreur devient problématique.

### Heuristique 3 : "Chercher l'asymétrie d'information"

Quelles sous-questions ont une **base rate connue** ? Décomposer dans cette direction.

**Exemple** : pour estimer une probabilité d'acquisition, on connaît mieux la base rate "taux annuel d'acquisitions dans le secteur" que la base rate "probabilité qu'une entreprise précise soit acquise dans 18 mois".

### Heuristique 4 : "Tester par triangulation"

Si possible, **décomposer la même question de deux manières différentes** (causale ET temporelle, par exemple). Si les deux décompositions donnent des estimations très divergentes, c'est un signal qu'au moins une est mal posée.

---

## Pièges classiques

### Piège 1 : Multiplication aveugle

Multiplier 5 probabilités conditionnelles donne presque toujours une probabilité finale très basse (effet de l'exposant). Si la multiplication donne < 1%, **vérifier** :
- Les sous-événements sont-ils réellement nécessaires ?
- Les probabilités conditionnelles ne sont-elles pas sous-estimées ?
- N'y a-t-il pas une corrélation positive qui devrait remonter le total ?

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

Plutôt que d'estimer directement, décomposer par seuils de siège :

- P(X obtient ≥ 289 sièges, seuil de majorité) = ?

= P(X reste premier parti) × P(X mobilise sa base) × P(X capte les indécis)

ou alternativement, plus opérationnellement :

= Σ P(X obtient exactement N sièges), pour N ≥ 289

### Décomposition par méthode sondages

P(X majorité) ≈ probabilité que la fonction de vote estimée par sondages aboutisse à ≥ 289 sièges

= f(intentions de vote actuelles, marge d'erreur sondages, simulation projection siège)

### Décomposition par base rate historique

P(X majorité) ≈ base rate × ajustements
= (cas où un parti a obtenu la majorité dans une élection comparable) × facteurs spécifiques

### Triangulation des trois décompositions

Si les trois donnent ~25%, on peut estimer ~25% avec confiance.
Si elles divergent (15%, 25%, 40%), c'est un signal d'incertitude profonde : choisir la moyenne pondérée par la fiabilité de chaque méthode, et noter l'incertitude.

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

Réponse réelle (Yellow Pages) : entre 30 et 80. Estimation Fermi : excellente.

Le même type de décomposition appliqué à une question prospective produit une prédiction plus solide qu'une intuition globale.
