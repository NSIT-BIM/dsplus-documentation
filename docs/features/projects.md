---
tags: dsplus,documentation
title : projects
description: Lister les projets
---


# Projects

Produit la liste des projets.

## Syntaxe

```
dsplus projects  
```



!!! info

    Prérequis: les paramètres suivant doivent être prédéfinis dans le fichier de configuration (ou ajoutés en arguments à la ligne de commande):
    
    - domain
    - username
    - password


## Format de sortie

La sortie est au format `json`

## Exemple

```
dsplus projects  
```
```json
[
  {
    "name": "ANALYZERPROJECT",
    "dsServerName": "IS-EN-CONDUCTOR-0.EN-COND",
    "portNumber": 31538
  },
  {
    "name": "dstage1",
    "dsServerName": "IS-EN-CONDUCTOR-0.EN-COND",
    "portNumber": 31538
  },
  {
    "name": "dstage2",
    "dsServerName": "IS-EN-CONDUCTOR-0.EN-COND",
    "portNumber": 31538
  }
]
```