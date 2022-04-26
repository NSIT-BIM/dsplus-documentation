---
tags: dsplus,documentation
title : init
description: Initialiser
---

# Init
Initialise ou met à jour un repository local en batch.


## Syntaxe

```
dsplus init [--update]
```

Cette commande fonctionne de manière identique à ce que ferait la commande ```get``` appliquée en boucle à ce qui est retourné par la commande ```list```

Les options possibles sont donc les combinaisons des options de ces 2 commandes.

L'option `update` permet d'appliquer la commande uniquement sur les objets modifiés vis-à-vis de l'index.
Cet index est actualisé lorsque la commande init ou get est utilisée avec l'option `git`.


## Format de sortie

La sortie est au format mixte `multi-json`, informationnel et batch suivant les options choisies.
Les sorties informationnelles peuvent être rendues silencieux avec l'option ```silent/DSP_SILENT``` activée.

## Exemples




