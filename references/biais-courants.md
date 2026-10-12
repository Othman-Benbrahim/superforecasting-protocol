# Biais courants en prédiction & contre-mesures

Ce fichier liste les biais cognitifs documentés qui dégradent la prédiction, avec leur **contre-mesure opérationnelle** dans le cadre du protocole superforecasting.

C'est un fichier de consultation rapide pendant l'application du protocole. À relire avant chaque prédiction importante.

---

## Biais 1 — Excès de confiance (overconfidence)

**Description** : probabilités plus extrêmes que ne le justifie la performance. Le prévisionniste moyen se croit plus fiable qu'il ne l'est, particulièrement aux extrêmes (90 %, 95 %, mais aussi 5 %, 10 % : annoncer 5 % pour un événement qui survient 15 % du temps est aussi de la sur-confiance).

**Manifestation typique** : attribution de 95 % à un scénario qui se réalise en réalité ~75 % du temps.

**Évidence** : Lichtenstein, Fischhoff & Phillips (1982), « Calibration of probabilities: The state of the art to 1980 », in Kahneman, Slovic & Tversky (Eds.), *Judgment under Uncertainty* — revue de la littérature (pas une méta-analyse au sens statistique) ; Fischhoff, Slovic & Lichtenstein (1977) : environ 17 à 30 % d'erreurs sur des réponses jugées certaines.

**Contre-mesure** :
- **Limiter** les probabilités extrêmes (< 5 % et > 95 %) aux cas où l'on a un taux de base explicite ; c'est la règle `justification_extreme` commune avec `calibration-engine`.
- Demander : *"sur 100 prédictions similaires faites par le passé, combien se sont avérées ?"*
- Utiliser `calibration-engine` pour mesurer son propre patron d'overconfidence.

---

## Biais 2 — Biais de confirmation (confirmation bias)

**Description** : recherche sélective des informations qui confirment l'hypothèse préférée, écartement des informations qui la contredisent (Wason, *Quarterly Journal of Experimental Psychology*, 1960).

**Manifestation typique** : après avoir formulé S1 comme scénario favori, on accumule les indicateurs pro-S1 et ignore les indicateurs pro-S2.

