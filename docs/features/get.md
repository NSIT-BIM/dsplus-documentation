---
tags: dsplus,documentation
title : get
description: extraire
---

# Get

Obtenir des informations sur ou exporter un objet.


## Syntaxe

```
dsplus get --AssetType NomObjet [--options]
```

## Options

Les types d'objets (AssetType) possibles:

* job
* routine
* container
* tabledef
* paramset
* stage
* dataconnection

Les options possibles:

* metadata : extraire les métadonnées techniques de l'objet 
* info : les métadonnées à extraire
* code : code source
* image : capture d'écran
* export : export isx
* ast : représentation json du job
* doc : documentation markdown de l'objet
* checksum: hash de l'objet
* run : informations sur la dernière exécution du job (nécessite que l'operation console soit active)
* output : écrire les informations extraites dans des fichiers
* target : racine de la cible pour les fichiers
* git : indexe l'objet
* verbose: affiche les informations extraites dans la sortie standard


L'option **info** s'applique à l'option **metadata** et peut prendre les valeurs:

* category
* name
* type
* jobType
* RID
* modificationTimestamp
* modifiedByUser
* creationTimestamp
* createdByUser
* isSystem
* shortDescription
* project
* server
* **all** équivaut à toutes les valeur précédentes


!!! info
    En cas d'écriture de ces informations en fichier plats, ceux-ci sont placés dans la cible sous l'arborescence ```category/name/name.extension```.
    Par défaut la racine de la cible est le répertoire courant ou la racine du repository git si on se trouve dans un repository git. On peut définir la cible avec l'option `target`.
    Le format de l'arborescence peut être défini par la variable d'environnement `DSP_TARGETFORMAT`. Par exemple si on veut ajouter la notion de projet:
    `[project]/[category]/[name]/[name]`.
    Les paramètres possibles sont:
    
    * name
    * category
    * server
    * project
    * type (job/routine...)
    * ext (pjb/sjb...)
    * Y: Année de dernière modification
    * M: Mois de dernière modification
    * D: Jour de dernière modification
    * H: Heure de dernière modification
    * m: Minute de dernière modification


## Format de sortie

La commande est silencieuse à moins d'activer l'option `--verbose`.
Dans ce cas le format dépend des informations produites et sera multi-format:

* metadata : json 
* code : xml/texte
* ast : json
* doc : markdown
* checksum: texte
* run : json



## Exemples




