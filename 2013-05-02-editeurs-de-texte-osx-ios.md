---
title: "Éditeurs de texte OSX et iOS"
date: "2013-05-02"
categories: 
  - "apps"
  - "dossier"
  - "ios"
  - "macos"
  - "markdown"
---

Je vous propose dans cet article de partager mon retour d'expérience concernant les applications d'édition et de traitement de texte pour Mac OSX et iOS.

Après avoir exploré quelques méthodes et possibilités d'utilisation, nous essaierons de choisir simplement le bon outil pour la bonne tâche.

#### Ce que vous ne trouverez pas ici

- un comparatif exhaustif des éditeurs de texte pour OSX et iOS
- un tutoriel concernant les éditeurs de texte pour OSX et iOS

#### Ce que vous trouverez ici

- de bonnes raisons d'écrire en texte pur ou en Markdown
- des critères vraiment importants pour choisir son éditeur de texte
- un point de vue humain, sans sponsor à satisfaire
- des choix qui reflètent mes préférences mais qui s'ouvrent aussi aux autres options

# Contexte

J'ai déjà mentionné dans mon [guide sur nvALT](http://aya.io/blog/nvalt-prise-de-notes) que je préférais utiliser des **formats texte** pour écrire.

Je ne veux pas utiliser de logiciels générant des formats de fichier tels que le `.doc` de Microsoft Word ou quelconque autre format illisible en dehors de l'application qui le crée.

> Evidemment j'aimerais pouvoir bénéficier de cette liberté dans le monde du travail, mais ce n'est pas encore vraiment d'actualité en dehors des univers du Web et des technologies modernes. Les entreprises plus classiques ont encore du mal à penser en des termes autres que Word et Excel...

Savez-vous ce que contient réellement un fichier Word ? Des données binaires, inutilisables en dehors de Word ou d'un logiciel compatible.

Voici en image le contenu d'un fichier `.docx` dans lequel j'ai simplement écrit la phrase "Bonjour mes amis !" :

