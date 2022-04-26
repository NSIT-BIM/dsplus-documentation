---
tags: dsplus,documentation
title : status
description: Comparaison avec un index
---


# Status
Compare l'état d'un projet avec un index à la racine d'un repository ou dans le répertoire courant.

Produit le même type de sortie que la commande **list** mais avec une coloration:

* vert: objets ajoutés dans le projet
* bleue: objets modifiés
* rouge: objets supprimés dans le projet

!!! info
    L'index est un fichier nommé `index.json` celui-ci est produit ou mis-à-jour lorsque l'option `--git` est active avec les commandes `dsplus init` ou `dsplus get`.



## Syntaxe

```
dsplus status --project Projet
```

## Format de sortie
La sortie est au format mixte `multi-json` et informationnel.

## Exemples

