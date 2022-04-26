---
tags: dsplus,documentation
title : current
description: Version courante d'un projet
---


# Current

Produit les information de version d'un projet:

* name: nom de l'artefact
* repository: nom de la racine de l'artifact (en cas d'utilisation d'un gestionnaire d'artefacts)
* git: revision git
* mode: mode de constitution du package (FULL/DELTA)
* remote: url du repository git d'origine
* created: date de constitution du package
* deployed: date de déploiement
* version: version déclarée à la constitution du package

!!! info
    Cette commande peut être utilisée si les déploiements sont faits avec l'option `trackversions` activée.


## Syntaxe

```
dsplus current --project Projet [--verbose]
```

## Format de sortie

Sortie au format `JSON`.

## Exemples

