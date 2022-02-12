<!-- pi400-pixandneofetch.png  -->

Peut-on remplacer son Mac par un Raspberry Pi au quotidien ? Oui ! Enfin, non. Bon, ça dépend...

Ca ne marchera pas pour le développement iOS pour des raisons évidentes, mais pour tout le reste, ça le fait carrément bien, à condition de ne pas avoir peur de mettre les mains dans le cambouis.

Je raconte comment j'ai installé puis configuré, aux petits oignons, une station Raspberry Pi 400 ou Pi 4 avec Raspberry OS.

<!-- more -->

# Installer la distribution

Il faut installer Raspberry Pi OS sur une carte dédiée. Je conseille 16Go minimum. 32 seront confortables, et 64 est idéal si vous comptez manipuler des gros fichiers, mais le plus important est que la carte soit rapide, classe 10 et bon fabriquant sont indispensables.

Le plus simple pour l'install est d'utiliser l'app [Raspberry Imager](https://www.raspberrypi.com/software/), disponible sur toutes les plateformes. 

![pi imager](images/pi400-piimager.png)

Dans l'app, sélectionnez la version de votre choix de Raspberry OS (32 ou 64 bits) mais surtout faites bien attention à choisir **Raspberry OS** et non pas Ubuntu par exemple, qui est complètement buggée pour Pi.

La version 64 bits est 20% plus rapide, mais occupe deux fois plus de place et mange plus de RAM. Perso j'ai pris la version 32 bits, largement assez véloce sur le Pi 400 de toute façon.

Une fois l'image copiée sur la carte vous pouvez l'insérer dans le Pi puis démarrer. 

Ensuite suivez les instructions pour la configuration de base - WIFI, timezone, langage, username, password, etc, tut est simple et visuel.

Arrive un moment où le bureau sera chargé. C'est le gestionnaire LXDE avec le bureau PIXEL spécialement conçu pour les Pi. Sympa, mais très limité. Nous allons le remplacer par Xfce 4, tout aussi léger mais bien plus configurable et arrangeant, surtout avec 4 Go de RAM.

# Installation Xfce

Pour un Pi, c'est l'environnement de bureau idéal. Bien sûr vous pourriez installer un KDE Plasma ultramoderne, ça passe avec 8 Go de RAM, mais je trouve que ça fait un peu contresens sur un Pi. On pourrait aussi de l'autre côté choisir un environnement minimaliste, ce qui est parfaitement valable - mais aujourd'hui nous allons suivre la voie du milieu.

Il y a dans Raspberry OS un petit assistant qui va nous faciliter la tâche.

Faites

```bash
sudo tasksel
```

puis dans le menu sélectionnez Xfce et appuyez sur Espace pour sélectionner, puis Tab pour aller sur Ok puis Enter.

Tasksel va télécharger tous les fichiers nécéssaires à Xfce puis les installer proprement.

Ensuite nous voulons remplacer le login automatique vers PIXEL par un login automatique vers Xfce. Ca se fait avec un autre utilitaire :

```bash
sudo update-alternatives --config x-session-manager
```

Dans la liste, sélectionnez "Xfce4" en pressant le numéro correspondant.

Ensuite un reboot et on c'est ok.

Au redémarrage, si Xfce vous propose un "panel" par défaut, dites oui pour faciliter la config, même si personnellement je l'ai enlevé tout de suite après. Je garde le panel du haut, qui fait "power bar", mais j'enlève le panel du bas qui fait "Dock".

# Dracula

[Dracula](https://draculatheme.com/) est un thème - palette de couleurs, décoration de fenêtres, etc - qui a la particularité d'être disponible pour plus de 200 applications, ce qui permet d'obtenir un résultat homogène. Vous pouvez appliquer Dracula non seulement au bureau, fenêtres, icônes, menus, mais aussi à tout le système et à toutes les apps : terminal, navigateur, traitement de texte, etc.

Tout ce que l'on installe dans ce tuto est thémé avec Dracula, y compris Vim et Zsh !

Je trouve que l'environnement de travail que l'on va installer est sublimé par ce thème, qui unifie parfaitement bien tous les éléments de l'interface graphique.

![fichiers et chromium](images/pi400-filesandchromium.png)

![menus](images/pi400-menus.png)

Si vous ne l'aimez pas, il vous faudra supprimer toutes les lignes de commande qui y font référence... ce qui serait dommage quand même ! Donnez-lui une chance, vous verrez c'est bien. :)

