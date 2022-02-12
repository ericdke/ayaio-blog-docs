---
title: "Un mini serveur d'API en Ruby"
date: "2015-05-09"
categories: 
  - "dev"
  - "ruby"
  - "tuto"
---

On a souvent besoin de tester des requêtes Internet quand on développe une application, par exemple pour vérifier dans une app iOS que la connexion se fait bien en arrière-plan, que le JSON reçu est bien décodé, etc.

On serait tenté de s'adresser à son serveur de prod, ou même d'utiliser Dropbox... mais il y a plus cool : se faire son propre mini serveur de tests.

Et avec Ruby, c'est très simple, et ça prend à peine vingt lignes de code.

Let's go!

## Présentation

Ces temps-ci j'ai souvent besoin de tester la validité d'un payload JSON, ou la solidité d'un upload d'image vers le Web, ou la qualité d'une connexion et de son timeout, etc.

Au lieu d'utiliser plusieurs services pour ça, et même de laisser traîner des fichiers dans des dossiers protégés de mon serveur de prod, comme on est souvent tenté de le faire, ou de s'adresser à des outils qui ne sont pas faits pour ça comme Dropbox, il est plus efficace - et même plus simple - de se faire son propre serveur en local.

Avec Ruby et Sinatra ça prend quelques lignes à peine et ça rend un service incroyable.

## Le serveur

On va avoir besoin de Sinatra, donc on l'installe avec ses dépendances :

```bash
gem install sinatra thin webrick
```

On crée ensuite un simple fichier Ruby `app.rb` avec cet en-tête :

```ruby
#!/usr/bin/env ruby
# encoding: utf-8

require "sinatra"
require "json"
```

On peut obtenir une version fonctionnelle pour tester l'install avec juste trois lignes à ajouter :

```ruby
get '/' do
    "Hello World"
end
```

Ca veut dire que Sinatra va surveiller l'URL racine, dans notre cas localhost sur le port 4567, et répondre par le contenu de `do ... end`.

On le lance puis on teste :

```bash
ruby app.rb
curl localhost:4567
```

Résultat : "Hello World" s'affiche dans le terminal.

_Stoppez le serveur en faisant CTRL+C._

On vient de voir que créer un serveur minimal était simplissime. On va maintenant créer des routes et fonctions plus utiles.

### JSON

Par exemple, on veut une URL "localhost:4567/api" qui retourne du JSON.

On crée donc une route pour l'URL :

```ruby
get '/api' do
end
```

et dans cette methode on va créer le contenu qui sera retourné.

Comme on veut du JSON, on va faire un hash (un dictionnaire) et le convertir en JSON.

```ruby
get '/api' do
    # On précise le format pour Sinatra
    content_type :json
    # On créer un hash avec nos contenus
    jj = {
        'meta' => {
            'code' => 200,
            'message' => 'Welcome to MiniServer API.'
        }
    }
    # On transforme le hash en joli JSON
    # Comme on est en Ruby, la dernière déclaration est retournée, donc par convention on n'indique pas explicitement `return`
    JSON.pretty_generate(jj)
end
```

Résultat :

```bash
ruby app.rb
curl localhost:4567/api
```

```json
{
  "meta": {
    "code": 200,
    "message": "Welcome to MiniServer API."
  }
}
```

### Fichier JSON

Et si on veut que notre serveur retourne du JSON plus complexe ? On peut lui demander, au lieu de créer un hash et de le convertir, de lire un fichier JSON existant.

Dans notre exemple très simple sans configuration, le fichier devra être présent au même niveau que `app.rb`.

```ruby
get '/file/*.*' do
    # `params` est le nom de la variable globale de Sinatra qui contient les paramètres passés dans l'URL, et `splat` représente un format contenant `*`
    name = params["splat"].join(".")
    File.read(name)
end
```

Disons que j'aie un fichier `test.json`, je fais :

```bash
curl localhost:4567/file/test.json
```

et j'obtiens le JSON.

Sinatra autorise à forcer une URL sous forme de nom de fichier avec les deux astérisques et le point, qui retourne un array qu'il faut donc rejoindre avec un point.

On lit ensuite le contenu du fichier, qui est automatiquement retourné.

Donc par exemple au lieu de taper sans cesse une vraie API en ligne qui distribue du JSON, vous pouvez enregistrer le résultat d'une requête puis la rejouer autant que vous voulez dans votre propre mini serveur :

```bash
curl www.big-api.com/api/bigdatachunk > test.json
ruby app.rb
curl localhost:4567/file/test.json
```

### Fichier à downloader

Ici j'utilise une image en exemple. Sinatra permet de faire ça très simplement grâce à un de ses helpers :

```ruby
get '/picture' do
    send_file '/Users/you/Images/bird.jpg'
end
```

Collez `http://localhost:4567/picture` dans un browser, et votre image s'affiche.

### Détails d'une requête

On peut vouloir inspecter l'URL formée à partir de paramètres, on va donc partir de notre précédente méthode associée à l'URL `/api` et lui ajouter ces fonctions :

```ruby
get '/api/*' do
    jj = {
        'meta' => {
            'code' => 200,
            'message' => 'Welcome to MiniServer. Request accepted.'
        }
    }
    if params['splat'].first != ""
        jj['data'] = {}
        jj['data']['components'] = params['splat'].first.split('/')
        if !params["q"].nil?
            jj['data']['query'] = params["q"]
        end
    end
    content_type :json
    JSON.pretty_generate(jj)
end
```

Ce n'est qu'un exemple pour démontrer le principe.

