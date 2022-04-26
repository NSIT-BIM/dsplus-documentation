---
tags: dsplus,documentation
title : Variables d'environnement
description: Configuration par les variables d'environnement
---


# Variables d'environnement

Toute option peut être valorisée par variable d'environnement en respectant la nomenclature suivante:
<code>DSP_[OPTION]</code>
L'option devant être en majuscules, ex:
`DSP_PROJECT` est équivalent à l'option `--project`
Lles commandes dsplus ci-dessous sont équivalentes:
```bash
dsplus list --project dstage1
######
DSP_PROJECT=dstage1 dsplus list
#####
export DSP_PROJECT=dstage1
dsplus list
```

## Cas spéciaux

Certaines options définies dans le fichier de configuration peuvent être de type hierarchiques. Par exemple l'option *filters*:
```yaml
filters:
  category: Jobs
```
La convention pour la variable d'environnement équivalente est:
`DSP_FILTERS_category=Jobs`

!!! warning
    Les options de type *array* ne sont pas supportées



## Fichier .env

Les variables d'environnement peuvent être également définies dans un fichier `.env` situé dans le répertoire courant.