---
tags: dsplus,documentation
title : publish
description: Publier un package sur un gestionnaire d'artefacts
---


# Publish

Publie un package sur un gestionnaire d'artefacts (Artifactory, Nexus...).


## Syntaxe

```
dsplus publish --pack Package.isx
```

## Configuration

Il est nécessaire de configurer le ou les gestionnaires en fonction de leur api:

* registry: définition du nom du gestionnaire par défaut
* dependencies:
  * *registry* : nom du gestionnaire
    * uri: Endpoint de l'api ou de la racine du dépôt 
    * path: emplacement des packages
    * options: options pour l'api (authentification etc...) 

Les options uri et path acceptent des placeholders au format `[[parametre]]`.

## Format de sortie

La sortie est de type texte.

## Exemples

