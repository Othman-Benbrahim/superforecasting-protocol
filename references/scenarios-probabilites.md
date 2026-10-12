# Scénarios concurrents & Probabilités granulaires

Ce fichier détaille la construction de scénarios MECE (Mutually Exclusive, Collectively Exhaustive) et l'usage des probabilités granulaires.

---

## Pourquoi des scénarios concurrents

L'analyste non discipliné formule **un scénario** (le plus plausible à ses yeux) et l'argumente. C'est le piège du scénario unique, discuté par Schoemaker (« Scenario planning: A tool for strategic thinking », *Sloan Management Review*, 1995) : on devient prisonnier de son récit, on cherche la confirmation, on ignore les signaux contraires.

Les scénarios concurrents forcent l'analyste à :
- **reconnaître** que d'autres trajectoires sont possibles
- **estimer** explicitement la probabilité de chacune
- **valider** par sommation à 100% qu'il a couvert l'espace
- **comparer** la fertilité respective des trajectoires

C'est aussi la condition pour que la prédiction soit **scorable** : le Brier score compare des probabilités attribuées à un ensemble complet d'issues (deux pour une question binaire, davantage pour une question multinomiale).

---

## Construire un set MECE

### Test MECE (à appliquer systématiquement)

**Mutually Exclusive (ME)** :
- *"Si je connais le résultat futur, puis-je le classer dans un seul des scénarios sans ambiguïté ?"*
- Si non → les scénarios se chevauchent, reformuler.

**Collectively Exhaustive (CE)** :
- *"Existe-t-il un résultat plausible qui ne rentre dans aucun de mes scénarios ?"*
- Si oui → ajouter un scénario "autre" ou reformuler.

**Test final** : les probabilités somment-elles exactement à 1.00 ? Si non, il manque une issue ou il y a double comptage. (La somme à 1 est nécessaire, pas suffisante : des scénarios qui se chevauchent peuvent sommer à 1 par ajustement.)

---

### Stratégies de construction

#### Stratégie A — Binaire

Pour les questions oui/non simples :
- S1 = OUI (P)
- S2 = NON (1−P)

Trivialement MECE. C'est le format minimal, et le format naturel des questions binaires. Ajouter des scénarios n'a de sens que si l'on veut distinguer les **voies** ou **modalités** de réalisation.

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

Si « Autre » porte plus de 20 % de probabilité (seuil indicatif), c'est probablement qu'au moins un scénario significatif n'est pas explicité. **Le nommer**.

### Antipattern 4 — Scénarios non-exhaustifs

❌ Probabilités sommant à 80% sans scénario résiduel.

Ajouter d'abord un scénario « aucun des précédents » : les 20 % manquants représentent souvent une issue réelle. Ne renormaliser proportionnellement que si l'on est certain que les scénarios listés sont exhaustifs — la renormalisation masque sinon l'issue oubliée.

### Antipattern 5 — Trop de scénarios

❌ 8 scénarios à 12.5% chacun.

Au-delà de 5 scénarios, il devient difficile de discriminer entre eux (heuristique). **Regrouper** les scénarios similaires, sauf si la question l'impose (ex. intervalles d'une variable continue).

---

## Probabilités granulaires

### Ce que dit la recherche

La version 1.0 affirmait que les superforecasters utilisent « quasi exclusivement » des pas de 5 % et que toute précision plus fine serait de la « fausse précision ». C'est contredit par les données du Good Judgment Project : Friedman, Baker, Mellers, Tetlock & Zeckhauser (2018) montrent que **arrondir les prévisions à des catégories plus grossières dégrade systématiquement leur précision**, et que les meilleurs prévisionnistes distinguent en moyenne une dizaine de niveaux de probabilité (davantage pour certains). Dans ces données, environ la moitié des prévisions sont des multiples de 10 % et un quart d'autres multiples de 5 % : c'est une habitude, pas un optimum démontré.

### Règle pratique du skill (convention)

- **Zone 10-90 %** : des pas de 5 % sont un bon défaut ; une valeur plus fine est admise si l'analyse la justifie.
- **En dessous de 10 %** : pas plus fins — 1 %, 2 %, 3 %, 5 %, 7 %, 10 % — car un facteur 2 (1 % vs 2 %) est une différence importante.
- **Au-dessus de 90 %** : 90 %, 93 %, 95 %, 97 %, 98 %, 99 %.
- **Plage admise** : [1 % ; 99 %] ; hors de [5 % ; 95 %], justification explicite (règle commune avec `calibration-engine`).

### Discipline : pas de "vers 30%"

L'analyste discipliné dit "30%" ou "35%", jamais "vers 30%". L'imprécision verbale masque le manque de réflexion. Le choix entre 30 et 35 doit être délibéré.

### Test du pari

**Outil classique de la théorie de la décision** (interprétation subjective des probabilités chez de Finetti et Savage), souvent recommandé en prévision : *« Êtes-vous prêt à parier à cette cote ? »*

