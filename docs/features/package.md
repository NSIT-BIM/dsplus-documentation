---
tags: dsplus,documentation
title : package
description: Packager
---

# Package
Packager un ensemble d'objets depuis un dossier ou un repository.

## Syntaxe

```
dsplus package --mode DELTA|FULL --pack pack.isx  [--git --version]
```

## Options

* mode : mode de packaging complet (FULL), ou uniquement les objets modifiés entre 2 révisions (DELTA)
* pack : nom du fichier produit (format isx)
* git : indique que le repository est du type git
* version:
    * si mode FULL: révision git à packager (commit, tag, branche)
    * si mode DELTA: modifications entre 2 révisions


## Objets externes

Les fichiers (paramétrages, scripts etc...) présents dans le sous-dossier `external` du repository seront également packagés.

!!! info
    On peut spécifier un autre nom de sous-dossier via l'option `extdir` ou la variable d'environnement `DSP_EXTDIR`.


## Manifeste

Un package produit avec dsplus contient également un manifeste décrivant les informations ci-dessous:

* Informations du package:
    * version
    * revision git
    * mode (FULL/DELTA)
    * date de packaging
    * repository git distant (si possible)
* Checksums des objets datastage
* Métadonnées des objets datastage
* En mode FULL:
    * liste des objets datastage
    * liste des objets externes
* En mode DELTA:
    * liste des objets datastage créés
    * liste des objets datastage modifiés
    * liste des objets datastage supprimés
    * liste des objets externes créés
    * liste des objets externes modifiés
    * liste des objets externes supprimés
* La configuration projet si elle existe

Le manifest est au format json et peut être affiché via la commande:
`dsplus manifest --pack Package.isx`

## Format de sortie

La sortie est la liste des objets packagés au format `json`.