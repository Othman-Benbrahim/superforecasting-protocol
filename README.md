# 🎯 Superforecasting Protocol — Discipline de prédiction structurée

> *"Une prédiction qui ne précise ni horizon, ni probabilité, ni condition de réfutation n'est pas une prédiction. C'est une opinion."*

Un skill Claude qui applique à toute question prospective une **discipline de prévision inspirée des travaux du Good Judgment Project** (Tetlock, Mellers et collègues) : décomposition Fermi, base rates, scénarios probabilisés, indicateurs observables, conditions de falsification. Transforme une intuition en prédiction structurée, scorable, améliorable.

---

## Positionnement

Ce skill ne *remplace* pas l'analyse OSINT ni l'intuition stratégique. Il les **discipline**. Il prend une question prospective brute et en produit une *prédiction techniquement valide* — c'est-à-dire :

- assortie d'une probabilité numérique explicite,
- décomposée en sous-questions tractables,
- ancrée dans une base rate historique,
- formulée en plusieurs scénarios concurrents qui somment à 100%,
- accompagnée d'indicateurs observables datés,
- réfutable par des conditions précises.

C'est la discipline minimum sans laquelle aucun système prédictif ne peut s'améliorer dans le temps.

---

## Pourquoi ce skill

L'analyse géopolitique, économique et organisationnelle souffre d'une faiblesse documentée par Tetlock dans *Expert Political Judgment* (2005) : en moyenne, les prédictions des experts font **à peine mieux que le hasard** ou que des règles d'extrapolation simples, surtout à horizon de plusieurs années.

Le Good Judgment Project (2011-2015), financé par l'IARPA, a montré que la précision dépend en bonne partie de facteurs travaillables : entraînement au raisonnement probabiliste, travail en équipe, mises à jour fréquentes, agrégation des prévisions (Mellers et al., 2014 ; Mellers, Stone, Atanasov et al., 2015, *Journal of Experimental Psychology: Applied*, 21(1), 1-14). L'équipe Good Judgment a battu le groupe contrôle du tournoi de plus de 50 % ; Good Judgment affirme aussi une précision supérieure de plus de 30 % à celle d'analystes du renseignement ayant accès à des informations classifiées (chiffre institutionnel, sans méthode publiée sur la page source : https://goodjudgment.com/resources/the-superforecasters-track-record/).

