---
title: "Le Terminal et ses usages"
date: "2014-04-12"
categories: 
  - "culture"
  - "dossier"
  - "pinned"
  - "term"
---

Voici un dossier, accompagné d'un tutoriel, sur le Terminal et ses usages.

Je m'adresse particulièrement aux 'débutants' qui n'osent pas l'utiliser ou qui ne savent pas trop à quoi ça sert.

Cette introduction à l'univers de la "ligne de commande" vous révèlera, je l'espère, comment envisager l'usage de la "console" de manière ludique et efficace.

# Le Terminal

## Introduction

### Le mode graphique, c'est bien

Il y a des années, des personnes très intelligentes et talentueuses ont créé des [interfaces graphiques](http://fr.wikipedia.org/wiki/Interface_graphique) pour nous aider à communiquer plus facilement avec nos ordinateurs.

Grâce à la souris, au trackpad, au tactile, aux fenêtres et autres menus déroulants, icones et codes couleur, nous pouvons aisément trouver notre route parmi les commandes complexes et nombreuses options disponibles d'un logiciel professionel ou d'un système d'exploitation.

### Le mode texte, c'est bien

Plusieurs générations auparavant, d'autres génies de la même trempe avaient créé la [ligne de commande](http://fr.wikipedia.org/wiki/Interface_en_ligne_de_commande), qui permet de s'exprimer logiquement et efficacement lorsque l'on a des requêtes à transmettre à son ordinateur.

"Parler" en anglais naturel à ses machines était bien sûr impossible : ils ont donc conçu un système ou les commandes ressemblent à des mots et des verbes, permettant à _l'utilisateur_ et non pas seulement à l'administrateur, de construire des requêtes élaborées.

Une poignée de mots suffisent à déclencher des séquences complexes, de par la puissance de ce concept.

### L'un n'est pas "mieux" que l'autre

Taper des commandes en mode texte est très puissant mais necessite d'être rigoureux (les fautes de frappe sont plutôt malvenues) et d'apprendre un vocabulaire qui peut devenir complexe avec l'ampleur des tâches que l'on souhaite confier à la machine.

Cliquer dans une interface graphique est très pratique mais necessite d'apprendre les positions et contenus des menus et boites de dialogue, par exemple, mais plus généralement d'apprendre à utiliser l'application ; ainsi que de développer une certaine dextérité manuelle (souris/trackpad), et d'avoir beaucoup de patience.

Le modèle tactile a apporté une fraîcheur certaine depuis quelques années, mais l'on se rend bien compte que l'on ne peut pas tout faire non plus avec un tel appareil.

> J'estime pour ma part qu'il faut utiliser le bon outil dans le bon contexte, et que toute querelle partisane est nulle et non avenue.

## Un peu d'histoire

Alors je ne vais pas me lancer ici dans l'histoire de l'informatique et des interfaces Homme/Machine, ça pourrait prendre un peu de temps...

Non, nous allons très simplement voir d'où vient ce fameux Terminal.

### Mainframe/Terminal

Les premiers ordinateurs vraiment puissants, il y a à peine plus de quarante ans, étaient énormes : ils remplissaient facilement une salle entière.

Ces machines avaient généralement un poste dédié qui permettait de leur donner des instructions: le [terminal](http://fr.wikipedia.org/wiki/Terminal_informatique), c'est-à-dire un simple écran avec clavier qui envoie ce qui est tapé à la vraie machine, le [mainframe](http://fr.wikipedia.org/wiki/Ordinateur_central), qui reçoit les instructions, les traite, et renvoie le résultat sous forme textuelle vers le terminal.

![](https://aya.io/blog/images/terminal.gif)

Le Terminal est complètement idiot et ne sait strictement rien faire de part lui-même : c'est juste un pont entre vous et la machine.

A cette époque, le Terminal était physiquement séparé des mainframes, avec son propre écran et son propre clavier.

Quand les systèmes devinrent multi-utilisateurs, les terminaux se sont multipliés dans les bureaux, s'adressant aux grosses machines installées dans les départements IT des entreprises.

### GUI

Puis vinrent les Graphical User Interface -- les interfaces graphiques, avec les fenêtres, les icones, etc.

C'était une _vraie_ révolution !

![](https://aya.io/blog/images/xerox.jpg)

Auparavant, les machines n'étaient tout simplement pas assez puissantes pour pouvoir afficher autre chose que du texte.

Ensuite, même une machine avec des capacités graphiques (par exemple pour afficher des courbes, des chartes, etc) n'était pas forcément _commandable_ par sa couche graphique.

Il a fallu l'invention de la souris et d'autres révolutions par [Douglas Engelbart](http://fr.wikipedia.org/wiki/Douglas_Engelbart) et la mise au point des nouveaux paradigmes par [Xerox, Apple et autres](http://fr.wikipedia.org/wiki/Xerox_PARC) pour que ce que vous trouvez normal aujourd'hui devienne une réalité : le bureau, les menus déroulants, la corbeille, les boites de dialogue, etc.

### Complémentarité

Mais ces interfaces n'avaient pas pour but de remplacer les lignes de commande.

Et ne l'ont d'ailleurs pas fait. :)

Elles se sont ajoutées aux outils textuels déjà disponibles.

Par exemple, je ne me vois pas cliquer dans des dizaines de sous-menus et/ou déplacer plein de fenêtres pour aller trouver un malheureux fichier.

De la même manière je ne vais pas utiliser le Terminal pour créer des montages vidéo ou retoucher des photos.

Il serait de même irresponsable d'utiliser un système fenêtré avec plein d'animations graphiques pour manipuler des fichiers de configuration sur un serveur à l'autre bout du monde... question de bon sens.

Bref, la tronçonneuse ce n'est pas _mieux_ que le scalpel, c'est _différent_.

## Usage

Mais alors, qu'est-ce qu'on y tape comme texte dans cette ligne de commande, comment ça marche ?

La plupart du temps vous y tapez `nom_de_la_commande` + `paramètres` + `cibles`.

Euh... hein ?

Par exemple :

```bash
ls -l Documents
```

va demander de montrer les fichiers (ls) en mode liste (-l) du dossier Documents.

_`ls` est le nom de la commande; `-l` est une option; `Documents` est la cible._

### Exemples

La commande `more` :

```bash
more Documents/bidule.txt
```

va afficher le contenu page par page (more) du fichier bidule.txt dans le dossier Documents.

La commande `mv` :

```bash
mv Photos/portrait.jpg Documents
```

va demander de déplacer (mv) un fichier du dossier Photos vers le dossier Documents.

`mv` est le nom de la commande, qui signifie 'move', `Photos/portrait.jpg` est l'emplacement du fichier à déplacer, `Documents` est le nom du dossier dans lequel on veut le déplacer.

La commande `rm` :

```bash
rm -i Documents/machin.txt
```

va supprimer (rm) le fichier machin.txt définitivement, en demandant confirmation (-i).

Que sont ces commandes, `ls`, `mv`, etc ?

Des applications.

`ls` est une application, tout comme `mv`, `rm`, `more` et les milliers d'autres installées dans votre système.

Les systèmes Unix ont une myriade de toutes petites applications qui font chacune une seule chose mais la font [extrêmement bien](https://web.archive.org/web/20140408082841/http://www.faqs.org/docs/artu/ch01s06.html).

C'est toute la philosophie Unix : on manipule de minuscules programmes qui deviennent, de fait, des commandes presque 'naturelles' quand on les combine.

Les plus utilisées de toutes sont certainement `ls` et `cd` : ce dernier permet de se déplacer dans les fichiers et dossiers (cd = Change Directory).

Saurez-vous deviner le résultat de cette séquence d'instructions ?

```bash
cd ~/Desktop
ls
mv lolcat01.jpg ~/Pictures
rm lolcat*
```

1. j'entre dans le dossier Desktop
2. je liste les fichiers
3. je déplace le fichier lolcat01.jpg vers le dossier Pictures de mon compte utilisateur
4. je supprime du Desktop tous les fichiers commençant par "lolcat"

**Au fait, très important: on ne tape pas toutes les lettres !**

Vous rigolez ou quoi ?

Vous vous imaginez qu'on va s'amuser à taper

```text
/Users/myname/Desktop/ohlepitindenomdefichierpaspossible.txt
```

en entier à chaque fois ? :)

Non, vous allez utiliser la touche TAB comme tout le monde (la flèche collée au taquet, à gauche du clavier, généralement au-dessous de la touche '@' sur un Mac), ce qui vous permettra **d'auto-compléter** les commandes et les cibles.

Si je reprends mon exemple précédent, voilà ce que j'ai en fait tapé :

```bash
cd ~/De (TAB)
ls
mv l (TAB) 01 (TAB) ~/P (TAB)
rm l (TAB) *
```

Alors oui, ça a l'air étrange décrit comme ça, mais à faire ça va super vite et on se rend compte immédiatement que la logique est imparable.

Petite astuce bien utile : les flèches HAUT et BAS du clavier vous déplacent dans l'historique des commandes que vous avez déjà tapé.

Par exemple vous avez fait un ls bien compliqué deux commandes plus tôt et vous voulez recommencer, vous faites HAUT HAUT.

Résumé des commandes que nous avons vues :

`cd` = change directory (changer de dossier)

`ls` = list (lister les fichiers)

`cp` = copy (copier)

`mv` = move (déplacer)

`rm` = remove (supprimer)

`more` = lire page par page

## Applications

Nous venons d'évoquer des applications, certes, mais ce sont des utilitaires système : copier ou déplacer des fichiers, etc.

![](https://aya.io/blog/images/lynx-aya.jpg)

Cependant il existe évidemment toutes les autres gammes logicielles en ligne de commande, du navigateur web (hé oui!) au client email, du cloneur de disques durs à la calculatrice scientifique, tableur, jeu, serveur, etc.

La seule différence avec les logiciels que vous utilisez couramment, tels que Microsoft Word ou Apple Mail, est que ces derniers affichent leur texte dans des fenêtres graphiques, alors que les applications en ligne de commande n'affichent que du texte.

## Le Terminal

Aujourd'hui le Terminal n'est plus une machine physique connectée à une salle des machines, mais une application connectée à un ordinateur.

Bien sûr, grâce au réseau, ce Terminal logiciel peut aussi (c'est sa nature de Terminal) se connecter à une autre machine, ce qui vous permet de la diriger comme si vous étiez sur son clavier. Ce n'est pas de la 'télécommande' : c'est plutôt de la prise en main à distance.

En effet, quand vous êtes dans le Terminal et que vous vous connectez à un serveur, et vous vous retrouvez avec le prompt de ce serveur; _vous n'êtes plus dans votre machine mais dans la machine distante_. C'est très différent de 'je commande une machine à partir de la mienne', qui est aussi très pratique, évidemment.

Bref, passons là-dessus, ça mériterait des livres entiers.

Il existe de nombreuses applications de Terminal, et avec Mac OS X est livrée une version qui se défend bien, qui se trouve dans le dossier Applications/Utilitaires et qui se nomme simplement "Terminal.app".

J'utilise pour ma part [iTerm2](http://www.iterm2.com/), mais c'est un détail cosmétique et pratique, et ne change rien au contenu de ce tutorial.

Certaines applications de Terminal vous permettent d'utiliser la souris dans une certaine mesure, par exemple pour sélectionner du texte ou cliquer sur un lien, mais n'oubliez pas que par design un Terminal n'est qu'une machine idiote destinée à envoyer et recevoir du texte.

# Tutoriel

## Déplacement et affichage

Nous avons évoqué ce sujet dans l'introduction mais nous allons maintenant entrer un peu dans le détail.

Vous vous retrouvez donc devant le Terminal, qui vous affiche quelque chose comme :

```text
Last login: Wed Apr 9 14:21:28 on ttys010
yourlogin@yourmachine:~ $
```

> Et là vous vous dites, tiens je mangerais bien des chips, moi.

![](https://aya.io/blog/images/robocop.jpg)

Bon, supposons que vous soyez encore en train de lire ceci...

Traditionnellement, à l'ouverture, un Terminal vous affiche l'heure de votre dernière connection et l'identifiant du Terminal utilisé.

Ensuite, optionnellement, "You've got mail" ou similaire (ce qui est faux la plupart du temps car mal configuré).

Puis finalement le _prompt_, en français "l'invite", c'est-à-dire l'emplacement ou vous pouvez commencer à taper votre texte: juste après le signe "$" qui suit les indications d'identité (votre login et le nom de votre machine).

Bien sûr, selon le système utilisé et selon le Terminal utilisé, cela peut grandement différer : cependant le principe restera le même, vous tapez votre texte à l'invite, au prompt, et nulle part ailleurs dans le Terminal.

Vous allez certainement d'ailleurs rapidement remarquer que l'écran du Terminal est plutôt passif : le seul endroit interactif est la ligne de commande, le reste de l'écran ne sert qu'à l'affichage.

Chaque nouvelle ligne ajoutée en bas de l'écran fait remonter les lignes précédentes d'un cran.

L'écran se déplace par sauts de ligne.

### Le tilde

Vous avez remarqué ce petit caractère dans le prompt, le tilde ? Celui-ci :

`~`

**Ce symbole représente le dossier utilisateur, souvent dénommé "home", la maison.**

C'est traditionnellement là que s'ouvre un Terminal.

Au lieu d'afficher ou de taper par exemple "/Users/yourname/", on fait `~`, ça va plus vite. (sur un clavier Mac, on tape un tilde en faisant ALT+n puis espace).

Hé bien le Terminal affiche, par défaut, le répertoire courant, et donc il nous affiche ici un tilde.

Exemple :

```bash
cd ~
```

vous ramène dans votre dossier utilisateur, d'où que vous soyez.

Autre exemple : vous êtes dans le Bureau mais vous voulez entrer dans le dossier Téléchargements qui est dans votre dossier utilisateur.

Vous faites :

```bash
cd ~/Downloads
```

(en effet les noms de dossiers de Mac OS X sont traduits par l'interface graphique mais pas par l'interface texte !).

Lister les fichiers du dossier Home ?

```bash
ls ~
```

Du dossier Téléchargements :

```bash
ls ~/Downloads
```

C'est la même chose que de faire `ls /Users/yourname/Downloads`.

### Les deux points

Voici une autre astuce : le symbole `..` (deux points), qui représente le _dossier supérieur_.

Par exemple, vous êtes dans le dossier Downloads (on va rester hors traductions maintenant) et vous voulez "remonter" dans le dossier Home. Vous faites :

```bash
cd ..
```

Vous voulez remonter de deux niveaux ?

```bash
cd ../..
```

Le concept est simple mais puissant, vous vous en rendrez compte rapidement.

### Le point

Associé à ce principe, nous avons le point: `.` qui représente le _dossier courant_.

Ce point signifie littéralement 'ici'.

Par exemple si vous êtes dans le dossier Pictures et que vous voulez déplacer ici (dans le dossier Pictures, donc) une image qui est sur le bureau, vous faites :

```bash
mv Desktop/lolcat.jpg .
```

### Le slash

Je ne l'ai pas expliqué mais vous l'aviez déjà compris : le caractère `/`, le slash, représente une séparation dans le chemin des fichiers et dossiers.

Par exemple, pour représenter le fichier machin.txt qui est dans Downloads qui est dans Home, on écrit

`~/Downloads/machin.txt`

On peut bien évidemment lister n'importe quel dossier à partir de n'importe où :

```bash
ls /Applications
```

vous donnera toujours le contenu du dossier Applications qui se trouve à la racine du disque, où que vous soyez vous-même, _parce que vous avez mis le caractère `/` devant_.

**Le caractère `/` en début de chemin signifie "racine du disque dur".**

Quand on ne précise pas ce caractère en début de chemin, le Terminal assume que nous partons du dossier actuel et utilisera un chemin relatif.

Si je tape `ls Applications` cela signifie que je demande à voir les fichiers du dossier Applications qui se trouve dans le dossier courant ! S'il n'y en a pas => erreur.

### Exemples

```bash
cd /
ls ~/Downloads
cd ~
ls Downloads
ls ../..
cd ..
```

Explication ligne par ligne :

- j'entre à la racine du disque
- je liste les fichiers qui sont dans Home / Downloads
- j'entre dans Home
- je liste encore le contenu de ce même dossier Downloads
- je liste le dossier qui se trouve deux niveaux au-dessus de moi, c'est-à-dire le dossier /User
- je 'remonte' dans Home (c'est-à-dire /User/yourname)

Note : je rappelle, une dernière fois, que je ne tape jamais toutes les commandes en entier !

La touche TAB est votre grande amie, ne l'oubliez pas.

Elle sait compléter les commandes mais aussi _et surtout_ elle sait compléter les chemins.

Petite astuce : si vous êtes perdus, tapez `pwd` (qui signifie Print Working Directory) et le Terminal vous affichera le chemin du dossier courant en entier.

Maintenant que nous avons vu les bases, découvrons quelques commandes supplémentaires.

## Les essentiels

Les commandes essentielles sont tous simplement des équivalences à ce que vous avez l'habitude de faire avec la souris.

![](https://aya.io/blog/images/chat.jpg)

Par exemple, déplacer un fichier téléchargé vers le dossier documents.

Vous ouvrez le Finder, double-cliquez sur Downloads (ou dépliez sa flèche en cliquant), cliquez sur le fichier (par exemple _truc.txt_), maintenez cliqué, appuyez sur la touche CMD et maintenez appuyé, déplacez la souris jusqu'au dossier cible, relâchez le clic puis la touche.

Ce n'est pas exactement trivial, en fait... et bonne chance si vous avez la tremblote. ;)

Avec le Terminal :

```bash
cd ~
mv Dow (TAB) tr (TAB) Doc (TAB)
```

Voilà, environ trois secondes. :)

Mais alors, la souris c'est quand même plus pratique pour déplacer plusieurs fichiers à la fois, non ?

Pas toujours. Et souvent pas du tout, en fait.

Voyons quelques exemples de ce qui fait la force de l'interface textuelle.

### L'englobeur

Vous pouvez utiliser le symbole `*`, que j'appelle l'englobeur, en français l'astérisque (l'étoile), pour représenter _tous_ les objets d'un ensemble.

Par exemple, tous les fichiers dans Downloads qui commencent par les lettres "Tru" :

```bash
ls Downloads/Tru*
```

Ici, par exemple, ça va englober les fichiers Truc.txt, Trucmachin.jpg, Truduc.doc, etc.

Ou encore, une copie de toutes vos photos de vacances que vous avez balancées sur le Bureau, vers une clé USB :

```bash
cp Desktop/*.jpg /Volumes/USB/
```

On demande à `cp` de copier tous les fichiers .jpg du Bureau vers le volume nommé USB qui se trouve dans /Volumes, comme tous les volumes externes dans Mac OS X.

Déplacer mes notes du mois de janvier vers un dossier de backup :

```bash
mv Documents/notes-2014-01-*.txt /Volumes/HDDExterne/Backups/notes/
```

Ici ça va englober notes-2014-01-01.txt, notes-2014-01-02.txt, notes-2014-01-03.txt, etc.

Supprimer, sans demander confirmation, tous les fichiers zip téléchargés :

```bash
rm -f Downloads/*.zip
```

On demande d'effacer (rm) sans demander de confirmation (-f) tous les fichiers zip (\*.zip) du dossier Downloads.

> Attention ! Pas de corbeille ni de 'undo' ici ! On fait gaffe à ce qu'on tape... :)

### Le redirecteur

Attention, fonction puissante mais qui exige attention et rigueur : on peut rediriger le _contenu_ d'un fichier vers un autre fichier avec le symbole

`>`

Mais apprenons d'abord une nouvelle commande : `echo`.

La commande _echo_ permet d'écrire du texte.

```bash
echo "Wesh gro ou bien"
```

Notre exemple va simplement écrire "Wesh gro ou bien" à l'écran.

En effet, quand on ne précise pas à une commande à quel endroit elle doit montrer sa sortie, elle le fait à l'écran.

Mais on peut lui demander de sortir son texte non pas à l'écran, mais dans un fichier, par exemple.

L'application , elle, ne sait pas si elle affiche à l'écran ou ailleurs : elle se contente de balancer ses données en sortie, et c'est vous qui décidez de quelle sera cette sortie.

Par exemple, vous voulez créer un fichier texte nommé "wesh.txt" dans votre dossier Documents pour y sauvegarder cette merveille de la littérature française ?

```bash
echo "Wesh gro ou bien" > ~/Documents/wesh.txt
```

Si le fichier n'existe pas, il sera créé.

Nous avons utilisé la même commande `echo "Wesh gro ou bien"` que précédemment, mais nous avons cette fois précisé une route de sortie _vers un fichier_.

Notre phrase sera ici "affichée" dans un fichier, et donc... enregistrée.

Le redirecteur fonctionne aussi avec les fichiers au lieu de phrases.

Nous aurons besoin de la commande `cat` qui ne miaule pas mais qui lit le contenu de tout fichier :

```bash
cat ~/Documents/wesh.txt
cat ~/Documents/wesh.txt > ~/Desktop/yo.txt
```

Dans la première ligne, `cat` lit le contenu de wesh.txt et l'affiche à l'écran.

Dans la deuxième ligne, `cat` lit le contenu de wesh.txt, et le redirige non pas vers l'écran mais vers yo.txt sur le Bureau, créant de ce fait une copie de wesh.txt avec un nouveau nom à ce nouvel emplacement.

Attention, si yo.txt existe déjà, il sera remplacé !

Dernier point tant que nous sommes là : le double redirecteur, `>>`, permet _d'ajouter_ du texte _à la fin_ d'un fichier.

```bash
echo "Première ligne" > pensées.txt
echo "La suite, ..." >> pensées.txt
echo "Signé le zinkou" >> pensées.txt
```

### Le pipe

![](https://aya.io/blog/images/magritte_pipe.jpg)

Le pipe, en français... le pipe. Ca signifie "le tuyau", et c'est le symbole

`|`

Cette barre verticale s'obtient par combinaison de touches. Sur Mac, c'est SHIFT+ALT+L.

Ce symbole de tuyau... symbolise un tuyau, qui envoie le _résultat_ d'une commande, sa sortie, vers _une autre commande_.

De plus, on peut enchaîner autant de commandes et de pipes que l'on veut. Voici un exemple concret.

Disons que vous avez un fichier qui contient plusieurs mots, et que vous voulez les trier par ordre alphabétique.

Il existe la commande `sort` qui permet de faire du tri, et cette commande accepte des données en entrée.

Je vais donc _lire_ le contenu de mon fichier texte avec `cat` et rediriger la sortie de "cat" vers `sort` comme ceci :

```bash
cat mots.txt | sort
```

_"cat" lit le contenu et l'envoie à "sort" qui le trie puis l'affiche._

La liste triée est longue, et vous voulez la lire page par page ? Envoyez la à `more` :

```bash
cat mots.txt | sort | more
```

Et si vous vouliez, ensuite, compter les mots qu'il y a dans le fichier ? Il existe la commande `wc` (qui signifie Word Count et non pas, euh, bon arrêtez de ricaner bêtement là) qui permet de compter les mots (ou lignes, ou caractères, etc).

```bash
cat mots.txt | wc -w
cat mots.txt | wc -l
cat mots.txt | wc -m
```

La première ligne compte les mots, la deuxième compte les lignes, la troisième compte les caractères. En effet, la commande `wc` comme de nombreuses commandes, accepte un certain nombre d'options, parmi elles `-l`, `-w` et `-m`.

### Exemples

_Voici quelques exemples de commandes pour clore cette section._

Lister tous les fichiers d'un dossier, triés, dans un fichier texte :

```bash
ls -A ~/Pictures/*.jpg | sort > ~/Desktop/liste.txt
```

Je vous encourage à faire `man sort` pour découvir les options de `sort`.

_Astuce_: la commande `man` (pour Manual) permet d'obtenir le manuel d'utilisation d'une commande (s'il existe à ce format).

Lire et afficher le contenu d'un fichier sur Internet :

```bash
curl https://aya.io/blog/files/salut.txt
```

`curl` est une commande qui permet de récupérer des données à partir d'un serveur. On peut lire toutes sortes de fichiers, également uploader, aussi par exemple télécharger des sites web entiers, etc.

Ici, j'ai simplement mis une phrase dans le fichier 'salut.txt' puis partagé ce fichier avec Dropbox, dont vous lisez le contenu sans 'télécharger' le fichier.

Savez-vous que vous avez un dictionnaire de mots installé dans Mac OS X et Linux ?

```bash
cat /usr/share/dict/words | grep 'text'
```

D'abord nous lisons le contenu de ce fichier de mots avec `cat`, puis nous utilisons une nouvelle commande, `grep`, qui permet de sélectionner des éléments dans des données.

Ici, la commande `cat /usr/share/dict/words` envoie _tous_ les mots du fichier de mots à la commande `grep` qui sélectionn les mots contenant la séquence de lettres 'text'.

Quand votre Terminal est plein de sorties texte illisibles, il est temps de passer un coup de chiffon :

```bash
clear
```

Ensuite on peut se détendre devant un bon vieux film...

```bash
telnet towel.blinkenlights.nl
```

### Sudo

Tout ce que nous avons effectué jusqu'à présent, nous l'avons fait avec nos _droits d'utilisateur_.

Comme vous le savez probablement déjà, pour installer une application au niveau système ou pour modifier des paramètres clés du système, il faut avoir les _droits d'administrateur_.

Dans la ligne de commande, pour obtenir les droits d'administrateur _le temps d'une commande_, il faut précéder la commande de `sudo` (qui signifie Super User Do).

```bash
sudo rm -f ~/.Trash/*.jpg
```

Ici, nous demandons de supprimer (rm) tous les fichiers JPG (\*.jpg) de la Corbeille (le dossier `.Trash` qui se trouve dans Home) sans demander de confirmation (-f).

Comme nous le faisons avec les droits d'admin (sudo), cela permet par exemple de supprimer des fichiers que votre _corbeille utilisateur_ ne pouvait pas supprimer (ce qui arrive parfois à cause de conflits de droits d'accès).

Le Terminal vous demandera alors votre mot de passe système, que vous taperez à l'aveugle (pas de petites étoiles pour signifier les caractères).

Est-il utile de préciser qu'il faut faire _très_ attention à ce que l'on tape quand on est en sudo ? ;)

### Warning

Par ailleurs, ça ne fait pas de mal, un petit warning : attention aux espaces !

Par exemple, regardez cette commande qui supprime tous les fichiers du dossier `temp` qui est à la racine du disque :

`rm /temp/*`

On demande à `rm` d'effacer tous les fichiers et dossiers du dossier /temp.

Si vous faites un faute de frappe et que vous mettez un espace entre le slash et le nom du dossier, comme ceci :

> Attention, ne tapez pas cette commande !

`rm / temp/*`

vous demandez alors deux choses à 'rm' :

- la première est d'effacer tous les dossiers et fichiers _de la racine du disque_ (/), **donc de tout le disque** !
    
- la seconde est d'effacer le contenu du dossier temp.
    

**Mais quand 'rm' essaiera d'effacer le dossier temp, celui-ci n'existera plus, pas plus que... le contenu de votre disque dur.**

> Méfiance !!!

\[embed\]https://www.youtube.com/embed/Ek2IZlyAwwM\[/embed\]

## Allons plus loin

Et essayons d'utiliser de véritables situations.

Nous allons être obligés de voir de nouvelles commandes : vous n'êtes pas obligés de les apprendre !

L'essentiel est de saisir le fonctionnement global, les conventions, et ensuite vous apprendrez tranquillement par la pratique et la documentation.

### Alias

Vous utilisez maintenant la touche TAB en permanence pour compléter les noms de fichiers et les commandes, c'est bien.

Il existe aussi, pour continuer à se faciliter la vie, une fonction nommée "alias" qui permet de créer des nouveaux noms pour des commandes existantes.

Par exemple, vous vous rendez compte que vous tapez souvent `ls -l ~/Documents`.

Vous pouvez créer un alias comme ceci :

```bash
alias ldoc='ls -l ~/Documents'
```

Et si maintenant vous tapez `ldoc`, le Terminal exécutera `ls -l ~/Documents` à la place.

J'ai choisi le nom "ldoc" totalement arbitrairement, vous pouvez mettre ce que vous voulez, à condition que ça ne remplace pas une commande existante...

Car si vous faites `alias ls='ls -l'`, ça exécutera `ls -l` à chaque fois que vous demanderez un `ls` normal ! Ca peut être très utile, mais attention à ce que vous faites.

Maintenant, problème : cet alias ne vit que pendant cette session du Terminal. Si vous le quittez puis le relancez, l'alias aura disparu.

Il existe donc un fichier de configuration du Terminal, qui est lu à chaque fois que le Terminal est ouvert ou relancé.

Ce fichier a une particularité : c'est un fichier "invisible". Il n'apparaît pas lors d'un `ls` normal, pas plus que dans les fenêtres du Finder.

Parce que le nom de ce fichier _commence par un point_.

Et c'est une convention pour dire que le fichier ne doit pas être normalement visible. Pour le voir avec "ls" il faut ajouter l'option "-a" : `ls -a`, et dans le Finder c'est une option à cocher.

Ce fichier se nomme `.bashrc` et se trouve à la racine de votre dossier Home (maison, le dossier utilisateur).

Pourquoi ce nom ? Parce que "bash" est en fait le nom de l'application dans laquelle vous êtes quand vous utilisez le Terminal. :)

Et oui, le Terminal n'est.. qu'un Terminal, il ne sait rien faire. Il affiche du texte, connecté à une machine, localement ou en réseau.

Dans ce Terminal se lance automatiquement un "shell", c'est-à-dire une application qui accepte des lignes de commande et les envoie au système, qui lui retourne des résultats, que le shell affiche dans le Terminal.

Il y a plusieurs shells, mais le plus répandu (et installé par défaut dans Mac OS X) se nomme "bash".

Revenons-donc à notre fichier `.bashrc` et allons regarder son contenu :

```bash
cat ~/.bashrc
```

Il y a déjà au moins une ligne remplie automatiquement par la configuration du système, et qui déclare le chemin (path) vers les exécutables du système (si ce fichier est vide, aucune importance, le chemin est probablement dans un des autres fichiers de configuration genre .bash\_profile).

Pour faire perdurer un alias, il suffit de le rajouter dans le fichier .bashrc (ou .bash\_profile, donc).

Ca peut se faire en ouvrant le fichier dans un éditeur, mais aussi en ajoutant notre alias à la fin du fichier comme nous savons désormais le faire :

```bash
echo "alias ldoc='ls -l ~/Documents'" >> ~/.bashrc
```

Il faut ensuite "rafraîchir" le Terminal, soit en le quittant/relançant, soit en faisant :

```bash
source ~/.bashrc
```

Voilà, désormais quand vous taperez `ldoc` c'est la séquence complète qui sera exécutée à la place.

Voici un extrait de mes alias, juste pour l'exemple :

```bash
alias ls='ls -GhFa'
alias src='source ~/.bashrc'
alias ip="curl icanhazip.com"
alias cpu='top -o CPU'
```

On peut mettre d'autres choses que des alias dans le fichier bashrc, mais ce sera pour un autre article...

### Scripts

Jusqu'à présent nous avons exécuté une seule commande à la fois, en la tapant dans la ligne de commande ; ou plusieurs commandes à la fois, en les enchaînant grâce au pipe.

Mais la puissance de la "ligne de commande" est démultipliée dès que l'on fait des _scripts_, c'est-à-dire des fichiers exécutables qui contiennent plusieurs lignes de commande.

Le système lance le script, qui s'exécute ligne après ligne, dans l'ordre.

Par exemple, créons un mini script, sans quitter l'invite :

```bash
mkdir ~/scripts
echo "ls ~/Pictures/* > ~/Desktop/liste_images.txt" > ~/scripts/listim.sh
chmod u+x ~/scripts/listim.sh
```

1. Je crée un dossier "scripts" dans Home grâce à la commande `mkdir`
2. J'écris la commande `ls ~/Pictures/* > ~/Desktop/liste_images.txt` dans un fichier nommé listim.sh dans le dossier scripts
3. Je rends ce fichier exécutable

Dorénavant, à chaque fois que j'exécuterai ce fichier (comme si c'était une app), le système exécutera son contenu : dans notre exemple, un nouveau fichier texte contenant le listing du dossier Pictures sera créé sur le bureau.

L'extension `.sh` désigne un fichier de script "bash".

La commande système `chmod` permet de donner certains droits à certains fichiers : ici nous donnons les droits "exécutable" (`u+x`) à notre fichier de script.

Comment exécuter ce fichier ? En l'appellant simplement. Par exemple si je suis sur le bureau ou n'importe où ailleurs :

```bash
sh ~/scripts/listim.sh
```

Si le fichier est exécutable, pas besoin de `sh` :

```bash
~/scripts/listim.sh
```

Si j'étais dans le dossier scripts, j'aurais pu le lancer en précisant seulement le symbole du dossier local :

```bash
./listim.sh
```

Mais la solution recommandée est d'ajouter, dans votre fichier `.bashrc`, une entrée dans le chemin qui pointe vers votre dossier de scripts.

Par exemple, dans mon cas, j'ai simplement rajouté le chemin du dossier scripts à la fin de la ligne existante, après les deux points (`:`), ce qui donne au final :

```bash
export PATH=/usr/local/sbin:/Users/ericdke/.rvm/gems/ruby-2.1.0/bin:/usr/local/git/bin:/usr/bin:/usr/sbin:/bin:/sbin:/Users/ericdke/scripts
```

En faisant ça, plus besoin de spécifier le chemin de l'éxécutable pour le lancer.

En effet, si l'on ne précise pas le chemin, alors le système va chercher dans les dossiers connus, y compris dans celui que vous venez de rajouter.

On peut donc désormais faire tout simplement :

```bash
listi (TAB)
```

à partir de n'importe où, et le contenu du script sera exécuté.

Vous vous doutez bien qu'il y aurait beaucoup à dire sur le sujet, mais ce serait sortir du contexte de ce tuto.

## Terminaux

### Terminal.app

Le Terminal fourni avec Mac OS X est basique mais suffit à la plupart des usages.

Néanmoins il est préférable de se l'approprier un peu, donc nous allons voir quelques réglages interessants.

Vous avez déjà vu que vous pouvez lancer des nouvelles fenêtres qui ont des thèmes différents, c'est dans le menu.

Mais vous pouvez aussi personnaliser ces thèmes, notamment la police de caractères et les couleurs.

Pour la fonte c'est une question de goût, certes, mais aussi de lisibilité.

Je vous conseille 'Inconsolata', 'Menlo', 'Ubuntu', 'Open Sans' et 'Source Sans'.

Perso, j'adore Menlo en minuscules, magnifique, très naturel. Dommage que les lettres accentuées du français soient un peu étranges.

Ubuntu est très ronde et agréable, et la plus 'neutre' est Source Sans.

Elles sont toutes disponibles soit dans votre système soit sur le web.

Pour les couleurs, faites votre sauce... Je vous conseille ceci dit d'éviter les contrastes trop forts, genre blanc pur sur noir pur, ça fatigue les yeux.

Vous pouvez aussi mettre une image de fond dans le Terminal (bravo pour la lisibilité...) ou le rendre semi-transparent pour se la jouer hollywood.

Dernier conseil, ne dépassez pas les 80 colonnes en largeur, ça rend également les phrases plus difficiles à lire si elles s'affichent sur une ligne trop longue. L'oeil préfère les retours à la ligne.

### iTerm2

iTerm2 est un terminal gratuit très puissant et configurable.

Puissant, ça veut dire qu'il a plein d'options et de fonctions qui le rendent bien plus pratique et agréable à utiliser que la plupart de ses concurrents.

Par exemple, vous avez la possibilité d'ouvrir plusieurs tabs par fenêtre, plusieurs panneaux par tab, de détacher les tabs vers des fenêtres, etc.

Il y a également un formidable 'Hotkey panel', un mini-terminal dont l'apparition est déclenchée par l'appui d'une combinaison de touches.

Ce mini-terminal 'slide' du haut ou bas de l'écran : on tape la commande, et hop il disparaît. Bien pratique.

#### Config

Au lieu de lister les options à modifier, ce qui serait fastidieux, je vous donne en exemple des screenshot de ma config.

![](https://aya.io/blog/images/iterm2-prefs-01.png)

![](https://aya.io/blog/images/iterm2-prefs-02.png)

![](https://aya.io/blog/images/iterm2-prefs-03.png)

![](https://aya.io/blog/images/iterm2-prefs-04.png)

![](https://aya.io/blog/images/iterm2-prefs-05.png)

![](https://aya.io/blog/images/iterm2-prefs-06.png)

Fichiers à importer : [couleurs, dont Solarized](https://github.com/mbadolato/iTerm2-Color-Schemes), et [raccourcis clavier](http://brettterpstra.com/2011/08/12/option-arrow-navigation-in-iterm2/).

#### Thèmes

iTerm2 peut enregistrer, et donc importer, ses réglages : layout, couleurs, options, etc.

Il existe sur le web de nombreux sites qui proposent de magnifiques thèmes.

J'ai pour ma part une préférence pour Solarized Dark, qui en plus d'avoir une gamme de couleurs absolument superbe, propose un contraste équilibré et reposant.

![ayadn solarized](https://aya.io/blog/images/ayadn-checkins.png)

### A l'ancienne

Vous voulez retrouver les conditions de travail des hackers de la grande époque ?

Essayez [Cool Retro Term...](https://github.com/Swordfish90/cool-retro-term)

## Conclusion

J'ai essayé de rester simple dans mes explications tout en n'omettant pas les éléments importants, pourtant probablement déroutants au premier abord, j'en suis bien conscient.

Nous n'avons fait que survoler le sujet, mais je crois que nous en avons vu assez pour que, même si vous n'en reteniez qu'une partie, vous pouviez déjà vous sentir plus à l'aise.

Il n'y pas de véritable synthèse à proposer ici : je vous invite au contraire à considérer ce tutoriel comme une première étape vers un univers qui, s'il paraît aride au début, se révèle rapidement magique.

En fait, je vous laisse apprécier, en guise de conclusion, les commandes inscrites sur le t-shirt de la dame...

![](https://aya.io/blog/images/morebeer.jpg)