Requête :

```bash
curl localhost:4567/api/test/server/whatever/\?q=yo
```

Résultat :

```json
{
  "meta": {
    "code": 200,
    "message": "Welcome to MiniServer. Request accepted."
  },
  "data": {
    "components": [
      "test",
      "server",
      "whatever"
    ],
    "query": "yo"
  }
}
```

### 404

Il faut bien se préparer aussi un petit 404, encore une fois Sinatra nous aide avec un helper pour, cette-fois, la route :

```ruby
not_found do
    {
        'meta' => {
            'code' => 404,
            'message' => 'Welcome to MiniServer. Request not found.'
        }
    }.to_json
end
```

_Ici j'ai volontairement choisi de retourner du JSON brut, non pretty-print, pour montrer que c'est encore plus simple à faire._

### Upload

Bien sûr, on peut aussi tester autre chose que `GET`. Par exemple, pour l'upload d'un fichier :

```ruby
post '/upload' do
    jj = {
        'meta' => {
            'code' => 200,
            'message' => 'Welcome to MiniServer API. File received.'
        }, 
        'data' => {
            'env' => request.env
        }
    }
    content_type :json
    JSON.pretty_generate(jj)
end
```

On fait par exemple avec notre précédent fichier de test (mais ça pourrait être une image ou tout autre fichier) :

```bash
curl -X POST -d @"test.json" localhost:4567/upload
```

Résultat :

```json
{
  "meta": {
    "code": 200,
    "message": "Welcome to MiniServer API. File received."
  },
  "data": {
    "env": {
      "SERVER_SOFTWARE": "thin 1.6.3 codename Protein Powder",
      "SERVER_NAME": "localhost",
      "rack.input": "#<StringIO:0x007ff1e298b2b0>",
      "rack.version": [
        1,
        0
      ],
      "rack.errors": "#<IO:0x007ff1e20ca4f0>",
      "rack.multithread": true,
      "rack.multiprocess": false,
      "rack.run_once": false,
      "REQUEST_METHOD": "POST",
      "REQUEST_PATH": "/upload",
      "PATH_INFO": "/upload",
      "REQUEST_URI": "/upload",
      "HTTP_VERSION": "HTTP/1.1",
      "HTTP_USER_AGENT": "curl/7.35.0",
      "HTTP_HOST": "localhost:4567",
      "HTTP_ACCEPT": "*/*",
      "CONTENT_LENGTH": "49",
      "CONTENT_TYPE": "application/x-www-form-urlencoded",
      "GATEWAY_INTERFACE": "CGI/1.2",
      "SERVER_PORT": "4567",
      "QUERY_STRING": "",
      "SERVER_PROTOCOL": "HTTP/1.1",
      "rack.url_scheme": "http",
      "SCRIPT_NAME": "",
      "REMOTE_ADDR": "127.0.0.1",
      "async.callback": "#<Method: Thin::Connection#post_process>",
      "async.close": "#<EventMachine::DefaultDeferrable:0x007ff1e21e3558>",
      "rack.request.form_input": "#<StringIO:0x007ff1e298b2b0>",
      "rack.request.form_hash": {
        "{\"meta\":{\"code\":200,\"message\":\"Test from file.\"}}": null
      },
      "rack.request.form_vars": "{\"meta\":{\"code\":200,\"message\":\"Test from file.\"}}",
      "sinatra.commonlogger": true,
      "rack.logger": "#<Logger:0x007ff1e2872680>",
      "rack.request.query_string": "",
      "rack.request.query_hash": {
      },
      "sinatra.route": "POST /upload"
    }
  }
}
```

Yeah, c'est plutôt complet ce que nous donne Sinatra comme infos, pas mal du tout !

## Exemple complet

```ruby
#!/usr/bin/env ruby
# encoding: utf-8

require "sinatra"
require "json"

# C'est pratique aussi d'avoir un log
configure do
  file = File.new("#{Dir.home}/temp/server.log", 'a+')
  file.sync = true
  use Rack::CommonLogger, file
end

# On peut choisir une liste de serveurs compatibles, choisir le port, et choisir le dossier racine
set :server, %w[thin webrick]
set :port, 4567
set :root, File.dirname(__FILE__)

# Routes

get '/' do
    "yo"
end

get '/api' do
    content_type :json
    jj = {
        'meta' => {
            'code' => 200,
            'message' => 'Welcome to MiniServer API.'
        }
    }
    JSON.pretty_generate(jj)
end

get '/file/*.*' do
    name = params["splat"].join(".")
    File.read(name)
end

get '/api/*' do
    jj = {
        'meta' => {
            'code' => 200,
            'message' => 'Welcome to MiniServer. Request accepted.'
        }
    }
    if params['splat'].first != ""
        jj['data'] = {}
        jj['data']['components'] = params['splat'].first.split('/')
        if !params["q"].nil?
            jj['data']['query'] = params["q"]
        end
    end
    content_type :json
    JSON.pretty_generate(jj)
end

get '/picture' do
    send_file '/Users/me/images/bird.jpg'
end

post '/upload' do
    jj = {
        'meta' => {
            'code' => 200,
            'message' => 'Welcome to MiniServer API. File received.'
        }, 
        'data' => {
            'env' => request.env
        }
    }
    content_type :json
    JSON.pretty_generate(jj)
end

not_found do
    jj = {
        'meta' => {
            'code' => 404,
            'message' => 'Welcome to MiniServer. Request not found.'
        }
    }
    content_type :json
    JSON.pretty_generate(jj)
end
```
