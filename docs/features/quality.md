---
tags: dsplus,documentation
title : quality
description: Contrôler la qualité
---


# Quality

Vérifie le respect des normes et bonnes pratiques des objets d'un projet.

Des règles standards sont précodées et seront appliquées par défaut. Il est possible de définir des règles ou de modifier les règles standards.

Produit les informations suivantes:

* rule: nom de la règle
* expected: résultat attendu
* pass: réussite du test (peut être un booléen ou une liste d'objets)
* fail: échec du test (peut être un booléen ou une liste d'objets)
* categories: categories de la règle (bug, performance, maintenabilité, bonnes pratiques etc...)
* severity: sévérité du test (information, mineure, majeure, critique)
* message: message informatif
* name: nom de l'objet testé
* category: catégorie de l'objet testé
* criticity: niveau de criticité



## Syntaxe

### Dynamique

Pour analyser directement le projet:
```
dsplus quality --project Projet [options]
```

La commande et les options sont similaires à la commande `list`

### Statique

Pour analyser des objets extraits dans un repository, pour une utilisation dans une chaîne CI/CD sans dépendances avec une infrastructure DataStage.

```
dsplus quality --external Category/Job
```

Supporte le globing, par exemple pour analyser tout le repository:
```
dsplus quality --external "**"
```
```
dsplus quality --external "Category/**"
```

!!! info
    ** pour une traverse recursive
    \* pour tous les objets du répertoire


!!! warning
    Pour que ces analyses statiques fonctionnent correctement il est nécessaire que le repository contiennent les métadonnées, la représentation syntaxique et les informations de dernière executions des objets. Soit lors d'un `dsplus get` ou `dsplus init` les options:
    --metadata
    --info name type jobType
    --ast
    --run
    --output


## Format de sortie

La sortie par défaut est au format `json`.


### Formateurs additionnels

* html: l'option `--html` produit un rapport html
* Code Climate: l'option `codeclimate/DSP_CODECLIMATE` produit la sortie suivant le standard Code Climate (peut être combiné avec le format html)


## Exemples

