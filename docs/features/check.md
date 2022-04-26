---
tags: dsplus,documentation
title : check
description: Vérifier l'intégrité d'un package
---


# Check

Vérifier l'intégrité d'un package contre un projet.

Lorsque le checksums des objets d'un repository est présent, celui-ci est intégré au manifeste lors du packaging.
Avec cette commande on peut vérifier l'intégrité d'un package contre un projet après un déploiement.

!!! warning
    A l'heure actuelle cette commande ne fonctionne pas pour les parameterSets.


## Syntaxe

```
dsplus check --pack Pack.isx --project Projet [--verbose]
```



## Format de sortie

La sortie est au format json/texte:

* La liste des objets dont le checksum ne correspond pas au projet au format json (avec l'option `--verbose` tous les objets du package sont listés):
    * asset: nom de l'objet
    * type: type de l'objet
    * csum1: le checksum de l'objet dans le package
    * csum2: le checksum de l'objet dans le projet
    * modificationTimestamp: date de modification de l'objet dans le projet
    * modifiedByUser: utilisateur ayant effectué la dernière modification
* Le statut de la vérification au format texte

En cas de non intégrité la commande fini en erreur.

## Exemples