![](https://aya.io/blog/images/docx-aya.jpg)

Bien sûr il existe aujourd'hui des logiciels compatibles, qui permettent de lire ces fichiers sans acheter Word, par exemple [Libre Office](https://www.libreoffice.org/), mais ça ne résoud pas le problème de l'accès aux fichiers sur une machine qui n'est pas équipée de logiciel compatible...

Ca ne résoud pas non plus le problème de la pérénnité de vos textes, qui sont liés (menottés) à un logiciel ou à une marque.

**Le principal avantage d'un simple fichier texte est que son contenu est toujours accessible**.

Quelle que soit la machine, PC, Mac, iPhone, téléphone, voiture, frigo, que sais-je, il ne sera pas necessaire de l'équiper d'un logiciel particulier pour pouvoir ouvrir _vos propres fichiers_ : ils seront toujours là, lisibles, prêts à l'usage.

Le format texte n'est pas près de disparaître...

Même quand Windows, Mac OSX, iOS, Androïd et autres auront disparu du paysage, vos fichiers textes seront toujours lisibles, qu'ils soient "plats" ou en Markdown.

> J'ai débuté sur CP/M avec PROTEXT, vous vous souvenez, sur le 464 ? Allons, ce n'était qu'il y a 30 ans, quoi. CPquoi ? PROquoi ?

De plus, il est pour moi inconcevable de mélanger le contenu et le contenant si je dois produire du rédactionnel, autrement dit je ne veux pas me soucier de _présentation_ pendant que je rédige.

**Penser à la _structure_, oui, et de plus ça aide à structurer sa pensée également ; penser également aux altérations de texte qui portent du sens : italiques, gras, titres, tableaux, notes de pied de page, liens, etc.**

**Mais surtout, ne pas embourber son processus de rédaction avec des éléments de pure cosmétique (polices de caractères, couleurs, images, alignements, marges, etc).**

C'est d'ailleurs principalement pour cette raison que John Gruber a créé Markdown : il souhaitait rédiger des pages Web pleines de contenu sans avoir à taper toutes les balises HTML, fastidieuses, et qui rendent le texte illisible.

Le flot de mots et phrases doit pouvoir se construire facilement sans être interrompu.

Une chose à la fois. On ne fait pas l'ingénieur du son quand on compose de la musique, on ne fait pas le designer quand on écrit.

> Il faudra que j'en parle un jour. La possibilité pour un musicien d'avoir un home-studio en a rendu certains incapables de composer dans leur installation, car ils se perdaient toujours dans les réglages à essayer de trouver un beau son, sans réussir, et pendant ce temps-là, la belle idée qui leur avait fait empoigner leur instrument faisait pshiit...

Et non seulement l'application ne doit pas nous déranger, mais elle doit nous soutenir et s'adapter à nos besoins (ben quoi c'est permis de rêver hein).

Le texte achevé, relu et corrigé, on peut s'attaquer à son habillage, à son aspect.

Markdown est fait pour ça : ce format texte lisible à l'oeil nu se transforme nativement en HTML et est donc décorable par du CSS, de manière à obtenir n'importe quel aspect désiré.

Pas d'affolement, il n'est nullement necessaire de connaître ces deux technologies du Web pour écrire en Markdown ou pour exporter son texte : un bon éditeur de texte est justement capable de s'en occuper de manière satisfaisante.

# Critères

Nous écartons ainsi toute application qui ne gère pas nativement des fichiers texte (`hello.txt` par exemple) ou Markdown (`hello.markdown`, `hello.md`).

Cela exclut bien sûr tout fonctionnement avec une base de données, car celles-ci fonctionnent avec des données binaires, très rarement avec du texte pur.

Nous laissons également de côté les formats pseudo ouverts tels `.rtf`, `.odt`, `.sxw`, etc, car ils présentent au final le même défaut que les formats de Microsoft.

L'essentiel étant de pouvoir manipuler les fichiers manuellement en cas de besoin ou à des fins de sauvegarde, même si l'application qui utilise les fichiers propose un paradigme de fonctionnement différent (niveau d'abstraction élevé par rapport au système de fichiers).

**De la prise de notes occasionnelle au roman ou au scénario, les besoins de quelqu'un qui écrit sont multiples et variés, et un seul outil ne peut pas satisfaire correctement toutes les situations**.

En essayant tout de même de ne pas tomber dans la surconsommation, car jongler entre une dizaine d'éditeurs de texte n'est pas non plus l'idéal et peut mener à beaucoup de temps perdu et de confusion, nous allons essayer de choisir quelles sont les applications qui pourraient mériter de figurer dans notre Mac ou notre iPad.

> Tout ceci est filtré selon mes propres critères, mais si vous cherchez un comparateur exhaustif des applications disponibles, [Google](https://www.google.fr/search?q=os+x+markdown+editor) est votre ami, ainsi que [Brett Terpstra](http://brettterpstra.com/ios-text-editors/), comme d'habitude.

Je trouve personnellement que trois ou quatre éditeurs bien différents les uns des autres permettent de se sortir efficacement de toutes les situations.

J'ai choisi de travailler mes textes dans quatre logiciels essentiellement :

- [nvALT](http://brettterpstra.com/projects/nvalt/)
- [iA Writer](http://www.iawriter.com)
- [Mou](http://mouapp.com/)
- [Sublime Text 2](http://www.sublimetext.com)

J'explique dans cet article pourquoi et comment j'en suis arrivé à ces choix.

N'oubliez pas que c'est un choix actuel : il est évident que si un nouvel éditeur de qualité apparaît sur le marché, il faudra considérer son utilité et l'éventualité de changer de monture.

_Mais tout d'abord, un point sur le fait que je conseille toujours, en plus de s'en tenir aux fichiers texte, de prendre l'habitude d'écrire en Markdown._

# Markdown

Je prends systématiquement mes notes et je rédige tous mes textes en Markdown.

Qu'est-ce que c'est ?

C'est simplement un jeu de symboles à utiliser pour structurer le texte.

Markdown, c'est du texte normal + des éléments supplémentaires qui permettent, une fois le fichier Markdown exporté dans un autre format, de bénéficier de mise en page et de formatage.

Voici un petit exemple de texte écrit en Markdown :

```markdown
    # Chapitre 1

    ## Sous-titre

    Texte de paragraphe. Tout texte sans symbole supplémentaire est traité comme du simple texte. Mais si l'on rajoute par exemple le signe `#` devant une ligne, cette ligne devient un titre. En doublant ce signe on obtient un titre de niveau de 2, et ainsi de suite.

    Un mot ou une phrase entourés d'étoiles seront en *italique*, tandis qu'un mot ou une phrase entourés de deux étoiles seront en **gras**.

    On peut utiliser les tirets à la place : _phrase en italique_ et __phrase en gras__.

    Il suffit de sauter une ligne pour commencer un nouveau paragraphe.

    On peut créer des listes avec des traits, étoiles ou chiffres :

    - premier élém`ent de la liste
    - deuxième élément de la liste

    1. une autre ligne de liste
    2. encore une autre
```

Comme vous avez pu le remarquer, on dirait du texte normal.

_Bien sûr, puisque ça en est !_

Markdown est un système qui permet de structurer sans avoir à se soucier de décoration.

Une fois le texte terminé, vous déciderez que les titres seront de telles police, de telle taille et couleur, que les paragraphes seront de telle hauteur de ligne, etc.

_Une fois le texte terminé, tout sera déjà prêt à être habillé._

Exemples crées en deux minutes avec [Marked](http://markedapp.com/) à partir de l'extrait ci-dessus :

![](https://aya.io/blog/images/marked-antique-aya.jpg)

![](https://aya.io/blog/images/marked-citizen-aya.jpg)

![](https://aya.io/blog/images/marked-dark-aya.jpg)

Vous disposez de fichiers texte écrits en Markdown, lisibles tels quels, mais également utilisables par des applications qui vont décorer le texte, l'exporter en pdf, en epub, en html, etc.

Apprendre le Markdown est facile, vous venez de le faire !

Bien sûr il n'y a pas que ça, mais c'est l'idée de base, et ça suffit pour les usages courants.

# Exigences

Les applications que nous allons sélectionner doivent donc être compatibles Markdown, sans exception.

Elles devront proposer également au moins un système de synchronisation, l'idéal étant d'en proposer plusieurs, dont iCloud et Dropbox nativement.

En effet, on ne peut plus, de nos jours, se contenter de stocker ses précieux fichiers dans un seul appareil et de s'occuper soi-même de leur envoi vers d'autres machines.

Et bien entendu l'éditeur ne doit jamais perdre un seul mot ou un seul fichier, même en cas de plantage de l'application : le contenu doit être en sécurité à tout instant.

_Je sépare les critères de qualité qu'un éditeur de texte doit avoir en quatre catégories, selon les situations et les types de texte à rédiger : urgence, note, texte court, texte long._

## Pour les urgences

Dans les situations stressantes ou d'urgence, ou encore dans un moment de confusion ou si votre correspondant ne peut pas répéter à l'envi, il est important de pouvoir prendre une petite note instantanément, comme un nom ou un numéro de téléphone.

Une telle application sera souvent de type "post-it".

Elle ne proposera pas forcément de gestion de fichiers : on tape directement et c'est immédiatement pris.

Click sur l'app ou raccourci-clavier _puis_ commencer à taper la note immédiatement, sans attente ni contrainte : voilà la fonction d'une telle application.

Dans cette catégorie, les applications OSX que j'ai considéré avant de faire mon choix sont [Noti](http://initsyndicate.com/noti/) et [Simplenote](http://simplenote.com/).

Noti fonctionne bien et se synchronise avec iCloud.

Un click et vous notez : c'est ce qu'on veut.

**Bien sûr l'app est vraiment loin d'être parfaite, mais dans cette catégorie, je les trouve franchement toutes moyennes.**

Il y en a de nombreuses autres, et certaines pourraient vous plaire, mais je n'en ai trouvé aucune qui utilise Markdown et qui se synchronise avec Dropbox.

Vu que je n'aime pas utiliser Simplenote dans ce genre de situation urgente, le choix a été fait rapidement...

Pour iOS : [Noti](http://initsyndicate.com/noti/) également.

![](https://aya.io/blog/images/draft-aya.jpg)

Sur Androïd, j'utilise aussi [Draft](https://play.google.com/store/apps/details?id=com.mvilla.draft), qui se synchronise avec Dropbox et qui permet d'écrire rapidement, même si l'accès n'est pas exactement instantané comme je le souhaiterais.

**Au final, pour mon usage personnel, sur le Mac, j'improvise sur le moment quand il s'agit de noter un numéro de téléphone ou une simple citation : un coup TextEdit, un coup Sublime Text s'il est ouvert, un coup nvALT si j'ai un titre en tête au moment de noter l'élément, etc.**

De toute façon, au final, je copie ce que je viens de taper en urgence et j'en fais ensuite une note titrée et taggée dans nvALT.

En revanche, sur le Galaxy SII, Draft est vraiment très bien et j'ai pris l'habitude de m'en servir.

Je ne tape pas de "post-it" sur mon iPad, je n'ai donc pas d'expérience personnelle à proposer en la matière.

On commencera néanmoins à trouver au chapitre suivant de bons éditeurs pour iOS, patience...

## Pour la prise de notes

La prise de notes plus traditionnelle doit bénéficier d'un accès rapide à la création, aucune attente n'est non plus acceptable.

Ce n'est pas quand on veut prendre une note, et donc par définition quand on manque de temps ou de mémoire, que l'on peut se permettre de chercher comment fonctionne une application ou d'attendre qu'elle daigne bien s'ouvrir.

Cependant comme la situation n'est généralement pas _urgentissime_ on peut tout de même prendre deux secondes pour créer un _titre_.

Il ne faut juste pas de gestion compliquée : s'il faut décider d'un dossier à utiliser ou si l'application exige de faire une mise à jour avant de pouvoir commencer à écrire une simple note, ce n'est pas bon…

L'application doit également proposer une synchronisation automatique des notes entre différents appareils, sinon ça n'est pas très utile...

On doit pouvoir aussi retrouver facilement une note par son titre ou un mot contenu dans les textes.

Gérer les tags (mots-clés) est bien entendu un plus non négligeable.

> Bien qu'il n'existe pas de solution évidente pour manipuler des tags de manière pérenne dans un fichier texte, on pourra utiliser [Open Meta](https://code.google.com/p/openmeta/) sans contraintes dans son système de notes. Il ne faut pas en revanche s'attendre à un fonctionnement parfait : si votre fichier `alloquoinonmaisallo.txt` contient le tag `pouf`, mais que vous ouvrez ce fichier dans une application qui ne comprend rien aux tags Open Meta, vous perdrez ce tag (l'application ignorante ignorera le tag quand elle enregistrera le fichier à son tour).

Dans cette catégorie, les applications OSX que j'ai considéré avant de faire mon choix sont : [Notational Velocity](http://notational.net), [nvALT](http://brettterpstra.com/projects/nvalt/), [Simplenote](http://simplenote.com/).

Pour iOS : [Nocs](http://www.wisd.com/nocs/) et [Simplenote](http://simplenote.com/).

Et toujours [Draft](https://play.google.com/store/apps/details?id=com.mvilla.draft) sur Androïd.

### nvALT

**C'est très clairement mon favori, et de loin.**

Je vous renvoie à mon [guide d'utilisation de nvALT](http://aya.io/blog/nvalt-prise-de-notes) pour en savoir plus.

_Notational Velocity, étant son vieux cousin, fonctionne à peu près de la même façon, la modernité en moins._

### Simplenote

[Simplenote](http://simplenote.com/) est facile à utiliser, mais nécessite de créer un compte chez eux, ce qui me déplaît fortement.

Il faut aussi passer par leur système de synchronisation, certes rapide, mais qui a déjà connu des problèmes par le passé : encore une contrainte.

Cependant, si vous débutez et que nvALT vous fait peur, alors pourquoi pas... à condition de ne pas oublier de changer quand vous deviendrez plus expérimenté.

### Nocs

Question design, ce n'est pas l'application de l'année, mais question fonctionnalité, pour une app gratuite, c'est top !

![](https://aya.io/blog/images/nocs-small-aya.jpg)

Sur iPad, en tout cas, l'utilisation de [Nocs](http://www.wisd.com/nocs/) est très agréable.

Une fois désigné le dossier Dropbox qui contient vos notes en txt ou Markdown, Nocs y accède d'un click et peut également enregistrer vos nouvelles notes immédiatement.

> Un des avantages de Nocs est qu'il est possible de naviguer dans n'importe quel dossier de la Dropbox, contrairement à nombre d'apps qui désignent d'office un dossier qu'elles créent.

Nocs permet de personnaliser l'affichage des notes : couleur du fond et du texte, polices de caractères, taille des caractères...

Mieux et rare : Nocs permet de personnaliser les éléments de Markdown, c'est-à-dire la façon qu'à l'app de "traduire" votre marquage Markdown en éléments HTML. Par exemple, on peut désactiver la transformation des liens, des images, listes, etc.

Nocs est de plus compatible avec la version iOS de [TextExpander](http://smilesoftware.com/TextExpander/index.html), un avantage indéniable.

## Pour les textes courts

Tout ce qui dépasse les quelques lignes peut être considéré comme un texte court (merci Sherlock).

Un éditeur de texte idéal pour les textes courts doit proposer un moyen de se concentrer sur un chapitre ou une section en particulier.

Ce type d'éditeur propose souvent un mode "distraction free", c'est-à-dire une option d'affichage qui cache tous les menus et boutons pour ne laisser apparaître que le texte au centre de l'écran.

C'est différent du véritable mode "plein écran", c'est une option supplémentaire.

Avec un tel éditeur, on doit pouvoir rapidement rédiger ou modifier une partie d'un texte de quelques pages maximum sans avoir à manipuler de menus, boutons ou raccourcis clavier.

Dans cette catégorie, les applications OSX que j'ai considéré avant de faire mon choix sont : [Byword](http://bywordapp.com/), [Mou](http://mouapp.com/), [WriteRoom](http://www.hogbaysoftware.com/products/writeroom), [iA Writer](http://www.iawriter.com/mac/), [Texts.io](http://www.texts.io/) et [TextWrangler](http://www.barebones.com/products/textwrangler/index.shtml).

Pour iOS : [Nocs](http://www.wisd.com/nocs/), [Elements](http://www.secondgearsoftware.com/elements/), [WriteRoom](http://www.hogbaysoftware.com/products/writeroom), [iA Writer](http://www.iawriter.com/) et [Textastic](http://www.textasticapp.com/).

### WriteRoom

Ancêtre de ce type d'éditeur, [WriteRoom](http://www.hogbaysoftware.com/products/writeroom) était vraiment révolutionnaire lors de son apparition.

Malheureusement, je trouve que cette app souffre de défauts rédhibitoires sur OSX.

Par exemple, il m'est arrivé que l'app ouvre une boîte de dialogue pour me proposer je-ne-sais-quoi alors que je suis en train d'écrire. Ca, vous l'aurez compris, je ne suis pas d'accord du tout.

J'ai également eu un problème avec Markdown, qui d'un coup n'était plus "traduit", m'obligeant à relancer l'app. Tss-tss, pas cool.

Sur iOS c'est mieux, l'app fonctionne bien.

Mais elle est de toute façon complètement dépassée par ses successeurs. Allez, à la retraite.

### iA Writer

Plus toute jeune non plus, [iA Writer](http://www.iawriter.com/mac/) est assez radicale : on est en mode "distraction free" _par défaut_.

![](https://aya.io/blog/images/iawriter-aya.jpg)

Il n'y a pas de préférences non plus, rien à régler. On aime ou pas.

Le texte centré, un jeu de décoloration nous force à nous concentrer sur la phrase en cours (mode "focus"), servie par de superbes polices de caractères au rendu extraordinaire.

Minimaliste et magnifique.

Rien d'autre à faire qu'écrire, comme sur une noble machine à écrire de grande qualité.

Ce qu'est exactement iA Writer, que j'aime beaucoup pour cette raison.

### Byword

[Byword](http://bywordapp.com/) est assez proche d'iA Writer dans son apparence, une fenêtre minimaliste pour se concentrer sur le texte, mais propose en plus quelques options et fonctions.

Les menus et raccourcis-clavier permettent de mettre en italique, gras, souligné, barré, etc, le texte que vous avez sélectionné, mais aussi d'insérer des liens, changer l'indentation, etc.

![](https://aya.io/blog/images/byword-aya.jpg)

Bien évidemment on n'est pas obligé d'utiliser ces mécaniques et l'on peut tout simplement écrire les symboles Markdown à la main.

Byword est plutôt agréable pour écrire du texte rédactionnel de taille moyenne, mais n'est pas terrible pour taper du code, ce qui n'en fait pas un outil idéal pour écrire des tutoriels techniques.

Un peu moins joli que iA Writer, mais joli quand même, Byword pour OSX semble inutile si l'on possède déjà un bon éditeur, mais propose finalement une apparence assez cool et un fonctionnement assez souple pour trouver sa place entre une app de prise de notes et un éditeur de texte plus évolué.

### Texts.io

Mention spéciale à [Texts](http://www.texts.io/), une appplication du type Byword, _gratuite et multi-plateforme_, que l'on retrouve donc également sous Windows.

_Texts_, tout comme _Byword_, est recommandé aux débutants qui craignent d'oublier les symboles Markdown, car il propose des menus et des raccourcis clavier faciles à retenir pour la plupart des éléments : titres, italique, gras, listes, pieds de page, etc.

### TextWrangler

Version allégée et _gratuite_ de [BBEdit](http://www.barebones.com/products/bbedit/index.shtml), [TextWrangler](http://www.barebones.com/products/textwrangler/index.shtml) est un éditeur de texte dédié au code mais qui est également agréable à utiliser pour du rédactionnel.

![](https://aya.io/blog/images/textwrangler-aya.jpg)

TextWrangler propose une coloration syntaxique pour de très nombreux langages et systèmes, y compris Markdown, ce qui le rend plutôt efficace dans le cadre de la rédaction de textes techniques.

De nombreuses fonctions d'édition avancée sont présentes : recherche, filtres, modalités d'affichage, etc.

**Une fonction très appréciable pour une app gratuite est le "fold", le repliement de blocs de texte, qui permet de faciliter la lecture et l'édition.**

Une application d'apparence un peu "old school" mais qui propose un jeu de fonctions complet.

### Mou

**[Mou](http://mouapp.com/) est un _excellent_ éditeur de texte gratuit.**

Doté de toutes les fonctions nécessaires que nous avons déjà présenté dans d'autres apps, comme la transformation de texte par menus et raccourcis en plus de la syntaxe Markdown, Mou propose en plus des fonctions originales et très appréciables.

S'il peut afficher une fenêtre classique comme les autres, Mou est surtout connu pour son mode "double panneau synchronisé".

D'un côté le texte en Markdown, qui bénéficie de coloration syntaxique, et de l'autre côté, _synchronisé_, le rendu en HTML+CSS.

![](https://aya.io/blog/images/mou-aya.jpg)

Les deux panneaux défilent en même temps mais pas à la même vitesse : Mou détecte les différences de taille entre le texte (taille fixe) et le rendu (titres plus gros, blocs de code, images, etc) et adapte la vitesse de défilement.

C'est _très_ pratique pour les textes destinés à être publiés et dont vous souhaitez contrôler le rendu au fur et à mesure que vous écrivez.

Vous pouvez choisir des thèmes pour le côté texte, et fournir un fichier CSS de votre choix pour le rendu.

Original : Mou est également capable de s'afficher "verticalement", c'est-à-dire en mode portrait, certainement utile si l'on travaille avec un écran de ce genre.

Et aussi insertion de la date par raccourci clavier, manipulation de blocs de texte, recherche et remplacement, etc.

**Pour la rédaction de textes de taille moyenne, Mou est clairement mon favori.**

Mais encore une fois, j'aime utiliser des outils adaptés, et ne pas me limiter : selon la situation, j'utilise donc Mou (souvent), iA Writer (pour réfléchir), ou Byword (pour des petits textes littéraires).

### Elements

Sur mon iPad, j'utilise principalement [Elements](http://www.secondgearsoftware.com/elements/).

![](https://aya.io/blog/images/elements-h-small-aya.jpg)

Il n'y a pas grand chose à dire : quand une application est si jolie et marche tout simplement très bien, fait tout ce qu'on lui demande et ne plante pas en mangeant les fichiers, c'est _cool_.

Pour le code je préfère cependant [Textastic](http://www.textasticapp.com/)... tout en précisant que je n'aime pas coder sur l'iPad.

Disons que je préfère en fait, sur l'iPad, me connecter au Mac en SSH ou VNC et utiliser un éditeur OSX...

> Ca tient surtout au fait que Textastic et ses confrères éditeurs de code moins bien dotés partagent tous le même défaut, qui est de stocker sur l'iPad des versions obsolètes de fichiers de code sur lesquels j'ai retravaillé ailleurs entre temps, et que je ne veux pas prendre le risque de pousser par erreur vers le Mac à partir de l'iPad, vautré dans le canapé...

## Pour les textes longs

La rédaction de textes longs exige un outil stable et efficace.

Cette efficacité provient de fonctions dont nous n'avons pas forcément l'usage pour des textes courts mais qui deviennent vite indispensables pour des formats longs :

- gestion des chapitres (possibilité d'en changer l'ordre)
- vue optimisée (annotations, chapitres repliés, etc)
- bibliothèques d'éléments ou de tags
- templates (modèles) de mise en forme
- gestion des versions du document
- création automatique de table des matières
- statistiques (nombre et fréquence des signes et mots par exemple)
- outils dédiés à la création (cartes à idées, thesaurus, etc)

Dans cette catégorie, les applications OSX que j'ai considéré avant de faire mon choix sont : [Scrivener](http://www.literatureandlatte.com/scrivener.php), [Ulysses](http://ulyssesapp.com/), [Multi Markdown Composer](http://multimarkdown.com/), et en bonus [Sublime Text 2](http://www.sublimetext.com).

Pour iOS : rédiger de longs documents sur un iPad n'est pas très pratique, et sur un iPhone n'en parlons pas. Néanmoins si vous ne pouvez pas faire autrement, la sélection d'apps pour les textes courts évoquée auparavant devrait en partie vous satisfaire.

### Ulysses III

[Ulysses III](http://ulyssesapp.com/) est un éditeur qui connaît un certain succès actuellement.

Une des raisons de ce succès, outre ses qualités propres, est qu'il se marie avec [Daedalus Touch](http://daedalusapp.com/) sur iOS, permettant de rester dans un environnement homogène.

![](https://aya.io/blog/images/ulyssesdaedalus-aya.jpg)

Ulysses III propose de nombreuses fonctions très intéressantes, comme une gestion des fichiers qui s'apparente à celle d'une bibliothèque, et surtout une abondance de petites palettes de contrôle, flottantes, permettant d'intervenir sur tous les réglages et fonctions du logiciel.

Ulysses III a aussi pour lui un superbe moteur de rendu de texte, différent de iA Writer (pas le même genre), mais tout aussi beau.

Néanmoins certains problèmes demeurent.

Cette gestion centralisée des fichiers est sympathique, mais elle ne marie que iCloud et le stockage local, il n'y a pas encore de fonctions pour accéder à Dropbox ou à un autre service de synchronisation dans le cumulonimbus.

J'ai aussi eu quelques comportements étranges avec la liste de fichiers. Peut-être un problème avec iCloud, je ne sais pas.

D'autre part, je trouve que l'écran est vite encombré, et si on fait de la place, on perd un peu l'intérêt d'Ulysses qui sont ces petites fenêtre flottantes.

Bref, ce n'est pas une app que j'adore, même si dois reconnaître qu'elle est très bien faite, et qu'elle mérite totalement son succès actuel.

### Multi Markdown Composer

[Multi Markdown Composer](http://multimarkdown.com/) était l'éditeur préféré de nombre de rédacteurs avant l'apparition d'Ulysses III.

C'est un logiciel très efficace, avec lui aussi pléthore de palettes flottantes, fonctions, gestion des fichiers, etc.

On trouvera également une sidebar proposant une table des matières du document, c'est assez rare pour un éditeur de ce prix, ainsi que les plus classiques fenêtres de prévisualisation, export en PDF ou HTML, etc.

Si vous ne voulez pas dépenser 40€ pour Ulysses, vous pouvez vous rabattre sans hésitation sur Multi Markdown Composer qui ne coûte que 11€.

Un peu moins _hype_, mais tout à fait capable. :)

### Scrivener

[Scrivener](http://www.literatureandlatte.com/scrivener.php) est un éditeur de texte très connu du monde des scénaristes et écrivains.

C'est également un traitement de texte très prisé des... éditeurs, correcteurs et relecteurs.

Scrivener est en quelque sorte le concurrent direct et abordable de [Final Draft](http://www.finaldraft.com), le célèbre traitement de texte pour scénaristes, aujourd'hui complètement dépassé et bien trop onéreux.

Scrivener est une application très complète, professionnelle, dotée de _centaines_ de fonctions utiles et remplissant des rôles très précis.

Il serait vraiment hors-sujet et fastidieux d'effectuer une étude de Scrivener ici ; il faut simplement savoir que si vous comptez rédiger un livre, un scénario ou toute oeuvre conséquente et nécessitant une gestion de nombreuses pages et chapitres, glossaires, index, etc, Scrivener est tout simplement le meilleur de sa catégorie.

Une petite sélection de ce que j'aime dans Scrivener :

- cartes à idées / pinboard
- tous les éléments (paragraphes, chapitres, etc) sont ré-arrangeables : parfait pour essayer différentes structures ou versions alternatives
- et donc évidemment gestion des versions avec fusion/différence, annotations, révisions, etc
- moteur unique de compilation du document : la fonction d'export de Scrivener est un monstre permettant de sortir un in-folio tout comme une encyclopédie en 12 tomes
- traitement intelligent des dialogues (centrage automatique des noms, etc)

Et avec ça nous sommes très loin d'avoir fait le tour.

Bref, à ce prix-là, si vous hésitiez, n'hésitez plus !

### Sublime Text 2

J'ai réservé une petite surprise pour la fin.

Mon éditeur Markdown favori _toutes catégories confondues_ est... [Sublime Text 2](http://www.sublimetext.com/) !

Sublime Text 2, à la base, c'est tout simplement le meilleur éditeur de code actuellement sur OSX.

C'est pour le moi le nouveau Vim ou Emacs.

> Comment ça je trolle ? Pas du tout, je le pense vraiment. Et la version 3 qui se prépare à l'air tout simplement grandiose.

Il est déjà bien cool pour le Markdown à la base, surtout grâce à ses snippets et extensions de texte automatisées (marié à TextExpander c'est une tuerie).

Rien qu'une fonction de Sublime Text 2 qui me fait pleurer de bonheur : le mini-map sur le côté.

C'est une petite colonne qui représente une vue miniaturisée de votre document, permettant de se repérer en un clin d'oeil.

![](https://aya.io/blog/images/st2minimap-aya.jpg)

Bon allez, une autre fonction : si vous avez l'habitude de naviguer dans tous les fichiers texte d'un projet à la souris, arrêtez tout de suite le massacre. Tapez `CMD+P` et s'affiche une petite barre façon [Alfred](http://www.alfredapp.com/).

Tapez le début _ou n'importe quelle partie_ d'un nom de fichier, et ce fichier et ceux ayant un nom semblable apparaissent sous la barre immédiatement, prêts à être ouverts d'une seule touche.

Ca semble simple, mais c'est unique, ultra rapide et d'une efficacité redoutable.

Mais Sublime Text 2 prend encore une toute autre ampleur après avoir installé les [plugins et thèmes de Brett Terpstra](http://ttscoff.github.io/MarkdownEditing/).

Raccourcis clavier intelligents, autocomplétion des astérisques, tirets et autres parenthèses, centrage du texte avec largeur bien pensée, mode focus sur le paragraphe, thèmes "distraction free" sont parmi les quelques bonus formidables que vous offre ce plugin.

Mariez ça avec [Marked](http://markedapp.com/), son application de prévisualisation et d'export pour Markdown, et vous obtenez le meilleur des mondes, tout simplement.

# Conclusion

Je me suis amusé à suivre l'évolution de mes essais d'applications pour la rédaction de cet article.

C'est-à-dire que j'ai commencé par quelques lignes et mots-clés dans nvALT, un peu façon "brainstorming", puis j'ai tracé une structure globale et couché quelques idées supplémentaires dans Byword.

> Le seul vrai unique brainstorm est [Brainstorm](http://www.imdb.com/title/tt0085271/), le chef-d'oeuvre de Douglas Trumbull.

J'ai ensuite écrit plusieurs paragraphes dans iA Writer, avant de finalement relire, corriger et reprendre le tout dans Mou, où j'ai développé l'essentiel du contenu.

Peu après avoir atteint la barre des 2000 mots j'ai ouvert mon fichier Markdown dans Sublime Text 2, où je me suis laissé porter jusqu'à la fin, ajoutant quelque 3000 mots supplémentaires de rédactionnel ainsi que tout ce qui est images, code, liens externes, références de pied de page, etc.

> Je trouve ça un peu idiot mais on dit souvent qu'il y a plusieurs barrières à passer quand on écrit : la première phrase, les 100 premiers mots, puis 800, 2000, 5000, 30000 et ainsi de suite. Pas trop d'accord en fait, écrire n'est pas un marathon, on gère son timing, et la valeur n'est pas dans la quantité. _Yé né soui pa zoune machine !_

A aucun instant un de ces logiciels n'a failli à sa tâche.

Ecrire cet article a été un grand plaisir, notamment grâce à toutes ces applications merveilleuses ; j'espère que vous aurez également pris du plaisir à le lire, mais surtout qu'il vous aura donné envie d'abandonner les sodas et d'attaquer les boissons d'homme (qui ont un certain goût de pomme)... ;)
