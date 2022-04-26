---
tags: dsplus,documentation
title : Configuration git
description: Configuration via Git
---


# Configuration Git

Les options peuvent également être spécifiées via la configuration du repository git local en respectant la nomenclature suivante: <code>dsplus.[option]</code>

Par exemple les commandes ci-dessous sont équivalents:
```bash
dsplus list --project dstage1
######
git config dsplus.project dstage1
dsplus list
```

Cette fonctionnalité permet donc d'avoir des options définies dans les paramètres du repository git et ne plus avoir à les entrer dans la ligne de commande. 
De manière générale on y définira par exemple les options:

* dsplus.project: Projet connecté au repository
* dsplus.filters.category: Catégorie du projet
* dsplus.git: true

!!! info
    Les branches sont également supportées. 
    Le format est alors dsplus.branche.option