Sinon dans le même genre il y a aussi [catppuccin](https://github.com/catppuccin/catppuccin) qui est très apprécié.

# Thème

On commence par installer le thème Dracula pour le bureau.

```bash
cd ~/Downloads
curl https://github.com/dracula/gtk/archive/master.zip
curl https://github.com/dracula/gtk/files/5214870/Dracula.zip
mkdir ~/.themes
unzip master.zip -d ~/.themes/dracula
mkdir ~/.icons
unzip Dracula.zip -d ~/.icons/dracula
```

Allez ensuite dans Menu Principal > Gestionnaire de paramètres > Apparence, et choisissez "dracula" dans Style, et "Papirus-Dark" dans Icones.

![dossier images](images/pi400-pictures.png)

# Fenêtres

C'est la grande mode des "tiling window managers" dans le monde Linux, et c'est vrai que c'est très attirant de pouvoir organiser ses fenêtres de manière géométrique sans qu'elles ne se marchent jamais dessus. Mais l'installation et la configuration de ces WM (type Xmonad) est incroyablement complexe, et je laisse ça pour un prochain dossier.

A la place, ici, nous allons tout simplement créér un jeu de raccourcis clavier pour le gestionnaire de fenêtres, qui va nous permettre de caler les fenêtres sans avoir besoin de WM étranger.

Allez dans Menu Principal > Gestionnaire de fenêtres > Clavier, puis assignez des combinaisons de touches pour les actions "Agencer la fenêtre en mosaïque ...". Par exemple je reprends les codes de Vim pour me souvenir facilement donc j'ai mis Maj+Ctrl+J pour demi écran en haut, Maj+Ctrl+K pour demi écran en bas, Maj+Ctrl+H pour demi écran à gauche, et Maj+Ctrl+L pour demi écran à droite.

![windows shortcuts](images/pi400-windowprefs.png)

Si comme mi vous enlevez les menus des fenêtres ainsi que leurs bordures (en tout cas pour le terminal Xfce), le tout en association avec Tmux, vous vous retrouverez avec un bureau super clean et bien calé, sans avoir besoin de rien ajouter.

Profitez-en pour regarder les autres actions proposées, il y a plein de réglages sympa à faire dans ces préférences.

# Terminal

Beaucoup de geeks vous diraient, avec raison, qu'il faut un bon terminal pour pouvoir administrer Linux correctement, et vous proposeraient des terminaux modernes de type Alacritty, Kitty, Terminator, etc. Alors certes ils sont très bien, mais ils sont également complexes à paramétrer et ne me sont pas spécifiquement utiles - je trouve que le terminal Xfce4 est largement suffisant pour mes usages.

Pour installer Dracula dans le terminal Xfce :

```bash
git clone https://github.com/dracula/xfce4-terminal.git
cp xfce4-terminal/Dracula.theme ~/.local/share/xfce4/terminal/colorschemes
```

Relancez le terminal puis allez dans son menu Préférences > Apparence > Couleurs et choisissez Dracula.

# Zsh

Dans ce terminal on ne pas utiliser Bash au quotidien, mais Zsh. On va le gérer avec l'utilitaire "Oh my Zsh" :

```bash
sudo apt install zsh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
git clone https://github.com/dracula/zsh.git
cp zsh/dracula.zsh-theme ~/.oh-my-zsh/themes/dracula.zsh-theme
source ~/.zshrc
```

Ces commandes vont installer Zsh puis Oh My Zsh. Suivez ensuite le tuto proposé par OMZ pour faire vos réglages de base.

# PowerLevel10k

Ensuite on ajoute PowerLevel10k qui permet de confectionner une superbe ligne de commande. Il faut d'abord [télécharger les fonts Meslo](https://github.com/romkatv/powerlevel10k#meslo-nerd-font-patched-for-powerlevel10k) qui sont idéales pour ça. 

Téléchargez les fichiers TTF, copiez les dans `.fonts` et activez-les :

```bash
mkdir ~/.fonts
cp ~/Downloads/*.ttf ~/.fonts/
fc-cache
```

Ensuite faites

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

puis éditez `~/.zshrc` et commentez la ligne de thème Robby Russel et ajoutez cette ligne à la place :

```text
ZSH_THEME="powerlevel10k/powerlevel10k"
```

et vous ajoutez cette ligne à la fin :

```text
source ~/.oh-my-zsh/custom/themes/powerlevel10k/powerlevel10k.zsh-theme
```

Ensuite vous rechargez Zsh:

```bash
exec zsh
```

puis maximisez la fenêtre de votre terminal et ensuite lançez la configuration de PowerLevel avec :

```bash
p10k configure
```

Toujours dans Xfce Terminal, dans Préférences, sélectionnez la police que vous venez d'installer.

Et pour finnir :

```bash
git clone https://github.com/dracula/powerlevel10k.git
cd powerlevel10k
cp ./files/.zshrc ~/.zshrc
cp ./files/.p10k.zsh ~/.p10k.zsh
```

*Lors de mes tests il est arrivé que la config tmux enlève la config zsh ou inversement. Dans ce cas il suffit de refaire la manip une fois.*

# Rofi

![rofi](images/pi400-rofi.png)

C'est un lanceur modal qui permet, comme dans macOS, de faire apparaitre une fenetre flottante avec un champ de texte pour trouver rapidement une application à lancer ou un fichier à ouvrir, d'un simple rraccourci clavier tel que Meta-Espace.

```bash
sudo apt install rofi
mkdir -p ~/.config/rofi
rofi -dump-config > ~/.config/rofi/config.rasi
git clone https://github.com/dracula/rofi
cp rofi/theme/config1.rasi ~/.config/rofi/config.rasi
```

Allez dans le menu principal du bureau, ouvrez Paramètres > Clavier > Raccourcis d'applications, et ajoutez un raccourci de votre choix (Alt+Espace pour faire comme dans macOS) contenant cette ligne :

```bash
rofi -modi "run,drun,window" -show run
```

# Ruby

Il est conseillé de ne pas utiliser les versions de Ruby packagées dans le système, comme sur macOS, et d'utiliser un gestionnaire de versions à la place. J'ai l'habitude d'utiser Rbenv.

```bash
git clone https://github.com/sstephenson/rbenv.git $HOME/.rbenv
mkdir $HOME/.rbenv/plugins
git clone https://github.com/sstephenson/ruby-build.git $HOME/.rbenv/plugins/ruby-build
```

Ouvrez `~/.zshrc` et ajoutez ces deux lignes :

```bash
export PATH=$HOME/.rbenv/bin:$PATH
eval "$(rbenv init -)"
```

Relancez zsh si besoin. Ensuite vous pouvez installer un Ruby récent et le déclarer comme version globale par défaut :

```bash
rbenv install 3.1.0 --verbose
rbenv global 3.1.0
```

# Tmux

Je me sers principalement de tmux pour diviser le terminal en panneaux, mais c'est également bien pratique pour détacher et attacher des sessions.

```bash
sudo apt install tmux
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

Ouvrez `~/.tmux.conf` et ajoutez ça à la fin :

```text
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'dracula/tmux'
set -g @plugin 'tmux-plugins/tmux-resurrect'
run -b '~/.tmux/plugins/tpm/tpm'
```

Finalement, activez le tout. Lancez tmux, puis sourcez, puis faites prefix+I pour installer les plugins listés :

```bash
tmux
tmux source ~/.tmux.conf
<prefix+I>
```

Faites-vous des réglages comme vous les aimez dans le fichier conf, perso je change pas mal de choses, notamment le préfixe (voir mon exemple à la toute fin de cette page). Et grâce au plugin resurrect, faites TmuxMeta-s pour sauver le contexte avant de quitter, ainsi vous pourrez le recharger avec TmuxMeta-r au prochain lancement.

> Astuce : si vous êtes perdus dans les layers bash/zsh/tmux, faites `exit` autant de fois que nécéssaire pour remonter les niveaux, de l'actuel jusqu'à la fermeture du terminal.

# vim

Si comme moi vous utilisez Vim tout le temps ou presque, je vous conseille quelques réglages et plugins pour vous faciliter son usage sur le Pi.

Installez d'abord vim si necessaire, puis le gestionnaire de plugins.

```bash
sudo apt install vim
vim
<:q>
curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

Installez node (on aura besoin plus tard de toute façon) puis téléchargez le CSS pour Markdown :

```bash
sudo apt install node
npm install github-markdown-css
```

Copiez le fichier `github-markdown.css` dans `~/.vim/` si le script d'install ne l'a pas fait.

Ajoutez ça à la fin de `~/.vimrc` :

```vim
let g:mkdp_refresh_slow=1
let g:mkdp_markdown_css='~/.vim/github-markdown.css'
let g:snipMate = { 'snippet_version' : 1 }

call plug#begin()

Plug 'sheerun/vim-polyglot'
Plug 'preservim/nerdtree'
Plug 'godlygeek/tabular'
Plug 'preservim/vim-markdown'
Plug 'iamcco/markdown-preview.nvim', { 'do': { -> mkdp#util#install() }, 'for': ['markdown', 'vim-plug']}
Plug 'dracula/vim', { 'as': 'dracula' }  
Plug 'MarcWeber/vim-addon-mw-utils'
Plug 'tomtom/tlib_vim'
Plug 'garbas/vim-snipmate'
Plug 'honza/vim-snippets'

call plug#end()
```

Ensuite relancez vim, puis tapez `:PlugInstall` pour commencer l'installation des plugins listés dans le fichier de conf.

```bash
vim
<:PlugInstall>
```

## NerdTree

En mode NORMAL, tapez `:NERDTree` + Enter pour faire apparaître le navigateur de fichiers intégré à Vim.

## SnipMate

En mode NORMAL, faites `:SnipMateOpenSnippetFiles` + Enter, cela va ouvrir la liste des fichiers de snippets disponibles. Sélectionnez-en un et observez la syntaxe pour vous en inspirer, c'est facile.

A l'usage, il suffit de se mettre en mode INSERT, de taper le mot-clé déclencheur puis de taper la raccourci décencheur, par défaut TAB.

## Yank to clipboard

Dans Vim le copier-coller avec la commande `yank` se fait avec les registres de Vim, c'est-à-dire que les tampons mémoire sont internes à Vim, le système ne les voit pas quand on copie en mode VISUAL avec `y`.

Ma solution est de map `Y` sur une commande qui partage le registre copié dans le clipboard du système. Faites `y` pour copier dans Vim ou `Y` pour copier dans le clipboard.

Ajoutez ça dans `~/.vimrc` :

```text
nnoremap Y "+y
vnoremap Y "+y
nnoremap yY ^"+y$
```

# SSH

Il est indispensable de pouvoir se connecter au terminal du Pi à partir d'une autre machine, il nous faut donc ouvrir le serveur ssh.

Changez le nom d'utilisateur si ce n'est déjà fait (il est déconseillé de garder le nom pi par défaut) et activez ssh à partir de l'utilitaire de configuration :

```bash
sudo raspi-config
```

Faites menu 1 pour le user name, puis faites menu 5 (Interfacing Options) pour sélectionner le bouton "Yes" qui va lancer le serveur automatiquement pour toutes les prochaines sessions.

Pour se connecter au pi en ssh à partir d'une autre machine il vous faudra connaître son adresse ip sur le réseau interne. Faites donc `ifconfig` et vous y verrez en principe l'interface "wlan0" qui représente le wifi, et son ip à côté.

Sur la machine distante, si l'utilisateur du Pi est "yolo" est l'ip du pi est "192.168.1.12" :

```bash
ssh yolo@192.168.1.12
```

Tout simplement.

# Accéder à un share

Si vous avez une machine qui partage des fichiers sur votre réseau, il est très facile d'y accéder à partir du Pi avec un gestionnaire de fichiers visuel tel que Thunar, déjà installé par défaut.

Ceci dit, si la machine qui partage les fichiers est un Mac, il faut commencer par aller, sur ce Mac, dans Préférences > Partage > Options, activer Partager via SMB, et ne pas oublier de cocher la case en face de votre user name.

Et pour y accéder en ligne de commande il y a quelques manipulations à faire.

Sur le pi créez un fichier `~/.smbcredentials` qui contient username et mot de passe de la machine qui partage, comme ceci :

```text
username=ed
password=1234
```

Ensuite dans le terminal faites

```bash
mkdir -p ~/mnt/name
sudo vim /etc/fstab
```

avec un nom de votre choix à la place de "name" (en principe on met le nom de la machine qui partage, par exemple "macmini" dans mon cas).

Puis ajoutez cette ligne à la fin :

```text
//machinequipartage/usernamecochédanspartage /home/usernamedupi/mnt/name cifs credentials=/home/usernamedupi/.smbcredentials 0 0
```

Si par exemple la machine qui partage est `macmini.local`, que sur cette machine l'utilisateur "ed" est le partageur de son compte, et que l'utilisateur du Pi est "yolo" et qu'il veut monter le dossier partagé, cette ligne serait :

```text
//macmini.local/ed /home/yolo/mnt/macmini cifs credentials=/home/yolo/.smbcredentials 0 0
```

Ensuite pour monter le partage faites

```bash
sudo mount -a
```

Cette manipulation vous permettra d'accéder au partage en lecture/écriture avec vos droits d'utilisateur sans avoir à passer par root.

# Chromium et Firefox

Normalement Chromium est déjà installé, et c'est franchement le navigateur qui a le meilleur compromis modernité/fiabilité/légèreté/vitesse sur le Pi. Mais je vous conseille également d'installer Firefox, même s'il est bien plus lourd en RAM et CPU, car il est aussi très joli, proposse un meilleur rendu des pages, et offres plus de features comme la synchro des bookmarks par exemple.

```bash
sudo apt install firefox-esm
```

# FileZilla

Un peu antique, mais il propose toutes les fonctionnalités que l'on attend de lui.

```bash
sudo apt install filezilla
```

# VSCode

Malheureusement Sublime Text n'est pas disponible sur le Pi en 32 bits (et n'est pas mature sous 64 bits de toute façon), et je vous déconseille l'utilsation d'IDE lourds tel que Eclipse sur le Pi. Il nous reste une excellente option avec VSCode qui tourne très bien même avec 4 Go de RAM.

```bash
sudo apt install code
git clone https://github.com/dracula/visual-studio-code.git ~/.vscode/extensions/theme-dracula
cd ~/.vscode/extensions/theme-dracula
npm install
npm run build
```

# bpytop

Le meilleur remplacement de luxe pour top, avec en prime le thème Dracula intégré !

```bash
sudo apt install bpytop
```

Une fois bpytop lancé, et passé le choc devant la geekerie de la chose, faites `M` pour ouvrir son menu, puis flèches droite/gauche pour naviguer dans les thèmes. Dracula et Nord sont ceux qui s'accordent le mieu avec notre bureau.

![bpytop](images/crunchingpngs.png)

# dotfiles

Tous les fichiers de configuration qui ont servi à cette installation sont disponibles sur mon compte [GitHub](https://github.com/ericdke/dotfiles-pi4).

Il y a même le fond d'écran tout joli.


