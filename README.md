# git-workflow-lite

Afin de pouvoir travailler en équipe sur vos projets avec GIT, je vous propose un workflow "lite" avec un ensemble de tips pour vous aider à gérer les différentes situations dans lesquelles vous risquez de vous trouver.

Nb :
* Les captures d'écran ont été réalisées avec [SourceTree](https://www.sourcetreeapp.com/).
* Le repository de demo est accessible par ici : *TODO*

***

## Résultat attendu

Tout d'abord, voici un aperçu de ce à quoi devrait ressembler votre historique : 

![flow1](https://raw.githubusercontent.com/ben-barbier/git-workflow-lite/master/pictures/flow1.png)

Vous pouvez remarquer que toutes les features (branche) partent de la même branche source (master) et finissent par rejoindre cette même branche.

## 1. Développer une feature (cas classique)

Pour développer une nouvelle feature, il faut tout d'abord commencer par créer une nouvelle branche (`git branch feature3`) avant de se positionner dessus (`git checkout feature3`).

![flow2](https://raw.githubusercontent.com/ben-barbier/git-workflow-lite/master/pictures/flow2.png)

Une feature sera donc réalisée sur une branche à part et contiendra un ensemble de commits.

Pour créer le premier commit :

    touch file3.txt
    git add file3.txt
    git commit -m "feat(feature3): add file3.txt"

![flow3](https://raw.githubusercontent.com/ben-barbier/git-workflow-lite/master/pictures/flow3.png)

Puis pour créer les deux suivants :

    touch file3-1.txt
    git add file3-1.txt
    git commit -m "feat(feature3): add file3-1.txt"
    
    touch file3-2.txt
    git add file3-2.txt
    git commit -m "feat(feature3): add file3-2.txt"

![flow4](https://raw.githubusercontent.com/ben-barbier/git-workflow-lite/master/pictures/flow4.png)

Une fois la feature terminée, c'est à travers *GitLab* qu'il faut demander son intégration à la branche source (Merge Request).

Après validation par un autre membre de l'équipe (revue de code), la branche `feature3` est "mergée" sur la branche `master` :

![flow5](https://raw.githubusercontent.com/ben-barbier/git-workflow-lite/master/pictures/flow5.png)

## 2. Développer une feature (en équipe)

Dans le cas d'un travail en équipe, plusieurs features sont constamment en cours de développement sur autant de branches. Prenons l'exemple suivant :
* Vous travaillez sur la feature 5 (branche `feature5`)
* Un membre de votre équipe travaille sur la feature 4 (branche `feature4`)

Voici à quoi devrait ressembler votre historique :

![flow6](https://raw.githubusercontent.com/ben-barbier/git-workflow-lite/master/pictures/flow6.png)

Apres l'exécution d'un processus classique de merge (voir [partie 1](#1-développer-une-feature-cas-classique)), la branche `release4` est mergée sur la branche `master`.

![flow7](https://raw.githubusercontent.com/ben-barbier/git-workflow-lite/master/pictures/flow7.png)

Jusqu'ici, aucun conflit n'était possible. Ce n'est à présent plus le cas. En effet, la branche `feature4` fraichement mergée sur la branche `master` a trés bien pu modifier les mêmes fichiers que ceux que vous avez modifiés sur votre branche `feature5`.

C'est donc à ce moment que vous devez gérer les conflits.

Pour ce faire, il vous faut réaliser un `rebase` de votre branche `feature5` sur la branche `master`.

    git rebase master

Lorsque vous exécuterez cette commande, git va exécuter vos commits (ici `55f633c`, `0d951ed` et `9ebacbf`) à la suite de la branche master.

GIT vous notifiera des conflits (s'il y en a) pour l'exécution de chacun des commits.

Pour lancer l'outil de gestion des conflits, il faut lancer la commande :

    git mergetool 

Une fois les conflits gérés, vous obtiendrez un historique comme celui-ci :

![flow8](https://raw.githubusercontent.com/ben-barbier/git-workflow-lite/master/pictures/flow8.png)

Vous pouvez maintenant à votre tour faire une "merge request" via GitLab (voir [partie 1](#1-développer-une-feature-cas-classique)) et obtenir un historique comme celui-ci après validation de votre "merge request" par votre équipe :

![flow9](https://raw.githubusercontent.com/ben-barbier/git-workflow-lite/master/pictures/flow9.png)

***

Made with :heart: by @ben-barbier
