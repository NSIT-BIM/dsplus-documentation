---
tags: dsplus,documentation
title : list
description: lister
---

# List

Liste les objets d'un projet

## Syntaxe

```
dsplus list [--AssetType] [--filter] [--info]
```

!!! info

    Prérequis: les paramètres suivant doivent être prédéfinis dans le fichier de configuration (ou ajoutés en arguments à la ligne de commande):
    
    - domain
    - server
    - username
    - password

## Options
Les types d'objets (AssetType) possibles (choix multiple):

* job
* routine
* container
* tabledef
* paramset
* stage
* dataconnection

Les options possibles:

* info : information à récupérer
* filter : filtre sql à appliquer

L'option **info** peut prendre les valeurs:

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
* **all** équivaut à toutes les valeur précédentes

## Format de sortie

La sortie est au format `json`.

## Exemples

```
dsplus list --project dstage1
```

```json
[
  {
    category: '/T_NR',
    name: 'Js_NR',
    jobType: '2'
  },
  {
    category: '/T_NR',
    name: 'Jx_NR_Lvl1',
    jobType: '3'
  },
  {
    category: '/T_NR',
    name: 'Jx_NR_Lvl1x',
    jobType: '3'
  },
  {
    category: '/T_NR',
    name: 'Jx_NR_Lvl2',
    jobType: '3'
  },
  {
    category: '/T_NR',
    name: 'Jx_NR_Lvl3',
    jobType: '3'
  },
  {
    category: '/T_NR',
    name: 'Jx_NR_Lvl4',
    jobType: '3'
  },
  {
    category: '/T_NR/archives',
    name: 'Jx_NR_Lvl2_old',
    jobType: '3'
  },
  {
    category: '/T_NR/jobs',
    name: 'Jx_NR_00_GetKeys',
    jobType: '3'
  },
  {
    category: '/T_NR/jobs',
    name: 'Jx_NR_Lvl1_0',
    jobType: '3'
  },
  {
    category: '/T_NR/params',
    name: 'Ps_NR_Db',
    jobType: undefined
  },
  {
    category: '/T_NR/routines',
    name: 'RtTnrGetKeys',
    jobType: '0'
  },
  {
    category: '/T_NR/routines',
    name: 'RtTnrSetKey',
    jobType: '0'
  },
  {
    category: '/T_NR/stages',
    name: 'StTnrRdStats',
    jobType: '3'
  },
  {
    category: '/T_NR/stages',
    name: 'StTnrWrStats',
    jobType: '3'
  }
]
```
```
dsplus list --paramset
```
```json
[
  {
    category: '/T_NR/params',
    name: 'Ps_NR_Db',
    jobType: undefined
  }
]
```
```
dsplus list --paramset --info all
```
```json
[
  {
    category: '/T_NR/params',
    name: 'Ps_NR_Db',
    RID: 'c2e76d84.19e8228.001n30kgk.0vrelio.f12j2b.r29ilfgnev3qkhcfj8atgf',
    modificationTimestamp: '2021/01/15 09:58:19',
    modifiedByUser: 'isadmin',
    creationTimestamp: '2020/04/16 10:37:28',
    createdByUser: 'isadmin',
    isSystem: 'false',
    shortDescription: 'Database parameters',
    type: 'paramset'
  }
]
```
```
dsplus list --job --info type jobType
```
```json
[
  {
    type: 'job',
    jobType: '2'
  },
  {
    type: 'job',
    jobType: '3'
  },
  {
    type: 'job',
    jobType: '3'
  },
  {
    type: 'job',
    jobType: '3'
  },
  {
    type: 'job',
    jobType: '3'
  },
  {
    type: 'job',
    jobType: '3'
  },
  {
    type: 'job',
    jobType: '3'
  },
  {
    type: 'job',
    jobType: '3'
  },
  {
    type: 'job',
    jobType: '3'
  }
]
```
```
dsplus list --job --info name --filter "jobType='2'"
```
```json
[
  {
    name: 'Js_NR'
  }
]
```
```
dsplus list --info type jobType --query 'select type,jobType,count(*) as nb from ? group by type,jobType' --format table
```
```
┌─────────┬────────────┬───────────┬────┐
│ (index) │    type    │  jobType  │ nb │
├─────────┼────────────┼───────────┼────┤
│    0    │   'job'    │    '2'    │ 1  │
│    1    │   'job'    │    '3'    │ 8  │
│    2    │ 'paramset' │ undefined │ 1  │
│    3    │ 'routine'  │    '0'    │ 2  │
│    4    │  'stage'   │    '3'    │ 2  │
└─────────┴────────────┴───────────┴────┘
```