---
title: "Réparer un fichier ZIP ou RAR"
date: "2013-06-02"
categories: 
  - "apps"
  - "linux"
  - "macos"
  - "term"
tags: 
  - "tip"
---

Il peut arriver qu'un fichier d'archive, `.zip` ou `.rar`, soit endommagé lors de son transfert.

Un serveur buggé, une copie FTP mal terminée, de nombreux passages sur des filesystem différents : il y a de nombreuses occasions d'abîmer un fichier compressé contenant des informations sensibles.

Vous double-cliquez sur un fichier d'archive et vous obtenez un message d'erreur du type _Fichier corrompu, impossible d'extraire le contenu de l'archive_.

Tout n'est pas perdu !

## Zip

L'outil **zip** en ligne de commande va probablement réussir à sauver votre fichier.

Entre autre options, cette commande permet en effet de réparer les erreurs les plus communément rencontrées dans un fichier Zip.

Il y a deux niveaux d'intervention, léger et lourd.

Mais essayez tout de même d'abord de dézipper votre fichier dans le Terminal, pour véfifier que l'erreur ne provienne pas de l'extracteur que vous utilisez.

> Si vous le souhaitez, faites glisser à la souris le fichier en question vers la fenêtre du Terminal pour éviter de devoir taper le chemin à la main.

```
unzip fichier.zip
```

Si vous obtenez toujours des erreurs, alors essayez la première option de réparation :

```
zip -F fichier.zip --out nouveaufichier.zip
```

**zip** va alors essayer d'extraire l'archive malgré les erreurs et de rassembler le contenu récupéré dans une nouvelle archive.

Si cela ne fonctionne pas, et que donc votre archive est vraiment très abîmée, vous pouvez tout de même essayer de récupérer le maximum de contenu en adoptant l'option qui force l'extraction :

```
zip -FF fichier.zip --out nouveaufichier.zip
```

**zip** va alors probablement vous demander si l'archive fait partie d'un sous-ensemble ou s'il s'agit d'un fichier unique.

Après que vous ayez répondu, l'outil va faire de son mieux pour extraire tout ce qui est récupérable et l'archiver dans un nouveau fichier.

## Rar

On peut également réparer un fichier `.rar` avec le Terminal mais contrairement à **zip**, **rar** n'est pas intallé par défaut sur Mac OSX, il va donc falloir le faire soi-même.

Commencez par récupérer la dernière version chez RAR Lab, au moment où j'écris c'est là : [RAR OSX](http://www.rarlab.com/rar/rarosx-5.0.b4.tar.gz)

Décompressez le dossier et rentrez dedans. On peut le faire à la souris ou à la main :

```
cd ~/Downloads/
tar zxvf rarosx-5.0.b4.tar.gz
cd rar
```

Collez ensuite les lignes suivantes pour installer les binaires :

```
sudo install -c -o $USER unrar /usr/local/bin
sudo install -c -o $USER rar /usr/local/bin
```

C'est la même chose que des les copier à la main puis de les déclarer exécutables mais ça va plus vite.

Le Terminal va vous demander le mot de passe de votre compte, donnez-le lui (comme d'habitude _on ne voit pas_ les mots de passe que l'on tape dans un Terminal, c'est normal).

Vous pouvez ensuite lancez la réparation de votre fichier :

```
rar r fichier.rar
```

Contrairement à **zip** qui crée une nouvelle archive à partir de l'ancienne, **rar** recrée l'archive elle-même avec le même nom.

Faites donc une copie auparavant si vous n'êtes pas sûr de vous. C'est de toute façon une bonne habitude à prendre.
