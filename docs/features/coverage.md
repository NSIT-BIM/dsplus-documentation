---
tags: dsplus,documentation
title : coverage
description: Extraction du taux de tests
---


# coverage

Extrait le taux de tests d'un projet.
Cette commande produit 3 informations:

- Taux de jobs réussis
- Taux de jobs en échec
- Taux de jobs non testés

Peut être appliquée directement à un projet ou pour vérifier le taux de tests d'un package contre un projet.

!!! info
    Un test est considéré réussi si le job a été exécuté correctement après sa dernière modification. 



## Syntaxe

```
dsplus coverage --project [--pack] [--verbose] [options]
```

Avec l'options verbose la liste complète des objets concernés est produite avec les information suivantes:

- Nom
- Date de modification
- Date d'exécution
- Statut
- Temps d'exécution
- Erreurs

### Projet

```
dsplus coverage --project Projet
```

Le périmètre vérifié est celui que renverrais la commande `dsplus list`, la même syntaxe s'applique.

### Package
```
dsplus coverage --pack Pack.isx --project Projet
```


## Format de sortie

La sortie est au format `json`.


### Formateurs additionnels

Avec l'option `--format junit` les informations sont produites au format xml standard de *junit*.

## Exemples

