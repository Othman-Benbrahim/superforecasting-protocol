# Scénarios concurrents & Probabilités granulaires

Ce fichier détaille la construction de scénarios MECE (Mutually Exclusive, Collectively Exhaustive) et l'usage des probabilités granulaires — deux des pratiques les plus distinctives des superforecasters.

---

## Pourquoi des scénarios concurrents

L'analyste non-discipliné formule **un scénario** (le plus plausible à ses yeux) et l'argumente. C'est le piège du scénario unique, documenté par Schoemaker (*Sloan Management Review*, 1995) : on devient prisonnier de son récit, on cherche la confirmation, on ignore les signaux contraires.

Les scénarios concurrents forcent l'analyste à :
- **reconnaître** que d'autres trajectoires sont possibles
- **estimer** explicitement la probabilité de chacune
- **valider** par sommation à 100% qu'il a couvert l'espace
- **comparer** la fertilité respective des trajectoires

C'est aussi la condition pour que la prédiction soit **scoreable** : un Brier score n'a de sens qu'avec des probabilités attribuées à plusieurs résultats possibles.

---

## Construire un set MECE

### Test MECE (à appliquer systématiquement)

**Mutually Exclusive (ME)** :
- *"Si je connais le résultat futur, puis-je le classer dans un seul des scénarios sans ambiguïté ?"*
- Si non → les scénarios se chevauchent, reformuler.

**Collectively Exhaustive (CE)** :
- *"Existe-t-il un résultat plausible qui ne rentre dans aucun de mes scénarios ?"*
- Si oui → ajouter un scénario "autre" ou reformuler.

**Test final** : probabilités somment-elles exactement à 1.00 ? Si non, il manque ou il y a double comptage.

---

### Stratégies de construction

#### Stratégie A — Binaire

Pour les questions oui/non simples :
- S1 = OUI (P)
- S2 = NON (1−P)

Trivialement MECE. C'est le format minimal.

#### Stratégie B — Tripartition standard

Le format le plus courant en analyse prospective :
- S1 = **Optimiste** (probabilité P1)
- S2 = **Probable** / médian (probabilité P2)
- S3 = **Critique** / pessimiste (probabilité P3)

⚠ **Piège** : "optimiste/médian/pessimiste" peut ne pas être MECE si les frontières ne sont pas définies. **Toujours préciser** où s'arrête chaque scénario par un indicateur seuil :
- S1 (Optimiste) = indicateur X > seuil A
- S2 (Probable) = seuil A ≥ indicateur X ≥ seuil B
- S3 (Critique) = indicateur X < seuil B

#### Stratégie C — Multinomiale par voie

Quand plusieurs voies de résolution existent :
- S1 = Résolution par voie A
- S2 = Résolution par voie B
- S3 = Résolution par voie C
- S4 = Non-résolution dans l'horizon

Exemple : *"Comment X va-t-il quitter ses fonctions d'ici fin 2027 ?"*
- S1 = Défaite électorale (15%)
- S2 = Démission volontaire (5%)
- S3 = Destitution (3%)
- S4 = Décès / incapacité (5%)
- S5 = Reste en fonctions (72%)
- **Total : 100%** ✓

#### Stratégie D — Sur intervalle continu

Quand l'événement est mesuré sur une échelle continue (croissance PIB, sièges, parts de marché), **discrétiser en 3-5 intervalles** :

Exemple : *"Croissance France 2026 ?"*
- S1 = < 0% (récession) — 10%
- S2 = 0-1% — 30%
- S3 = 1-2% — 35%
- S4 = 2-3% — 20%
- S5 = > 3% — 5%
- **Total : 100%** ✓

#### Stratégie E — Conditionnelle

Pour des questions à branche logique :
- S1 = A se produit ET B se produit (P1)
- S2 = A se produit ET B ne se produit pas (P2)
- S3 = A ne se produit pas ET B se produit (P3)
- S4 = Ni A ni B (P4)

Pour deux événements binaires, on a 4 scénarios. Pour trois, on a 8. Au-delà, la combinatoire explose — décomposer autrement.

---

## Antipatterns fréquents

### Antipattern 1 — Scénarios redondants

❌ S1 = légère détérioration, S2 = détérioration modérée, S3 = détérioration sévère.

Ce n'est pas trois scénarios — c'est un seul scénario (détérioration) avec trois niveaux d'intensité. Il **manque** :
- Le scénario "amélioration"
- Le scénario "stabilité"

**Reformulation correcte** : S1 amélioration, S2 stabilité, S3 légère détérioration, S4 forte détérioration.

### Antipattern 2 — Scénarios à frontière floue

❌ S1 = "crise majeure", S2 = "tension élevée", S3 = "stabilité".

Que signifient "majeure" et "élevée" précisément ? Sans seuils opérationnels, impossible de classer le résultat futur de manière non-ambiguë. **Spécifier des indicateurs seuils**.

### Antipattern 3 — Le "fourre-tout"

❌ S1 = Scénario A, S2 = Scénario B, S3 = "Autre".

Si "Autre" porte plus de 20% de probabilité, c'est qu'il y a au moins un scénario significatif non-explicité. **Le nommer**.

### Antipattern 4 — Scénarios non-exhaustifs

❌ Probabilités sommant à 80% sans scénario résiduel.

Soit ajouter un scénario "aucun des précédents", soit normaliser à 100% en remontant chaque probabilité.

