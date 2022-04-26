---
tags: dsplus,documentation
title : encrypt
description: Encrypter un mot de passe
---


# Encrypt

Encrypte un mot de passe.
Par défaut le chiffrement utilisé est celui d'Information Server. Il est possible de choisir d'autres type de chiffrements.
Le mot de passe ainsi encrypté peut être utilisé pour sécuriser les lignes de commandes ou les fichiers de configuration de dsplus.


## Syntaxe
```
dsplus encrypt --password
```

## Chiffrements

Le choix du type de chiffrement se fait via l'option `security.provider/DSP_SECURITY_provider`. Celle-ci peut prendre les valeurs:

* iisenc (défaut)
* dsplus
* *custom* 

### dsplus

Ce chiffrement plus sécurisé que iisenc (256 vs 128) utilise un vecteur d'initialisation aléatoire et une clé unique par poste, ainsi une clé générée ne le sera qu'une seule fois et ne pourra pas être réutilisée sur un autre poste.

### custom

On peut définir son propre mode de chiffrement, pour cela il est nécessaire de définir les options:

* security.provider/DSP_SECURITY_provider: nom de la méthode (ex: *custom*)
* security.key/DSP_SECURITY_key: clé de chiffrement
* security.iv/DSP_SECURITY_iv : taille du vecteur d'initialisation
* security.algorithm/DSP_SECURITY_algorithm: algorythme de chiffrement


## Format de sortie

La sortie est de type texte sous la forme `{chiffrement}MotDePasse`

## Exemples

