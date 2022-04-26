---
tags: dsplus,documentation
title: Fichier de configuration
description: Fichier de Configuration
---

# Fichier de configuration

L'utilisation d'un ou plusieurs fichiers de configuration permet de simplifier grandement les commandes ainsi que d'étendre les possibilités de l'outil.

## Emplacement et nom par défaut

* L'outil cherche à charger par défaut le fichier ```$HOME/dsplus.[ext]```.
* Cet emplacement peut être surchargé par la variable d'environnement ```DSP_CONFIG```
* Ou indiqué à l'exécution par l'option ```--config```


## Format et structure

Le fichier peut être aux formats: yaml, [toml](https://github.com/toml-lang/toml), ou json.

L'extension peut être donc:

* yml/yaml
* cfg (format toml)
* json

=== "yaml"
    ``` yaml
    defaults:
    dspath: "C:/IBM/InformationServer"
    domain: "adresseDomaine:portDomain"
    server: "adresseServeur"
    username: "userDataStage"
    password: "motDePasseDataStage"
    ```

=== "toml"
    ``` toml
    [defaults]
    dspath="C:/IBM/InformationServer"
    domain="adresseDomaine:portDomain"
    server="adresseServeur"
    username="userDataStage"
    password="motDePasseDataStage"
    ``` 

=== "json"
    ```json
    {
    "defaults": {
        "dspath": "C:/IBM/InformationServer",
        "domain": "adresseDomaine:portDomain",
        "server": "adresseServeur",
        "username": "userDataStage",
        "password": "motDePasseDataStage"
        }
    }
    ```

!!! tip
    On recomandera de préférence les formats yaml ou toml ceux-ci permettant notamment l'ajout de commentaires contrairement au json.

### Structure et Sections

Les sections définies et hiérarchisées ainsi sont possibles:

* defaults
* envs
    * *Nom Env*
* security
* dependencies
* plugins
* shortcuts
* filters

Les paramètres définis dans les section ```envs``` surchargent ceux définis en ```defaults``` et sont eux-mêmes surchargés par les options de la ligne de commande.

Lors de l'exécution de la commande on fait référence à l'environnement via l'option ```env``` ou en valorisant une exportant d'environnement ```env```.



## Options avancées

### Filtres

L'options ```filter``` permet déjà de filtrer les objets par une clause syntaxe sql. 
Dans certains cas on peut vouloir cumuler des filtres prédéfinis pour un environnement avec des personnalisés à l'appel.
Le fichier de configuration accepte en sous-section des environnements une section ```[filters]``` qui autorise des expressions régulières:




### Raccourcis

Il est possible de définir dans le fichier de configuration des alias ou des raccourcis afin de simplifier ou personnaliser son utilisation.

On les définis dans la section ```[shortcuts]``` par les commandes et options que l'on souhaite.

Exemple de 2 alias (avec différentes syntaxes):


On obtient ainsi les équivalances suivantes:



### Plugins

Il est possible de définir dans le fichier de configuration des plugins à exécuter dans certains contextes et évènements.
Voir la section dédiée pour plus de détails.



# Options spéciales

Les options ci-dessous ne sont pas modifiable par ligne de commande mais peuvent être modifiées par fichier de configuration, variable d'environnement ou configuration git.

*Certaines de ces options peuvent nécessité une assistance.*


Option | Commande | Type |  Description | Défaut
---|---|---|---|---
maxget | init | int |  Nombre d'opérations en parallèle | 10
maxexport | init | int | Nombre d'asset par batch d'export | 50
rollback | deploy | bool |  Produit un isx des assets modifiés avant de les écraser (mode FULL)
deletes | deploy | bool | Supprime les assets supprimés de git
deletes | git/init | chaine | Format et destination (avec <code>target</code> comme racine) des fichiers produits. Syntaxe avec des placesholders. | [category]/[name]/[name]
extdir | package | chaine | Répertoire à la racine du repository git contenant des assets externes non-datastage à packager/deployer | external
exttar | package | bool | les assets externes sont d'abord réunis en un tar avant d'être packagés.
customparser | get | chaine | chemin vers un fichier pour personnaliser le parser qui génère la représentation json du job
compilation | get/init/package | bool | active la vérification de compilation du job

#