### Antipattern 5 — Trop de scénarios

❌ 8 scénarios à 12.5% chacun.

Au-delà de 5 scénarios, l'analyste a en fait perdu sa capacité à discriminer. **Regrouper** les scénarios similaires.

---

## Probabilités granulaires : la règle des 5%

### Pourquoi 5%

Les superforecasters du GJP utilisent quasi-exclusivement des incréments de **5%** : 5, 10, 15, 20, 25, 30, ..., 95.

Pourquoi :
- **En dessous (1-2%)** : fausse précision. Personne ne distingue réellement 23% de 26%.
- **Au-dessus (10-25%)** : perte d'information. La différence entre 30% et 50% importe.
- **À 5%** : équilibre optimal entre précision et calibration.

### Exception pour les basses probabilités

Pour P < 5%, utiliser des incréments plus fins :
- 1%, 2%, 3%, 5%, 7%, 10%

Pourquoi : à basse probabilité, un facteur 2 (1% vs 2%) reste significatif.

De même pour P > 95% :
- 95%, 97%, 98%, 99%

### Discipline : pas de "vers 30%"

L'analyste discipliné dit "30%" ou "35%", jamais "vers 30%". L'imprécision verbale masque le manque de réflexion. Le choix entre 30 et 35 doit être délibéré.

### Test du parier

**Test classique du Good Judgment Project** : *"Êtes-vous prêt à parier à ce ratio ?"*

Si vous estimez 60% pour l'événement X, êtes-vous prêt à parier 60$ contre 40$ que X se produira ? Si vous hésitez, soit votre probabilité est trop haute (vous croyez moins), soit trop basse (vous croyez plus). Ajuster.

---

## Estimer correctement les basses probabilités

Les humains sous-estiment systématiquement la fréquence des événements rares mais réguliers (ex. crises financières) et sur-estiment la fréquence des événements catastrophiques médiatisés (ex. attentats terroristes), selon les travaux de Slovic, Fischhoff et Lichtenstein (*Risk Analysis*, 1980-1990).

### Heuristiques pour les basses probabilités

**Heuristique 1 — Inverser** : au lieu d'estimer P(X), estimer P(non X) si X est rare. Plus facile à intuitionner.

**Heuristique 2 — Comparer à des réferences connues** :
- P ≈ 1% : un événement par décennie (à l'échelle d'une vie active)
- P ≈ 5% : un événement par décennie ou deux en l'espérance
- P ≈ 10% : approximativement tous les 10 ans dans une décennie observable
- P ≈ 25% : un trimestre par an
- P ≈ 50% : un événement sur deux

**Heuristique 3 — Vérifier la cohérence avec d'autres prédictions** : si on estime P(A) = 5% et P(B) = 5%, mais qu'on jugerait également surprenant si A *et* B se produisaient, il y a incohérence.

---

## Mise en garde : conservation par défaut

L'inertie est puissante. Pour la plupart des questions prospectives, le scénario **statu quo** ou **continuation des tendances** est le plus probable à court terme — souvent 50-70%.

Si vos scénarios donnent moins de poids au statu quo, **vérifier** que c'est justifié par des indicateurs forts, pas par la séduction des changements dramatiques.

C'est l'erreur la plus commune des analystes débutants : sur-pondérer le changement parce qu'il est narratif plus séduisant.

---

## Cas-type complet

**Question reformulée falsifiable** : *"D'ici le 31/12/2027, le parti X aura-t-il obtenu la présidence du pays Y selon la résolution officielle de la commission électorale ?"*

### Construction des scénarios

#### Tentative 1 (à éviter)
- S1 = X gagne facilement (30%)
- S2 = X gagne de justesse (20%)
- S3 = X perd de peu (25%)
- S4 = X perd nettement (25%)

❌ Problème : S1+S2 et S3+S4 répondent à la même question fondamentale (X gagne ou perd). Le découpage par intensité n'apporte pas d'information pour la *prédiction de la présidence*.

#### Reformulation MECE
- S1 = X gagne au premier tour (5%)
- S2 = X gagne au second tour (45%)
- S3 = X perd au second tour (35%)
- S4 = X éliminé au premier tour (15%)
- **Total : 100%** ✓

#### Test MECE
- ME : un résultat ne peut pas être dans deux scénarios → ✓
- CE : peut-on imaginer un résultat hors de ces quatre ? → annulation ? → ajouter S5 = 0% (probabilité résiduelle, événement non considéré)

✓ Set valide.

### Probabilités granulaires

Toutes à incréments de 5% : 5, 45, 35, 15. Somme = 100. ✓

### Test du parier

P(X gagne au second tour) = 45%. Suis-je prêt à parier 45$ contre 55$ que cela se produira ? Si oui, la probabilité est bien calibrée. Si je trouverais le pari déséquilibré dans un sens, ajuster.

---

## Récapitulatif opérationnel

Pour chaque prédiction structurée :
1. Identifier le type de question (binaire / multinomiale / continue / conditionnelle)
2. Construire 3-5 scénarios MECE
3. Attribuer probabilités par incréments de 5% (1% pour très basses, 1% pour très hautes)
4. Vérifier somme = 100%
5. Tester MECE explicitement
6. Tester chaque probabilité par "test du parier"
7. Documenter dans le format standard du SKILL

Cette discipline est ce qui rend la prédiction scoreable, donc améliorable, donc utile.
