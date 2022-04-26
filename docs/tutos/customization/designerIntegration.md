---
tags: dsplus,howtos
title : Integrétation Designer
description: Quickstart dsplus
---

# Intégration avec le Designer


## Raccourcis

Pour gagner du temps, on peut créer des raccourcis qui simplifieront le workflow.
Editer le fichier `dsplus.yml` créé précédemment et ajouter les  lignes ci-dessous:

````yaml
shortcuts:
  git:
    get:
      ast: true
      metadata: true
      image: true
      export: true
      doc: true
      git: true
      output: true
````

On déduira la syntaxe de la définition des raccourcis:
````yaml
  nom raccourci:
    sous-commande d'origine:
      option: valeur
````

Cela aura pour effet de créer une sous-commande git pour dsplus dont l'appel
````bash
dsplus git
````
est équivalent à 
````bash
dsplus get --export --metadata --output --image --ast --doc 
````

Ainsi lorsqu'on se trouve dans le dossier du dépôt git, au lieu de:
````bash
dsplus get -xmoi --ast --doc --job job1 job2
````
On peut entrer:
````bash
dsplus git --job job1 job2
````


## Appel depuis le designer

Il est possible de se passer de l'utilisation des lignes de commandes en ajoutant dsplus aux custom tools du designer DataStage.
Cette fonctionnalité permet d'appeler des commandes arbitraires avec des paramètres contextuels tels que le nom du projet ou du job actuellement édité.

!!! question
    Jusqu'à maintenant les commandes ont été appelées depuis le dépôt lié au projet DataStage. Lors de l'appel depuis le designer on ne sait pas où se trouve le dépôt, il faut donc spécifier ce chemin d'une manière où d'une autre. 
    Plusieurs solutions à cela.

### Environnements

On introduit la notion d'environnement dans le fichier `dsplus.yml`. A l'origine, celle-ci est prévue pour pouvoir identifier plusieurs environnements (dev/test...). Ici on s'en sert pour déclarer le chemin du dépôt git lié au projet:

````yaml
envs:
  demoProject:
   target: "C:/.../CheminDepots/demoProject"
   project: demoProject
````

Ensuite on peut ajouter le custom tool au designer:

![](https://i.imgur.com/k8MvsE6.png)

![](https://i.imgur.com/qszlrxs.png)

![](https://i.imgur.com/htiLwjf.png)

![](https://i.imgur.com/LoDIDzc.png)

!!! success
    Cette opération permet donc de lancer la commande nécessaire dsplus lorsqu'un job est ouvert en passant par le menu: `Tools->Custom->git`



!!! note
    On pourrait se passer de la notion d'environnement en s'appliquant à bien standardiser les noms des dépôts et des projets.


Cependant dans le cas où un projet serait lié à plusieurs dépôts, par exemple, si chaque grande catégorie racine a son propre dépôt, la solution précédente ne marcherait pas.

### L'argument target

Pour palier à cela on peut, à la place de définir des environnements utiliser la capacité interactive du Custom Tool en spécifiant les arguments de la commande de la façon suivante:

```bash
git --project %ProjectName  --job %JobName --target "C:/.../CheminDepots/%AskArguments"
```

De cette manière lors de l'appel il est demandé à l'utilisateur de saisir le nom du dépôt vers lequel extraire le job.

Bien que plus souple cette méthode poser le risque des erreurs de saisies.

### Templating

La façon dont dsplus organise le dépot est pilotée par:

* l'argument target: racine du dépôt
* l'argument targetformat: arborescence des objets

Par défault la racine est le répertoire courant ou la racine du dépôt s'il s'agit d'un dépôt git.
Par défaut l'arborescence est la suivante:

```
racine
  |Catégorie Racine DataStage
    |_Sous catégorie
      |_ ...
        |_Nom du job
          |_NomDuJob.extension
```

Un mécanisme de templating permet de personnaliser cette organisation et accepte les arguments suivants:

* `server`: serveur d'origine
* `project`: projet d'origine
* `category`: categorie(s)
* `name`: nom
* `type`: type: job, routine, paramset...
* `ext`: extension: pjb (parallel job), qjb (sequence job) ...
* `Y`/`M`/`D`/`H`/`m`: Timestamp de modification

Plus les arguments spéciaux sur la catégorie:

* `categories.x`: où x est le numéro du dossier, permet de selectionner un dossier spécifique.
* `categories.-x`: où x est le nombre de dossiers à ignorer, permet de sélectionner les dossiers à partir d'une profondeur arbitraire.

Par défaut l'argument targetformat est donc `[category]/[name]/[name]`.

Enfin on peut donc lier l'emplacement d'un dépôt à la catégorie racine en spécifiant:
```yaml
target: "C:/.../CheminDepots/[categories.0]
```
Eventuellement, en ajoutant spécifiant le format de l'arborescence de sorte à ignorer la catégorie racine, cela évitera la répétition:
```yaml
targetformat: "[_category-1]/[name]/[name]"
```