Si vous estimez 60 % pour l'événement X, seriez-vous indifférent entre miser 60 € pour gagner 40 € si X se produit, et miser 40 € pour gagner 60 € si X ne se produit pas ? Si vous préférez nettement l'un des deux côtés, votre probabilité n'est pas la bonne : ajuster dans le sens du pari que vous préférez.

---

## Estimer correctement les basses probabilités

Dans l'étude classique de Lichtenstein, Slovic, Fischhoff, Layman & Combs (1978, « Judged frequency of lethal events », *Journal of Experimental Psychology: Human Learning and Memory*, 4(6), 551-578), les sujets **surestiment** la fréquence des causes de décès rares et spectaculaires (souvent médiatisées) et **sous-estiment** celle des causes fréquentes et banales. Pour la prévision : ne pas laisser la saillance médiatique fixer une probabilité, et toujours revenir au taux de base.

### Heuristiques pour les basses probabilités

**Heuristique 1 — Inverser** : au lieu d'estimer P(X), estimer P(non X) si X est rare. Plus facile à intuitionner.

**Heuristique 2 — Traduire en fréquences** (pour une probabilité **annuelle** constante) :
- P ≈ 1 % par an : environ une fois par siècle ; ≈ 10 % de chances sur une décennie
- P ≈ 5 % par an : environ une fois tous les 20 ans ; ≈ 40 % sur une décennie
- P ≈ 10 % par an : environ une fois par décennie ; ≈ 65 % sur une décennie
- P ≈ 25 % : une chance sur quatre
- P ≈ 50 % : une chance sur deux

(Sur n années, la probabilité d'au moins une occurrence vaut 1 − (1 − p)ⁿ, pas n × p. La version 1.0 contenait des équivalences erronées, ex. « 1 % = un événement par décennie ».)

**Heuristique 3 — Vérifier la cohérence avec d'autres prédictions** : P(A et B) ne peut pas dépasser min(P(A), P(B)). Si l'on estime P(A) = 5 % et P(B) = 5 % mais que l'on donne 10 % au scénario « A et B », il y a incohérence (erreur de conjonction). Inversement, si A et B sont indépendants, P(A et B) = 0.25 % : vérifier que la surprise ressentie correspond.

---

## Mise en garde : conservation par défaut

L'inertie est puissante. Pour beaucoup de questions prospectives à court terme, le scénario **statu quo** ou **continuation des tendances** est le plus probable (ordre de grandeur indicatif, à confirmer par le taux de base de la classe).

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
- CE : peut-on imaginer un résultat hors de ces quatre ? → oui : élection annulée ou reportée au-delà de la date butoir → ajouter **S5 = « pas de résultat officiel avant la date butoir » (1 %)** et réduire S4 à 14 %. Un scénario plausible ne reçoit jamais 0 % : ce serait une certitude qu'il n'arrivera pas.

Ensemble final : S1 5 %, S2 45 %, S3 35 %, S4 14 %, S5 1 %. Somme = 100 % ✓

### Probabilités granulaires

Pas de 5 % dans la zone centrale ; pas plus fins pour les issues rares (14 %, 1 %), conformément à la règle pratique ci-dessus.

### Test du parier

P(X gagne au second tour) = 45 %. Suis-je indifférent entre miser 45 € pour en gagner 55 € si cela se produit, et le pari inverse ? Si oui, la probabilité reflète ma croyance (ce qui n'en garantit pas la calibration, que seul le scoring établit). Si je préfère un côté, ajuster.

---

## Récapitulatif opérationnel

Pour chaque prédiction structurée :
1. Identifier le type de question (binaire / multinomiale / continue / conditionnelle)
2. Construire 3-5 scénarios MECE
3. Attribuer des probabilités explicites (pas de 5 % dans la zone centrale, pas plus fins aux extrêmes ; plage [1 % ; 99 %])
4. Vérifier somme = 100%
5. Tester MECE explicitement
6. Tester chaque probabilité par le test du pari
7. Documenter dans le format standard du SKILL

Cette discipline est ce qui rend la prédiction scoreable, donc améliorable, donc utile.

---

## Références

- Friedman, J. A., Baker, J. D., Mellers, B. A., Tetlock, P. E., & Zeckhauser, R. (2018). The value of precision in probability assessment. *International Studies Quarterly*, 62(2), 410-422.
- Lichtenstein, S., Slovic, P., Fischhoff, B., Layman, M., & Combs, B. (1978). Judged frequency of lethal events. *Journal of Experimental Psychology: Human Learning and Memory*, 4(6), 551-578.
- Schoemaker, P. J. H. (1995). Scenario planning: A tool for strategic thinking. *Sloan Management Review*, 36(2), 25-40.
- Tversky, A., & Kahneman, D. (1983). Extensional versus intuitive reasoning: The conjunction fallacy in probability judgment. *Psychological Review*, 90(4), 293-315.
