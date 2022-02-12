---
title: "Hackathon C++ dans Haiku"
date: "2020-11-29"
categories: 
  - "c"
  - "dev"
  - "haiku"
  - "linux"
  - "os"
---

Juste pour le fun j'ai voulu porter un exercice en C++ sur [Haiku](https://www.haiku-os.org), le système d'exploitation alternatif qui imite l'aspect de [BeOS](https://fr.wikipedia.org/wiki/BeOS) et en reprend les API système, mais dont le coeur est basé sur Linux.

Pas de rédactionnel détaillé malheureusement, car je n'avais pas prévu d'en faire un article de blog au début, mais je vous montre un peu quand même.

Je n'ai pas eu trop de surprises quant à l'installation de Haiku dans VirtualBox d'abord, puis VMWare Fusion Core (bien plus rapide et tout aussi gratuit).

Haiku est un super OS très léger, fluide, agréable à utiliser, mais encore très limité en applications disponibles. Tout démarre instananément, le système lui-même comme les apps, le build de notre app est immédiat, l'UI est hyper réactive, etc. Dans une VM avec juste 1GB de RAM et un seul core processeur dédié. Joli !

J'ai utilisé Paladin, un des éditeurs de code disponibles dans la distribution. Minimaliste, c'esr le moins qu'on puisse dire. Mais ça édite et ça build, donc on s'en sort pas si mal. Sinon y'avait Vim pas loin...

La difficulté principale a été que je n'ai pas réussi à installer les bibliothèques `boost` ni même à simplement compiler `libcurl` pour Haiku, donc pour la partie REST-client j'ai fini par faire des appels à `curl` comme un goret, mais bon, allez, je me pardonne.

Au final un beau moment de nostalgie - ah la la c'était vraiment bien BeOS, et Haiku reprend le flambeau avec moultes promesses - et une belle aventure au pays des systèmes alternatifs.

> Config PLD pour Paladin:

```txt
NAME=WeatherManHaiku
TARGETNAME=WeatherManHaiku
PLATFORM=HaikuGCC4
SCM=git
GROUP=Source files
EXPANDGROUP=yes
SOURCEFILE=CURLDownloader.cpp
SOURCEFILE=CURLDownloader.hpp
SOURCEFILE=URLResult.hpp
SOURCEFILE=Utils.cpp
SOURCEFILE=Utils.hpp
SOURCEFILE=Weather.cpp
SOURCEFILE=Weather.hpp
SOURCEFILE=main.cpp
LOCALINCLUDE=.
SYSTEMINCLUDE=B_FIND_PATH_DEVELOP_HEADERS_DIRECTORY/be
SYSTEMINCLUDE=B_FIND_PATH_DEVELOP_HEADERS_DIRECTORY/cpp
SYSTEMINCLUDE=B_FIND_PATH_DEVELOP_HEADERS_DIRECTORY/posix
LIBRARY=B_FIND_PATH_DEVELOP_LIB_DIRECTORY/libbe.so
RUNARGS=
CCDEBUG=no
CCPROFILE=no
CCOPSIZE=no
CCOPLEVEL=0
CCTARGETTYPE=0
CCEXTRA=
LDEXTRA=
```

> main.cpp

```cpp
#include "URLResult.hpp"
#include "CURLDownloader.hpp"
#include "Utils.hpp"
#include "Weather.hpp"

int main(int argc, const char * argv[])
{
    CURLDownloader dl;
    URLResult result = dl.makeURL(argc, argv);  
    if (result.success) {
        clear_screen();
        print("Downloading data...");
        std::string json_string = dl.download(result.url);
        Weather w = dl.parse(json_string);
        clear_screen();
        print(w.description());
        exit(0);
    } else {
        print("\nOops, that didn't work out very well...");  
        exit(1);
    }
}
```

> Weather.hpp

```cpp
#ifndef Weather_hpp
#define Weather_hpp

#include <iostream>
#include <cmath>
#include <vector>
#include <ctime>
#include <iomanip>
#include "Utils.hpp"

struct DateTime {
    std::string date;
    std::string time;
};

class Weather {
public:
    float temp;
    std::string city;
    std::string country;
    std::string category;
    std::string sub_category;
    float wind_speed;
    float wind_direction;
    float wind_speed_kmh();
    std::string wind_direction_compass();
    std::string description();
private:
    DateTime date_formatted();
};

#endif /* Weather_hpp */
```

> Weather.cpp

