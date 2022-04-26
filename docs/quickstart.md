---
tags: dsplus,howtos
title : Quickstart
description: Quickstart dsplus
---

# Quickstart
## Préparation
### Installation

1- Télécharger la dernière version de dsplus: https://d2ifpxp0ekyv6p.cloudfront.net/dsplus/latest/windows/dsplus.exe

2- Placer le binaire dans un répertoire spécifique

3- Ajouter le répertoire au PATH de l'utilisateur

![env](https://i.imgur.com/oQxicMI.png){ align=left }
![](https://i.imgur.com/mykGYaf.png)
![](https://i.imgur.com/KItdVlF.png)

### Configuration basique

Créer le fichier `dsplus.yml `et l'enregistrer dans `C:/Users/IdUser/` avec le contenu ci-dessous en modifiant les valeur de manière adéquate:

```yml
defaults:
  dspath: "C:/IBM/InformationServer"
  domain: "adresseDomaine:portDomain"
  server: "adresseServeur"
  username: "userDataStage"
  password: "motDePasseDataStage"
```

* dspath: emplacement de l'installation du client DataStage
* domain, serveur, username, password: identification du serveur et utilisateur DataStage. Pour référence, l'équivalent lors de la connexion avec un client lourd:

![](https://i.imgur.com/Eo1Sq78.png)

!!!info
    L'emplacement et le nom du fichier de configuration dans l'exemple sont ceux par défaut. Il est possible de le placer et le nommer autrement et ensuite d'y faire faire référence avec l'argument de ligne de commande `--config` ou via la variable d'environnement `DSP_CONFIG`.


!!!info
    Dans l'exemple le mot de passe est enregistré en clair dans le fichier de configuration. Celui-ci peut être encrypté (copier/coller l'intégralité de la sortie produite dans le fichier de configuration):
    ````bash
    dsplus encrypt --password motDePasseDataStage
    ````
    Le mot de passe peut aussi être enregistré en clair ou en crypté dans la variable d'environnement `DSP_PASSWORD` ou passé à chaque appel à `dsplus` via l'argument `--password`.


### Validation

Pour vérifier que tout fonctionne correctement ouvrir une invite de commande (ou powershell ou de préférence git bash) et entrer les commandes suivantes:
````bash
dsplus version
dsplus projects
````

!!! info
    On recommande l'utilisation de Git Bash pour les améliorations qu'il apporte: complétion, coloration et surtout prompt enrichi.


## Versionner des objet DataStage
### Créer ou copier un dépôt Git

Pour commencer à versionner des objets DataStage sous Git, il faut d'abord un dépôt Git.

* On peut le créer:
````git
git init demoProject
cd demoProject
````

* Ou bien on peut cloner un dépôt distant existant sur Azure DevOps:
````git
git clone http://adressedemoProject.git
cd demoProject
````

* Créer une branche:
````git

git checkout -b myBranch
````

### Configurer le dépôt

Certaines options dsplus sont à activer si ou souhaite l'ensemble de fonctionnalités. On peut le faire toujours via le fichier de configuration ou les variables d'environnement, pour plus de souplesse on le fait ici via la configuration locale du dépôt git:

1- Lier le dépôt à un projet spécifique:
````git
git config dsplus.project demoProject
````

!!!info
    Il n'est pas obligatoire de définir cette option mais cela permet de ne pas avoir à spécifier l'argument `--project` à chaque commande.


2- Filter les objets à inclure par exemple en fonction de la catégorie dans le projet:
````git
git config dsplus.filters.category Categorie/Jobs/
````

!!!warning
    La configuration du dépôt git est locale et ne sera pas partagée avec les autres développeurs.


### Vérifier le périmètre

On peut vérifier le périmètre des objets qui seront intégrés au dépôt:

````bash
dsplus list
````

Où alors la commande suivante permet de voir l'état de synchronisation entre le dépôt et le périmètre DataStage:

````bash
dsplus status
````

### Premier versionnement

Pour initialiser le dépôt avec l'intégralité du périmètre:
````bash
dsplus init --export --metadata --output
````

Cette commande exportera les objets DataStage et un fichier de métadonnées. Pour enrichir le dépôt d'autres informations il sera recommandé d'activer plus d'options:
````bash
dsplus init --export --metadata --output --image --ast --doc 
````
Ou la version raccourcie:
````bash
dsplus init -xmoi --ast --doc
````

Vérifier l'état du dépôt:
````git
git status
````
Ajouter les nouveaux éléments:
````git
git add .
````
Vérifier l'état du dépôt:
````git
git status
````
Valider:
````git
git commit -m "commentaire"
````
Pousser les modification:
````git
git push -u origin myBranch
````
!!! info
    L'instruction `-u origin myBranch` n'est à spécifier que lors du 1er push sur une nouvelle branche.


### Deuxième versionnement

Après modification ou création d'un ou plusieurs jobs:
````bash
dsplus status
````

Ajouter les objets modifiés/créés:
````bash
dsplus get -xmoi --ast --doc --job job1 job2
````
!!!info
    L'option job peut prendre plusieurs arguments, ici 2 jobs à ajouter.


Alternativement en mode batch:
````bash
dsplus init -xmoi --ast --doc --update
````

Vérifier l'état du dépôt:
````git
git status
````

Explorer les modifications:
````git
git diff --name-status HEAD^1 -- *.isx
git diff -- */job1.ast.json
````


Ajouter les nouveaux éléments:
````git
git add .
````
Vérifier l'état du dépôt:
````git
git status
````
Valider:
````git
git commit -m "commentaire"
````
Pousser les modification:
````git
git push
````


