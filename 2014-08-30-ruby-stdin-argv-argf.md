---
title: "Ruby : STDIN, ARGV et ARGF"
date: "2014-08-30"
categories: 
  - "dev"
  - "ruby"
  - "tuto"
---

Quand on débute en Ruby, on peut se demander comment réunir dans un seul script les comportements de base d'une application compatible Unix :

- accepte des paramètres de commande
    
- accepte des données en entrée
    
- accepte des fichiers en paramètres ou en entrée
    

Nous allons voir comment gérer ça de manière simplissime dans un petit script.

Pour une application d'envergure il vaut mieux passer par une Gem dédiée qui va parser les paramètres pour vous, de type Thor, mais pour un script modeste ces solutions sont très rapides et pratiques.

# Paramètres

## Arguments

Ruby fournit la constante `ARGV` qui est un tableau (_array_) contenant les arguments fournis lors de l'appel du script.

- _myscript.rb :_

```ruby
puts ARGV.inspect
```

- _Commande :_

```text
ruby myscript.rb --help 'ma commande'
```

- _Résultat :_

```text
# ["--help", "ma commande"]
```

C'est vraiment la base :

```ruby
if ARGV[0] == '--help'
  puts "Besoin d'aide à propos de '#{ARGV[1]}' ?"
else
  puts "Tout va bien."
end
```

Ca ne va pas bien loin avant d'être totalement fastidieux et labyrinthique, mais ça suffit pour deux ou trois options.

## Arguments ou Fichiers ?

Exemple un tout petit peu plus avancé.

Disons qu'on accepte une option `--file` qui fournit un fichier texte à lire, ou alors pas d'option et on affiche la liste indexée des arguments s'il y en a.

Nous allons utiliser la constante `ARGF` fournie par Ruby, c'est elle qui reçoit les fichiers passés en argument.

Créez un fichier d'exemple si vous le souhaitez :

```text
$ echo "hihiahahohoh" > ahah.txt
```

- _myscript.rb :_

```ruby
if ARGV.empty?
  puts "Rien. Le vide. Le silence."
elsif ARGV[0] == "--file"
  ARGV.shift
  puts "Contenu du fichier:"
  puts ARGF.read
else
  ARGV.each.with_index(1) {|arg, index| puts "Arg #{index}: #{arg}"}
end
```

- _Commande :_

```text
$ ruby myscript.rb
```

- _Résultat :_

```text
# Rien. Le vide. Le silence.
```

- _Commande :_

```text
$ ruby myscript.rb --file ahah.txt
```

- _Résultat :_

```text
# Contenu du fichier:
# hihiahahohoh
```

- _Commande :_

```text
$ ruby myscript.rb ok allo voilà
```

- _Résultat :_

```text
# Arg 1: ok
# Arg 2: allo
# Arg 3: voilà
```

_Note: je n'indiquerai plus la commande de l'interpréteur Ruby, mais vais considérer que vous avez rendu votre script exécutable._

> Ajoutez la ligne `#!/usr/bin/env ruby` au début du script, puis rendez le script exécutable dans votre shell: `chmod u+x myscript.rb`. Plus besoin de lancer le script avec `ruby myscript.rb`, il suffira de faire `./myscript.rb`.

# En entrée

On peut aussi vouloir accepter des données en entrée, comme par exemple avec le pipe du shell.

C'est la constante `STDIN` qui va nous fournir cette possibilité.

- _myscript.rb :_

```ruby
#!/usr/bin/env ruby
puts "Vous avez indiqué:"
puts STDIN.read
```

- _Commande :_

```text
$ echo 'ohlàlà' | ./myscript.rb
```

- _Résultat :_

```text
# Vous avez indiqué:
# ohlàlà
```

- _Commande :_

```text
$ cat ahah.txt | ./myscript.rb
```

- _Résultat :_

```text
# Vous avez indiqué:
# hihiahahohoh
```

Ca marche aussi dans l'autre sens avec le chevron !

- _Commande :_

```text
$ ./myscript.rb < ahah.txt
```

- _Résultat :_

```text
# Vous avez indiqué:
# hihiahahohoh
```

# Ensemble

Et maintenant, voyons un petit ensemble de conditions pour déterminer dans notre script de quelle façon les données ont été reçues.

Nous utilisons les contantes déjà vues plus haut, ainsi que la variable globale `$stdin` qui représente l'état du Terminal.

- _myscript.rb :_

```ruby
#!/usr/bin/env ruby
if $stdin.tty?
  if ARGV.empty?
    puts "Rien. Le vide. Le silence."
  elsif ARGV[0] == '--file' || ARGV[0] == '-F'
    ARGV.shift
    puts "Contenu du fichier:"
    puts ARGF.read
  else
    ARGV.each.with_index(1) {|arg, index| puts "Arg #{index}: #{arg}"}
  end
else
  puts "Vous avez indiqué:"
  puts STDIN.read
end
```

Avec `if $stdin.tty?` nous demandons si nous venons de recevoir des arguments après la commande.

Dans cette condition nous utilisons `ARGV` pour les arguments et `ARGF` pour les fichiers.

Si pas d'arguments fournis, l'autre branche de la condition lit les données en entrée avec `STDIN.read`.

_Tous les exemples de commande vus plus haut, que ce soient les arguments, les fichiers, le pipe ou le chevron, fonctionnent avec ce simple script._

# Conclusion

Cet aperçu des méthodes pour recevoir différentes données dans vos scripts Ruby était volontairement simple, le but était de répondre aux questions les plus fréquentes.

Mais n'oubliez pas d'utiliser une Gem dédiée si vous avez plus de deux ou trois options à traiter, ce sera bien plus puissant et modulable.
