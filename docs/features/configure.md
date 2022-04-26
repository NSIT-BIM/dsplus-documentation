---
tags: dsplus,documentation
title : configure
description: Configuration d'un projet
---


# Configure

Applique la configuration déclarée dans le fichier `project.yml` à un projet.
Cette configuration peut concerner les variables d'environnement ou les propriétés du projet.


## Syntaxe

```
dsplus configure --project Projet
```

## Fichier project.yml

2 types de données sont prises en compte par cette commande:

* env: variables d'environnements
* properties: propriétés

### env

Chaque variable doit être définie de la manière suivante:

```yaml
NomVariable:
  value: Valeur
  type: STRING|ENCRYPTED
  prompt: Libellé
```

## Format de sortie

Pas de sortie produite.

## Exemples

