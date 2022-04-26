---
tags: dsplus,documentation
title : Introduction
description: Introduction
---

# DSPLUS

Un outil en ligne de commande pour interagir avec DataStage et simplifier la mise en place d'une chaine CI/CD pour DataStage.


## Fonctionalités

* Requêter les objets d'un projet
* Extraire ou générer les informations d'un objet
    * Export
    * Métadonnées
    * Capture d'écran
    * Code source
    * Checksum
    * Arbre syntaxique
    * Documentation
* Versionner un objet
* Synchroniser avec un système de gestion de révisions
* Packager un ensemble d'objets en un artefact
* Déployer un artefact sur un projet
* Publier un artefact sur un gestionnaire d'artefacts
* Contrôler le respect de normes de qualités
* Configurer un projet


## Syntaxe

```
dsplus commande [options]
```

Les options sont spécifiées au format long ```--option valeur``` ou court (suivant les options) ```-o valeur```

Les options à valeurs multiples sont spécifiées de la manière suivante:

```--option valeur1 valeur2```

Les syntaxes ci-dessous sont acceptées:


```
--option=valeur
--option valeur1 --option valeur2
```

Les options aux format court sont combinables
```
-o -x
-ox
```



## Installation

Placer l'exécutable correspondant au système dans un répertoire faisant partie du PATH.

## Commandes

Les commandes reconnues par défauts sont:

* **projects** : lister les projets
* **list** : lister les objets d'un projet
* **get** : extraire les information d'un objet d'un projet
* **init** : extraire les informations de tous les objets d'un projet
* **status** : comparer un projet avec un repository local
* **package** : packager les objets d'un repository local
* **deploy** : déployer un package vers un projet
* **quality**: controler le respect de normes de qualité
* **coverage**: état des tests
* **configure**: appliquer une configuration sur un projet
* **publish**: publier un package sur un gestionnaire d'artefacts
* **current**: afficher les packages déployés sur un projet


## Options
### Générales

Ces options s'appliquent à la plupart des commandes

Option | Courte | Type |  Description
---|---|---|---
help | h | bool |  Afficher l'aide
domain| d | chaîne | Adresse du serveur applicatif et le port (format host:port)
server| s | chaîne | Adresse du moteur DataStage
username | u | chaîne | Utilisateur
password | p | chaîne | Mot de passe de l'utilisateur
config | | chaîne | chemin vers un fichier de configuration
env | | chaîne | Un environnement défini dans le fichier de configuration
project | P | chaîne | Nom du projet DataStage
target | | chaîne | Chemin vers un dossier cible local
verbose | v | bool | Affichage plus verbeux
output | o | bool | Ecrire les informations dans le dossier cible
format | f | chaîne | Format de la sortie standard, par défaut du json "pretty printed", les formats possibles: table, mtable (format markdown), csv, json, html (pour certains cas)
query | | chaîne | requête à appliquer à la sortie standard, soit au format sql: "select * from ?" soit au format jsonata (https://jsonata.org/)

### Informations

Ces options s'appliquent à la commande get et indiquent quelles informations sont à extraire ou générer

Option | Courte | Type |  Description
---|---|---|---
metadata | m | bool |  Métadonnées
code |c | bool |  Code source
image | i | bool |  Capture d'écran
export | x | bool |  Export isx
checksum | k | bool |  Checksum
ast | | bool |  Arbre syntaxique
doc | | bool |  Documentation
server| | bool | Hostname du moteur
project|| bool | Nom du projet
run | r | bool |  Informations sur la dernière execution (nécessite que l'operation console soit active)

### Options spécifiques
#### list
Option | Courte | Type |  Description
---|---|---|---
info  |  | chaîne |  Informations à lister
filter | | chaîne | Clause de filtrage (syntaxe de where sql)



#### package

Option | Courte | Type |  Description
---|---|---|---
git | g | bool | Le repository est de type git
mode | | chaîne |  FULL ou DELTA
version | | chaîne/array | Révisions git
pack | | chaîne | Nom du package

#### deploy

Option | Courte | Type |  Description
---|---|---|---
git | g | bool | Le repository est de type git
pack | | chaîne | Nom du package

## Fichier de configuration

Il est recommandé de mettre en place un fichier de configuration adapté à l'environnement et à l'usage souhaité. Cela permetra de simplifier les commandes. 

Le fichier est peut-être au format, YAML, JSON ou [TOML](https://github.com/toml-lang/toml), on peut y spécifier toutes les options dans les sections et sous-sections:

* defaults
* envs
    * *env*

Les options générales sont définies dans la section defaults on peut définir ensuite des environnements pour les options qui varieraient entre environnement.

En cas d'option définie de manière multiple la priorité est la suivante:
Ligne de commande > env > defaults

* Exemple au format yaml:
```yaml
defaults:
  dspath: "C:/IBM/InformationServer"
  domain: "localhost:9446"
  server: IS-ENGINEDOCKER
  username: isadmin
  password: "password"
```
* Exemple au format toml:
```toml
[defaults]
  dspath="C:/IBM/InformationServer"
  domain="localhost:9446"
  server=IS-ENGINEDOCKER
  username=isadmin
  password="password"
```

## Formats de sortie

L'outil produit en fonction des commandes des informations:

* Dans des fichiers plats
* Sur la sortie standard

Les fichiers plats sont en général produit lors des commandes `get` ou `init` lorsque l'option `output` est à `true`.

La sortie standard peut être de plusieurs types:

* Informations d'éxecutions (commandes `init/package/deploy`)
* JSON ou multi-json (commandes `list/get(metadata,ast,manifest,current,status)`)

Lorsque la sortie est de type JSON on peut utiliser l'option `query` pour la formater. On peut également indiquer l'option `format`.
Il est également possible de développer des formateurs personnalisés pour produire du html ou du markdown par exemple.


