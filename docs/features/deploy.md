---
tags: dsplus,documentation
title : deploy
description: Deployer
---

# Deploy

Deploie des exports ou des packages vers un projet


## Syntaxe

```
dsplus deploy --pack pack.isx/--isx export.isx --project Project
```

## Options

* pack : nom du package à déployer
* isx: nom de l'export isx à déployer
* project : nom du projet cible


## Objets externes

Si le package contient des objets externes ils seront déployés dans le répertoire courant par défaut ou dans celui défini par l'option `target`.

## Options spéciales

* rollback: en mode DELTA, un export de sauvegarde est fait avant de déployer
* deletes: les objets supprimés du repository source sont supprimés du projet cible
* trackversions: intègre au projet des informations issues du manifeste

Ces options sont toutes de type booléennes et peuvent être spécifiées soit dans le fichier de configuration soit via les variables d'environnement: DSP_ROLLBACK, DSP_DELETES, DSP_TRACKVERSION


## Vérifier l'intégrité d'un package déployé

Si les checksums des objets étaient présents au moment du packaging, ceux-ci seront dans le manifeste et pourront être comparés contre un projet avec la commande `dsplus check`:
`dsplus check --pack pack.isx --project Project`

## Format de sortie

La sortie est de type informationnelle.