**Statut** : le GJP n'a pas publié de « protocole en 7 étapes ». Il résume ses résultats en quatre leviers (talent, entraînement, équipe, agrégation) et Tetlock & Gardner (2015) en « Dix commandements ». Les 7 étapes de ce skill sont une **synthèse originale** de ces pratiques, avec des conventions internes signalées comme telles. La version 1.0 de ce README la présentait à tort comme « le protocole du GJP » et citait l'article de 2015 dans *Psychological Science* (où est paru l'article de 2014, distinct).

---

## Ce que produit le skill

Sur une question prospective soumise, le skill produit une **fiche de prédiction structurée** comprenant :

| Section | Contenu |
|---------|---------|
| **Reformulation** | La question en forme falsifiable (date, indicateur, seuil) |
| **Triage** | Type de question, horizon, prédictibilité estimée |
| **Décomposition** | Sous-questions tractables (Fermi) |
| **Base rate** | Fréquence historique (outside view) |
| **Inside view** | Ajustements spécifiques au cas |
| **Scénarios** | 3 à 5 scénarios concurrents avec probabilités sommant à 100% |
| **Indicateurs** | Événements observables datés qui actualiseraient chaque scénario |
| **Réfutation** | Conditions précises de falsification |
| **Cadence de révision** | Quand reprendre l'analyse |

Cette fiche est conçue pour être :
- **scorable** rétrospectivement par `calibration-engine`
- **actualisable** par `bayesian-updater` quand l'info évolue
- **traçable** pour audit ou apprentissage rétrospectif

---

## Cas d'usage typiques

- **Question géopolitique** : *"Quelle est la probabilité d'une rupture diplomatique entre X et Y dans les 12 prochains mois ?"*
- **Décision stratégique** : *"Cette restructuration aboutira-t-elle dans les délais annoncés ?"*
- **Prospective sectorielle** : *"L'industrie X subira-t-elle une consolidation majeure d'ici 2027 ?"*
- **Anticipation organisationnelle** : *"Ce dirigeant restera-t-il en fonction au-delà de l'horizon Z ?"*

Le skill est **inadapté** aux questions :
- Sans horizon temporel ("un jour", "à long terme")
- Sans indicateur observable ("la situation va se dégrader")
- À portée existentielle/morale ("est-ce que la démocratie va survivre")
- Sans base de comparaison historique

Dans ces cas, le skill **demande une reformulation** plutôt que de produire une fausse prédiction.

---

## Carte du dépôt

```
superforecasting-protocol/
│
├── README.md                              ← Ce fichier (page du dépôt, non chargé par l'agent)
├── SKILL.md                               ← Agent principal (7 étapes)
├── LICENSE                                ← GPL-3.0 (ajouté en v1.1 ; absent en v1.0)
│
└── references/
    ├── protocole-7-etapes.md              ← Détail opératoire de chaque étape
    ├── base-rates-outside-view.md         ← Méthode Kahneman + sources de base rates
    ├── decomposition-fermi.md             ← Décomposer une question complexe
    ├── scenarios-probabilites.md          ← Probabilités granulaires & somme à 100%
    └── biais-courants.md                  ← Pièges à éviter (overconfidence, narrative…)
```

---

## Fondements théoriques

| Référence | Apport |
|-----------|--------|
| **Tetlock & Gardner (2015)** — *Superforecasting* | Pratiques des meilleurs prévisionnistes, Dix commandements |
| **Tetlock (2005)** — *Expert Political Judgment* | Diagnostic : limites de la prévision experte |
| **Mellers et al. (2014)**, *Psychological Science* 25(5) | Effets de l'entraînement, des équipes, du suivi |
| **Mellers et al. (2015)**, *JEP: Applied* 21(1) | Déterminants de la précision (dispositions, situation, comportement) |
| **Friedman et al. (2018)**, *International Studies Quarterly* 62(2) | Valeur de la granularité des probabilités |
| **Kahneman & Lovallo (1993)** ; **Kahneman (2011)**, chap. 23 | Outside view, classe de référence |
| **Heuer (1999)** — *Psychology of Intelligence Analysis* | ACH, contrôle des biais |
| **Klein (2007)** — Pre-Mortem technique | Discipline anti-surajustement |
| **Hubbard (2010)** — *How to Measure Anything* | Calibration de l'incertitude |

Détail dans chaque fichier de référence.

---

## Activation

Le déclenchement repose sur le champ `description` du `SKILL.md`, seul champ chargé à l'avance par les agents conformes à la spécification Agent Skills. Formulations typiques : « quelle est la probabilité que… », « prédiction structurée », « forecast », « superforecasting », ou toute question prospective qui demande une probabilité explicite.

---

## Modes d'utilisation

Les trois modes (rapide, standard, approfondi) sont définis par des critères d'activation et un contenu précis dans le `SKILL.md`, section « Modes d'exécution ». Le taux de base reste obligatoire dans tous les modes.

---

## Dépendances et interopérabilité

Ce skill est conçu pour fonctionner **seul ou orchestré** :

| Skill frère | Relation |
|-------------|----------|
| `bayesian-updater` | Skill aval — actualise les prédictions quand l'info arrive |
| `calibration-engine` | Skill aval — score les prédictions a posteriori |
| `prediction-engine` | Orchestrateur — route vers ce skill (Mode A) |
| `signaux-du-futur` *(externe, non livré ici)* | Source amont — matériau OSINT brut |
| `miroir-trans-echelle` *(externe, non livré ici)* | Lecture symbolique croisée (plafond narrative attractor côté calibration) |

---

## Limites

- **La discipline ne crée pas la prescience.** Même rigoureux, le skill ne prédit pas mieux que ce que l'information disponible permet.
- **Les probabilités sont des estimations subjectives.** Elles ne sont pas des fréquences objectives — elles deviennent valides *à mesure que la calibration s'établit*.
- **Le protocole est coûteux.** Une fiche complète demande une vraie recherche de taux de base. Ce n'est pas un outil de réaction instantanée (voir le mode rapide pour les cas simples).
- **Le skill ne convient pas aux décisions à effet de seuil critique** (vie/mort, action immédiate) — il convient à la décision sous incertitude raisonnée.

---

## Licence

GPL-3.0, écosystème IRIS∞.

---

*« La prédiction n'est pas un don. C'est une discipline. Elle se mesure, elle s'entraîne, elle s'améliore — ou elle reste opinion. »*
