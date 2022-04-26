---
tags: dsplus,documentation
title : manifest
description: Affiche le manifest d'un package
---


# Manifest

Affiche le manifeste d'un package.


## Syntaxe

```
dsplus manifest --pack Package.isx
```

## Format de sortie

La sortie est au format json et contient l'intégralité du manifeste:

* infos: Information sur le package (mode, date, révision git, remote, version...)
* checksum: checksums des objets datastage
* metadata: métadonnées des objets datastage
* ds: liste des objets datastage
* configuration: configuration projet
* externals: lists des objets externes

## Exemples

