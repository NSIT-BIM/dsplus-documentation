---
tags: dsplus,howtos
title : Automatisation
description: Quickstart dsplus
---

# Automatisation



Les raccourcis et l'intégration au designer permettent d'industrialiser  et simplifier certaines parties du worflow. Mais pour l'instant il ne s'agit que aspects liés à DataStage, les opérations git restent à effectuer, il y a plusieurs manières pour cela:

* Lignes de commandes git classiques
* Clients git graphique

Cela restant des opérations essentiellement manuelles, nous allons voir comment il est possible de les déclencher automatiquement avec les plugins dsplus.



## Plugins dsplus

Comme pour les raccourcis, on définit les plugins dans le fichier de configuration.
Ici on veut déclencher automatiquement tout ou une partie de l'enchaînement suivant:

```bash
git status
git add .../job
git commit -m "commentaire"
git push
```

Les plugins dsplus peuvent être de 2 types:

* javascript
* commandes arbitraires

### Déclaration

Ce tutorial décrit la mise en place d'une commande arbitraire.

Pour déclarer un plugin on doit définir:

* son type: ici, bin
* le programme/commande
* les arguments: un tableau d'arguments qui seront passés à la commande. Ceux ci sont templatables.
* l'événement déclencheur du plugin: ici la fin de la commande get se traduire donc par "end:get"
* le contexte dans lequel le plugin se déclenchera: ici lors de l'appel à la commande get, pour simplifier et éviter le déclenchement intempestif on choisi de lier la plugin au raccourcis créée précédemment en ajoutant une option au contexte.

Pour le programme pour des raisons de facilité et portabilité on choisi de lancer la commande bash, les arguments sont le contenu du script qu'on souhaite lancer.

La déclaration ci-dessous fera qu'après avoir lancé la commande (en ligne de commande ou via le designer):
```
dsplus git --job ... 
```
L'enchaînement suivant se fera automatiquement:

* on se place dans le dépôt,
* vérification du statut,
* ajout des éléments du job
* vérification du statut,
* commit, avec comme commentaire la 1ère ligne de la description longue
* attente (pour éviter la fermeture de la fenêtre si appel depuis le designer)


``` yaml
plugins:
  autogit:
     type: bin
     program: bash 
     args: [ '-c', 
     'cd "${options.target}" && 
      git status "$(dirname "${file}")" && 
      git add "$(dirname "${file}")" index.json && 
      git status && 
      git commit -m "dsplus: $(echo "${assetmetadata.longDescription}" | head -1)" &&
      read
      ' 
      ]
     event: "end:get"
     context: 
        get:
          autogit: true

shortcuts:
  git:
    get:
      ast: true
      metadata: true
      image: true
      export: true
      doc: true
      git: true
      output: true
      autogit: true
```


!!! info
    Git permet également des raccourcis (alias), son extension (custom subcommands), ou de l'automatisation (git hooks).
    Ces fonctionnalités peuvent être utilisées telles-quelles ou combinées avec dsplus. 
