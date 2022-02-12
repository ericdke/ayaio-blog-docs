Peut-on remplacer son Mac par un Raspberry Pi au quotidien ? Oui ! Enfin, presque.

Ca ne marchera pas pour le développement iOS pour des raisons évidentes, mais pour tout le reste, ça le fait carrément bien... avec pas mal d'huile de coude.

Je raconte comment j'ai installé puis configuré, aux petits oignons, une station Raspberry Pi 400 ou Pi 4 avec Raspberry OS.

<!-- more -->

# Installer la distribution

Il faut installer Raspberry Pi OS sur une carte dédiée. Je conseille 16Go minimum. 32 seront confortables, et 64 est idéal si vous comptez manipuler des gros fichiers. L'essentiel est que la carte soit rapide, classe 10 et bon fabriquant sont indispensables.

Le plus simple est d'utiliser l'app Raspberry Imager. 

Dans l'app, sélectionnez la version de votre choix (32 ou 64 bits) mais surtout faites bien attention à choisir Raspberry OS (et non pas Ubuntu par exemple, qui est complètement buggée pour Pi).

La version 64 bits est 20% plus rapide, mais occupe deux fois plus de place et mange plus de RAM. Perso j'ai pris la version 32 bits, largement assez véloce sur le Pi 400 de toute façon.

Une fois l'image copiée sur la carte vous pouvez l'insérer dans le Pi puis démarrer. 

Ensuite suivez les instructions pour la configuration de base - WIFI, timezone, langage, username, password, etc.

Arrive un moment où le bureau sera chargé. C'est le gestionnaire LXDE avec le bureau PIXEL spécialement conçu pour les Pi. Sympa, mais très limité. Nous allons le remplacer par Xfce 4, tout aussi léger mais bien plus moderne est arrangeant, surtout avec 4 Go de RAM.

# Installation Xfce

Pour un Pi, c'est l'environnement de bureau idéal. Bien sûr vous pourriez installer un KDE ultramoderne, ça passe avec 8 Go de RAM, mais je trouve que ça fait un peu contresens sur un Pi. On pourrait aussi de l'autre côté choisir un environnement minimaliste, ce qui est parfaitement valable - mais aujourd'hui nous allons suivre la voie du milieu.

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


# Réglages Xfce

Si Xfce vous propose un "panel" par défaut dites oui, même si on va l'enlever plus tard.

Maintenant, les essentiels. 

Beaucoup de geeks vous diraient, avec raison, qu'il faut un bon terminal pour pouvoir administrer Linux correctement, et vous proposeraient des terminaux modernes de type Alacritty, Kitty, Terminator, etc. Alors certes ils sont très bien, mais ils sont également complexes à paramétrer et ne me sont pas spécifiquement utiles - je trouve que le terminal Xfce4 est largement suffisant pour mes usages.

Dans ce terminal en revanche, on ne pas utiliser Bash au quotidien, mais Zsh. On va le gérer avec l'utilitaire "Oh my Zsh" :

```bash
sudo apt install zsh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Ces commandes vont installer Zsh puis Oh My Zsh. Suivez ensuite le tuto proposé par OMZ pour faire vos réglages de base.

Ensuite on ajoute PowerLevel10k qui permet de confectionner une superbe ligne de commande. Il faut d'abord [télécharger les fonts Meslo](https://github.com/romkatv/powerlevel10k#meslo-nerd-font-patched-for-powerlevel10k) qui sont idéales pour ça. Téléchargez les fichiers TTF puis activez-les.

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

puis vous lançez la configuration de PowerLevel avec :

```bash
p10k configure
```