**Contre-mesure** :
- **Devil's advocacy** : formuler explicitement le meilleur argument pour le scénario opposé.
- **Red team** : demander à un tiers (ou à l'IA dans un autre prompt) d'argumenter contre la prédiction.
- **Liste de désistement** : pour chaque scénario, écrire 2-3 raisons qui le réfuteraient.

---

## Biais 3 — Biais de récence (recency bias)

**Description** : surpondération des événements récents par rapport aux fréquences historiques.

**Manifestation typique** : après un événement saillant (crise, attentat, krach), on surestime fortement la probabilité de récurrence à court terme.

**Évidence** : Tversky & Kahneman (*Cognitive Psychology*, 1973) — biais de disponibilité.

**Contre-mesure** :
- **Privilégier l'outside view longue** : base rate sur 20+ ans plutôt que 2 ans.
- Demander : *"si l'événement récent n'avait pas eu lieu, ma probabilité serait-elle différente ? De combien ?"* — c'est la magnitude du biais de récence.

---

## Biais 4 — Ancrage (anchoring)

**Description** : la première estimation reçue ou formulée influence disproportionnellement les suivantes (Tversky & Kahneman, *Science*, 1974).

**Manifestation typique** : après avoir lu "les analystes estiment 60% de probabilité", on aboutit à 55-65% indépendamment des arguments.

**Contre-mesure** :
- **Estimer d'abord, lire ensuite** : produire son estimation avant de consulter les sources tierces.
- **Ranger les sources par fiabilité** : pondérer explicitement.
- **Demander une fourchette plus large** au début : "si je devais donner un intervalle de confiance à 90%, ce serait quoi ?" — cela réduit l'ancrage sur un nombre unique.

---

## Biais 5 — Inside view excessive

**Description** : surpondération des spécificités du cas présent, sous-pondération de la base rate (Kahneman & Lovallo, *Management Science*, 1993).

**Manifestation typique** : "ce cas est différent parce que..." — l'analyste construit un argumentaire qui justifie un écart fort par rapport à la base rate.

**Contre-mesure** :
- **Seuil d'alerte des 20 points** (convention interne de ce protocole, non attribuable à Tetlock) : si l'inside view déplace la probabilité de plus de 20 points par rapport au taux de base, s'arrêter et justifier explicitement l'écart.
- **Tester avec une seconde classe de référence** plus large.
- Demander à un tiers : "si tu ne connaissais rien à ce cas, juste les chiffres, que prédirais-tu ?"

---

## Biais 6 — Narrative seduction (séduction narrative)

**Description** : préférence pour les scénarios qui racontent une histoire cohérente et émotionnellement satisfaisante, au détriment des scénarios statistiquement plus probables mais moins narratifs (Kahneman, *Thinking, Fast and Slow*, chap. 19 — "L'illusion de comprendre").

**Manifestation typique** : sur-pondération du scénario "scandale révélé" ou "retournement dramatique" par rapport au scénario "lente continuation".

**Contre-mesure** :
- **Formuler d'abord le scénario de statu quo** ou de continuation des tendances, puis les ruptures.
- Tester : *"si je devais résumer ce scénario en une phrase prosaïque sans drame, est-ce qu'il resterait crédible ?"* Si la séduction du scénario tient à son drame, c'est un biais.
- Privilégier les **scénarios ennuyeux mais plausibles**.

---

## Biais 7 — Effet de groupe (groupthink)

**Description** : convergence des estimations vers le consensus du groupe, indépendamment de la qualité des arguments (Janis, *Groupthink*, 1972).

**Manifestation typique** : dans une équipe d'analystes, les prédictions deviennent rapidement homogènes ; les dissensions individuelles s'effacent.

**Contre-mesure** :
- **Estimation silencieuse** : chaque analyste formule sa prédiction *avant* discussion.
- **Agrégation arithmétique** : médiane ou moyenne des estimations individuelles, **avant** débat.
- **Devil's advocate désigné** : rôle formel d'opposition pour chaque scénario.

---

## Biais 8 — Excès de pessimisme / d'optimisme situationnel

**Description** : selon l'humeur, le contexte, ou la disposition personnelle, l'analyste biaise systématiquement vers le sombre ou le rose.

**Manifestation typique** : un analyste très inquiet personnellement surpondérera systématiquement les scénarios catastrophiques ; un analyste enthousiaste l'inverse.

**Contre-mesure** :
- **Auto-monitoring** : noter son humeur et son contexte avant chaque prédiction. Calibration engine peut révéler des patrons.
- **Diversifier l'horaire et l'environnement** des prédictions importantes.
- **Cross-check** avec quelqu'un de tempérament opposé.

---

## Biais 9 — Régression à la moyenne ignorée

**Description** : après un événement extrême (très bon ou très mauvais), tendance à prédire la continuation de l'extrême, alors que la régression à la moyenne est statistiquement attendue (Galton, 1886 ; Kahneman, chap. 17).

**Manifestation typique** : après un trimestre de croissance exceptionnelle, prédiction d'une continuation au lieu d'un retour à la moyenne.

**Contre-mesure** :
- **Identifier explicitement** les extrêmes récents dans la chaîne d'observations.
- **Pondérer le scénario "retour à la moyenne"** plus fortement que ne le suggère l'intuition.
- Demander : *"sur la base de la distribution historique, quelle est la durée moyenne d'une déviation comparable ?"*

---

## Biais 10 — Pensée binaire (false dichotomy)

**Description** : formulation des scénarios en deux pôles opposés, ignorance des trajectoires intermédiaires ou orthogonales.

**Manifestation typique** : "soit la guerre, soit la paix" — alors que la réalité offre escalade contrôlée, conflit gelé, escalade médiatique sans action militaire, etc.

**Contre-mesure** :
- Pour les **questions ouvertes** (« comment X va-t-il évoluer ? »), formuler au moins 3 scénarios. Une **question binaire** bien posée garde ses deux issues (oui / non) ; le risque de fausse dichotomie concerne la façon de poser la question, pas le nombre d'issues d'une question binaire.
- Demander : *"quels sont les états intermédiaires ou orthogonaux entre mes deux pôles ?"*
- Inclure systématiquement un scénario "rien de remarquable ne se passe".

---

## Biais 11 — Conjunction fallacy

**Description** : tendance à attribuer une probabilité plus élevée à un scénario spécifique et détaillé qu'à un scénario plus général qui le contient (Tversky & Kahneman, *Psychological Review*, 1983 — exemple de Linda).

**Manifestation typique** : « Crise économique causée par un effondrement immobilier en Chine entraînant une contagion bancaire en Europe » reçoit une probabilité plus haute que « crise économique » tout court — alors que la probabilité d'un scénario détaillé ne peut pas dépasser celle du scénario général qui le contient.

**Contre-mesure** :
- Toujours formuler les scénarios au niveau **le plus simple** suffisant.
- Tester : si je détaille davantage, ma probabilité devrait *baisser*, pas monter. Si elle monte, biais.

---

## Biais 12 — Effet halo & contamination narrative

**Description** : un trait saillant influence les estimations sur des dimensions indépendantes.

**Manifestation typique** : un dirigeant charismatique est perçu comme plus compétent stratégiquement, alors que charisme et compétence stratégique sont relativement indépendants.

**Contre-mesure** :
- Pour chaque sous-question, repartir d'une base rate indépendante.
- Éviter de lire l'analyse narrative en début de processus — biaise les estimations subséquentes.

---

## Procédure de vérification anti-biais (à appliquer avant finalisation)

Avant de finaliser une fiche de prédiction, exécuter cette checklist :

```
□ Mes scénarios sont-ils MECE ? (test à l'étape 6)
□ Quel poids ai-je donné au statu quo / à la continuation ?
   S'il est faible, est-ce justifié par des indicateurs forts ?
□ Mon ajustement inside view est-il ≤ 20 points (seuil d'alerte interne) ?
   Sinon, l'écart est-il justifié explicitement ?
□ Quel serait mon Brier score attendu sur 50 prédictions similaires ?
□ Ai-je formulé l'argument du scénario opposé ?
□ Mes probabilités sont-elles explicites, dans [1 % ; 99 %],
   et justifiées si hors de [5 % ; 95 %] ?
□ Chaque chiffre cité (taux de base, statistique) a-t-il une source ?
□ Mon estimation finale serait-elle modifiée si je n'avais pas lu
   les sources tendancieuses en amont ?
□ Quelqu'un de tempérament opposé donnerait-il un chiffre très différent ?
□ Ai-je un événement saillant récent qui pourrait gonfler mes probabilités ?
```

Si une case n'est pas validée, **revisiter** l'étape correspondante avant de finaliser.

---

## Note sur l'apprentissage des biais

Les biais cognitifs **ne disparaissent pas par la connaissance**. Connaître l'overconfidence ne suffit pas à l'éliminer.

Ce qui marche, selon les travaux du Good Judgment Project (Mellers et al., 2014 ; Chang et al., 2016) et la littérature sur la débiaisation :
1. **Mesure répétée** (`calibration-engine`) — voir ses propres patrons.
2. **Pratique délibérée** — répéter la discipline sur 50-100 prédictions.
3. **Feedback** — confronter ses prédictions à la réalité.
4. **Comparaison avec pairs** — autres forecasters disciplinés.

Sans ces conditions, la liste de biais ci-dessus reste théorique. C'est précisément pourquoi le `calibration-engine` est indispensable.