```cpp
#include "Weather.hpp"

float Weather::wind_speed_kmh()
{
    return floor(((wind_speed * 3.6) * 5 + 0.5) / 5);
}

std::string Weather::wind_direction_compass()
{
    std::vector<std::string> compass = {"Nord","Nord Nord-Est","Nord-Est","Est-Nord-Est","Est","Est-Sud-Est","Sud-Est","Sud-Sud-Est","Sud","Sud-Sud-Ouest","Sud-Ouest","Ouest-Sud-Ouest","Ouest","Ouest-Nord-Ouest","Nord-Ouest","Nord-Nord-Ouest"};
    float wd = (wind_direction / 22.5) + 0.5;
    // % (modulo operator) is not available for floats, use fmod
    int index = fmod(wd, 16);
    return compass[index];
}

std::string Weather::description()
{
    // DateTime is a struct defined in the header
    DateTime dt = date_formatted();
    std::string dts = dt.date + ", " + dt.time;
    std::string cel = float_to_string(temp, 1);
    std::string ci = city + " (" + country + "), le " + dts + ".\n";
    std::string te = "Température: " + cel + "°C.\n";
    std::string ca = ci + te + "Temps: " + category + ".\n";
    // TODO: check if wind exists in API response before using it
    std::string w = float_to_string(wind_speed_kmh(), 1);
    std::string desc = ca + "Vent: " + wind_direction_compass() + " à " + w + " km/h.\n";
    return desc;
}

DateTime Weather::date_formatted()
{
    time_t temps;
    struct tm datetime;
    char format_date[32];
    char format_temps[32];
    time(&temps);
    datetime = *localtime(&temps);
    strftime(format_date, 32, "%d/%m/%Y", &datetime);
    strftime(format_temps, 32, "%Hh%M", &datetime);
    DateTime dt;
    dt.date = (std::string) format_date;
    dt.time = (std::string) format_temps;
    return dt;
}
```

> Utils.hpp

```cpp
#ifndef Utils_hpp
#define Utils_hpp

#include <iostream>
#include <iomanip>
#include <cstdio>
#include <stdexcept>
#include <string>
#include <array>

void clear_screen();
std::string exec(const char* cmd);
std::string float_to_string(float const& f, int const& p);
void print(std::string const& s);

#endif /* Utils_hpp */
```

> Utils.cpp

```cpp
#include "Utils.hpp"

void clear_screen()
{
    std::string cs = "clear";
    const char *p = cs.c_str();
    auto clear = exec(p);
    print(clear);
}

std::string float_to_string(float const& f, int const& p)
{
    std::stringstream stream;
    stream << std::fixed << std::setprecision(p) << f;
    return stream.str();
}

void print(std::string const& s)
{
    std::cout << s << std::endl;
}

std::string exec(const char* cmd) {
    std::array<char, 128> buffer;
    std::string result;
    std::unique_ptr<FILE, decltype(&pclose)> pipe(popen(cmd, "r"), pclose);
    if (!pipe) {
        throw std::runtime_error("popen() failed!");
    }
    while (fgets(buffer.data(), buffer.size(), pipe.get()) != nullptr) {
        result += buffer.data();
    }
    return result;
}
```

> URLResult.hpp

```cpp
#ifndef URLResult_hpp
#define URLResult_hpp

#include <string>

struct URLResult {
    URLResult(bool s, std::string r) : success(s), url(r) {};
    bool success;
    std::string url;
};

#endif /* URLResult_hpp */
```

> CURLDownloader.hpp

```cpp
#ifndef CURLDOWNLOADER_HPP
#define CURLDOWNLOADER_HPP

#include "URLResult.hpp"
#include "Utils.hpp"
#include "Weather.hpp"
#include "rapidjson/document.h"

class CURLDownloader {
public:
    Weather parse(const std::string& json_string);
    std::string download(const std::string& url);
    URLResult makeURL(int argc, const char * argv[]);
};

#endif  /* CURLDOWNLOADER_HPP */
```

> CURLDownloader.cpp

```cpp
#include "CURLDownloader.hpp"

using namespace rapidjson;

Weather CURLDownloader::parse(const std::string& json_string)
{
        Document document;
        const char *json_chars = json_string.c_str();
        document.Parse(json_chars);
        auto main = document["main"].GetObject();
        auto temp = main["temp"].GetFloat();
        auto city = document["name"].GetString();
        auto sys = document["sys"].GetObject();
        auto country = sys["country"].GetString();
        auto wind = document["wind"].GetObject();
        auto wind_speed = wind["speed"].GetFloat();
        auto wind_direction = wind["deg"].GetFloat();
        auto it = document["weather"].GetArray();
        auto first = it[0].GetObject();
        auto cat = first["description"].GetString();
        Weather w;
        w.temp = temp;
        w.city = city;
        w.country = country;
        w.wind_speed = wind_speed;
        w.wind_direction = wind_direction;
        w.category = cat;
        return w;
}

URLResult CURLDownloader::makeURL(int argc, const char * argv[])
{
    if(argc > 1)
    {
        // make a single string from all CLI input
        std::string input;
        for(int i = 1; i < argc; i++) {
            input += argv[i];
        }

        std::string url = "http://api.openweathermap.org/data/2.5/weather?q="
        + input
        + "&appid=d21991d7851f849bfe8cc24d12c795d0&units=metric&lang=fr";

        return URLResult(true, url);
    }
    return URLResult(false, "");
}

std::string CURLDownloader::download(const std::string &url)
{
    std::string result;
    std::string cmd = "curl -s \"" + url + "\"";
    const char *cstr = cmd.c_str();
    result = exec(cstr);
    return result;
}
```

## Instructions

Si Paladin est bien paramétré vous cliquez simplement sur `build`.

Sinon, `cd` dans le dossier qui contient les fichiers, puis `g++` tout le monde.

Il se peut que vous ayez à installer des bibliothèques manquantes à partir du gestionnaire de paquets.
