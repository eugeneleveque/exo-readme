# GitFlow

### Branches principales

- **Branche `main`/`master`** : Destinée à être déployée en production (ou préproduction/test, etc.).
- **Branche `develop`** : Branche sur laquelle personne ne travaille directement. Toutes les branches de features sont fusionnées (mergées) ici.

### Branches secondaires

- **Branche `feature`** : Une branche par feature. Une fois la feature terminée, une Pull Request (PR) est ouverte pour `develop`, afin que le travail soit validé par l'équipe ou les personnes concernées.
- **Branche `hotfix`** : Utilisée pour corriger rapidement des bugs critiques en production. Une fois le hotfix validé, il est fusionné à la fois sur `main` pour résoudre le bug en production, et sur `develop` pour que cette branche soit à jour.

### Workflow

1. Lorsqu'une étape est franchie (par exemple, à la fin d'un sprint), un **tag** est ajouté à la branche `develop`. Ce tag correspond à une version de l'application.
2. Une fois validé, ce tag est déployé sur la branche `main`/`master` et devient une version officielle de l'application.

### GitFlow : l'outil

GitFlow est un outil créé pour simplifier l'utilisation de cette méthodologie grâce à de nouvelles commandes.

#### Initialisation

Pour initialiser la branche `develop` :
git flow init

Cela demandera par la même occasion de définir les noms des branches utilisées (par défaut ci-dessous) :

- develop : pour fusionner toutes les features.
- main/master : pour la production.
- feature : pour ajouter des nouvelles fonctionnalités.
- release : pour taguer une version en production.
- hotfix : pour effectuer des correctifs urgents.


#### Travailler sur une nouvelle feature

Pour démarrer une nouvelle feature :

``git flow feature start [nom_de_la_feature]``

Ensuite, on effectue autant de commits que nécessaire pour réaliser cette feature. Une fois la feature prête, qu'elle a passé la PR, les tests, et autres vérifications, on peut la terminer avec :

``git flow feature finish [nom_de_la_feature]``

Cela aura pour effet de supprimer la branche localement.

#### Effectuer une release

Pour réaliser une release à partir de la version actuelle de **develop** :

``git flow release start v0.0.1``
``git flow release finish``


#### Effectuer un hotfix

Pour commencer un hotfix :
`git flow hotfix start [nom_du_hotfix]`
`git flow hotfix finish`

### Processus de tagging et versioning

Les versions de l'application sont taguées en suivant la convention **SemVer** (Versionnage Sémantique) :

- **MAJOR** : Incrémenté pour des changements importants ou rétro-incompatibles.
- **MINOR** : Incrémenté pour des ajouts de nouvelles fonctionnalités tout en restant rétro-compatibles.
- **PATCH** : Incrémenté pour des corrections de bugs mineurs ou des petites améliorations.

Par exemple : 
- `v1.0.0` : Première version majeure.
- `v1.1.0` : Nouvelle fonctionnalité ajoutée.
- `v1.1.1` : Correction d'un bug mineur.

Les tags sont ajoutés lors des releases, après validation des PR. Cela permet de tracer les différentes versions de l'application.

### Revue des Pull Requests (PR)

Avant de fusionner une branche `feature` ou `hotfix` dans `develop` ou `main`, un code review est indispensable. Voici les étapes recommandées :

1. **Création de la PR** : Une fois la feature ou le hotfix terminé, on crée une PR vers la branche cible (`develop` ou `main`).
   
2. **Revue par les personnes concernées** : Chaque PR doit être revue par au moins deux personnes de l'équipe, ou des membres désignés comme responsables de la validation des PRs.
   
3. **Validation des tests** : Avant de fusionner, les tests automatiques doivent être valides (tests unitaires, intégration, etc.).
   
4. **Fusion et suppression de la branche** : Une fois la PR validée et les tests passés, la branche est fusionnée, puis supprimée localement et sur le dépôt distant.

Cela garantit la qualité du code et évite l'introduction de bugs en production.

