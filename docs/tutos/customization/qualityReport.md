---
tags: dsplus,howtos
title : Afficher le rapport qualité depuis le designer
description: Quickstart dsplus
---

# Afficher le rapport qualité depuis le designer



Nous avons vu comment intégrer et automatiser le versionnement depuis le client Designer. Nous pouvons suivre la même logique pour générer le rapport qualité d'un job et l'ouvrir en un click depuis le Designer.

## Raccourcis

On commence par définir le raccourci qui sera intégré au Designer:
```yaml
  qualityReport:
    quality:
       openReport: true
       format: html
       reportsPath: "C:/Users/User/AppData/Local/Temp"
       #codeclimate: true
```

!!! note
    L'emplacement est arbitraire et est spécifié ici pour simplifier l'appel au plugin.


## Designer

On ajoute comme précédement une commande au Custom Tools. La commande de génération de rapport qualité ne générant des informations que sur la sortie standard, il faut faire une redirections. Certaines commandes complexes n'étant pas toujours supportées on contourne en appelant en réalité, le programme git-bash et en lui passant la commande en argument:

* Command: `C:\Program Files\Git\git-bash.exe`
* Arguments: `-c "dsplus qualityReport --job %JobName --project %ProjectName > /tmp/%JobName.html"`

!!! info
    Depuis git-bash /tmp est équivalent à C:/Users/User/AppData/Local/Temp


A ce stade là lors de l'appel depuis le desginer un rapport est généré. On va mettre en place un plugin pour l'ouvrir automatiquement.

## Plugin


```yaml
  openReport:
     type: bin
     program: explorer 
     args: ["file:///${reportsPath}/${asset.job.0}.html"]
     event: "finish:quality"
     context: 
        quality:
          openReport: true
```