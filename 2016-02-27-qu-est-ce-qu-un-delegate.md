---
title: "Qu'est-ce qu'un \"delegate\" ?"
date: "2016-02-27"
categories: 
  - "dev"
  - "swift"
  - "tuto"
---

Qu'est-ce qu'un "delegate" ?

On retrouve le principe de la délégation partout dans OS X et iOS.

Un champ de texte, par exemple, prévient son potentiel délégué que l'utilisateur est en train de taper du texte, a fini de taper, etc.

Ceci dit, est-il utile d'implémenter nous-même la délégation dans nos objets ? Et comment fait-on ?

On va s'amuser à explorer quelques exemples, purement en Swift, rapidement, dans un simple Playground.

# Principe

La délégation nécéssite : un protocole, un délégateur, un délégué.

## Protocole

Deux objets vont pouvoir communiquer grâce à un protocole.

Ce protocole définit quelles sont les méthodes et propriétés qui seront utilisables par les objets qui se conformeront au protocole.

On peut dire que dans ce contexte, un protocole est comme un contrat entre deux parties, définissante les rôles et responsabilités de ceux qui le signent.

## Délégateur

Le délégateur est l'objet qui _contient une variable_ souvent nommée par convention "delegate".

Cette variable est du type du protocole - mais optionnel, car le délégateur peut très bien ne pas avoir de délégué à un moment donné.

Le délégateur dépend donc d'une instance de l'objet qui servira de délégué.

## Délégué

Le délégué est l'objet qui se _conforme au protocole_.

Le délégué est donc celui qui doit implémenter les méthodes/propriétés exigées par le protocole.

# Du concret

Nous allons utiliser deux exemples.

D'abord, une très simple illustration du principe, qui va donner une idée générale.

Ensuite, une implémentation beaucoup plus intéressante mais forcément un peu moins lisible au premier abord.

# Exemple 1

Disons qu'on a un objet génère régulièrement des évènements, dans notre exemple une simple classe qui créé des numéros de code.

Pour respecter le principe de responsabilité unique, cette classe ne fait que générer les codes, elle ne les affiche pas.

A la place, elle _délègue_ la tâche d'afficher le résultat à d'autres objets - à condition que ces objets soient conformes au protocole exigé par le générateur.

## Le protocole

On va faire simple, le protocole exigera uniquement d'implémenter une méthode `anEventHappened(code: Int)` ("quelque chose est arrivé"), que le délégué pourra invoquer une fois son travail achevé :

```swift
protocol ListensToEvents {

    func anEventHappened(code: Int)

}
```

Comme c'est un protocole, il n'y a pas d'implémentation, seulement une déclaration.

L'implémentation est de la responsabilité de l'objet qui se conforme au protocole.

Le protocole est nommé `ListensToEvents` car il est utilisé par des objets qui écoutent des messages/événements.

Par convention, on nomme un protocole en restant dans le champ lexical de la responsabilité : "SomethingCompatible", "SomethingConvertible", etc, ou de l'activité : "IsAbleToDispatch", "ManagesRemovableStuff", etc.

## Le délégué

Le but étant de découpler la génération des codes de l'affichage des codes, notre délégué sera donc ici une "imprimante".

Le générateur génère, et dit à son délégué : "j'ai généré, tu peux afficher", et le délégué affiche - ou pas.

Par exemple :

```swift
class ClassicPrinter: ListensToEvents {

    func anEventHappened(code: Int) {
        print("CODE: \(code)")
    }

}
```

Notre imprimante, la classe `ClassicPrinter`, se conforme au protocole et l'implémente. Elle affiche simplement le code.

Autre exemple :

```swift
class FancyPrinter: ListensToEvents {

    func anEventHappened(code: Int) {
        print("\(NSDate()) - GENERATED CODE: \(code)")
    }

}
```

Cet autre objet, qui se conforme aussi au même protocole, implémente donc la même méthode, mais différemment - elle affiche aussi la date.

Ces deux objets vont servir de délégué chacun leur tour dans notre démo.

## Le délégateur

Une petite classe qui génère des codes et qui prévient le délégué à chaque code généré.

```swift
class EventsGenerator {

    var delegate: ListensToEvents?

    var codes = [Int]()

    func generateNewCode() {
        codes.append(Int(arc4random_uniform(1_000_000)))

        if let printer = delegate {
            printer.anEventHappened(codes.last!)
        } else {
            // No delegate, the code stays secret...
        }
    }

}
```

Le délégateur contient une variable du type du protocole, c'est cette variable qui sert de référence vers le/les délégué(s).

## Let's go

On colle tout ça dans un Playground :

```swift
protocol ListensToEvents {
    func anEventHappened(code: Int)
}

class ClassicPrinter: ListensToEvents {
    func anEventHappened(code: Int) {
        print("CODE: \(code)")
    }
}

class FancyPrinter: ListensToEvents {
    func anEventHappened(code: Int) {
        print("\(NSDate()) - GENERATED CODE: \(code)")
    }
}

class EventsGenerator {
    var delegate: ListensToEvents?

    var codes = [Int]()

    func generateNewCode() {
        codes.append(Int(arc4random_uniform(1_000_000)))
        if let printer = delegate {
            printer.anEventHappened(codes.last!)
        } else {
            // No delegate, the code stays secret...
        }
    }
}
```

Et pour faire fonctionner le tout, nous créons un générateur :

```swift
let generator = EventsGenerator()
```

Maintenant, que se passe-t-il si l'on invoque la génération d'un code ?

```swift
generator.generateNewCode()
```

On ne voit rien dans la console. Pourtant, nous savons que le code a été généré. Mais le générateur n'a pas encore d'imprimante déléguée, donc rien n'est imprimé.

Maintenant, offrons un délégué à notre générateur, et invoquons à nouveau la création d'un code :

```swift
generator.delegate = ClassicPrinter()
generator.generateNewCode()
```

Cette-fois ci nous voyons s'afficher :

> CODE: 423312

Le générateur a effectué le même travail, mais cette-fois ci son délégué à répondu son appel.

Donnons-lui maintenant un nouveau délégué :

```swift
generator.delegate = FancyPrinter()
generator.generateNewCode()
```

S'affiche donc logiquement :

> 2016-02-27 16:18:54 +0000 - GENERATED CODE: 782392

car l'imprimante a changé.

Et si on enlève le délégué ?

```swift
generator.delegate = nil
generator.generateNewCode()
```

Plus rien ne s'affiche, car le générateur n'a plus d'imprimante déléguée.

Mais nous pouvons vérifier que les quatre invocations du générateur ont bien produit quatre codes :

```swift
print(generator.codes)
```

> \[881982, 423312, 782392, 786518\]

Le premier était invisible, le deuxième était imprimé par ClassicPrinter, le troisième par FancyPrinter, et le quatrième de nouveau invisible.

**En utilisant la délégation, nous avons séparé les responsabilités entre les objets**, qui peuvent donc effectuer leur travail sans être dépendants les uns des autres - ce que l'on recherche en permanence avec la programmation "orientée objet".

_Le code du Playground pour cet exemple est [disponible dans ce Gist](https://gist.github.com/ericdke/aa1ce0a3d38bed3291e3)._

# Exemple 2

Un usage courant pour la délégation est le passage de message, souvent lorsqu'une tâche vient d'être accomplie.

Dans cette partie du tuto nous allons créer une double délégation : un canal de communication restreint entre objets en passant par deux protocoles, un pour délégateur->délégué et un pour délégué->délégateur.

On va raconter la petite histoire d'un chef de chantier qui va faire lancer deux équipes sur une maison.

Dans tous les cas, le chef donnera ses ordres et les équipes concernées effectueront le travail, mais tout ce qui est communication entre le chef et les équipes va se faire via délégation.

## Protocoles

Un protocole qui devra être adopté par les équipes et qui sera utilisé par le chef via sa variable _delegate_ :

```swift
protocol CanBuildHouses {

    func startWorking()

}
```

et celui qui sera adopté par le chef et sera utilisé par les équipes via leur variable _delegate_ :

```swift
protocol CanManageTeams {

    func aTeamHasStartedWorking(team: Team)

    func aTeamHasFinishedWorking(team: Team)

}
```

## Le délégateur

Le boss va avoir une méthode `giveOrder` qui demandera aux délégués d'invoquer leur propre méthode `startWorking`.

Dans `giveOrder` le boss va d'abord vérifier qu'une équipe est disponible en vérifiant que la variable `delegate` ne soit pas `nil`.

Comme cette variable représente une équipe employée par le boss, on va d'ailleurs la nommer `employee` ("employé").

Et pour pouvoir recevoir les communications d'une équipe, le boss doit implémenter les deux méthodes du protocole auquel il se conforme.

En fonction du message reçu, le boss félicitera ou pas l'équipe.

Voici le boss en entier :

```swift
class Contractor: CanManageTeams {

    var name: String

    init(name: String) {
        self.name = name
    }

    var employee: CanBuildHouses?

    func giveOrders() {
        guard let currentTeam = self.employee else {
            print("\(name): No new team in sight.\n")
            return
        }

        print("\(name): Ah! Let's give some work to this team...\n")

        currentTeam.startWorking()
    }

    func aTeamHasStartedWorking(team: Team) {
        print("\(name): Ok \(team.name), see you later today!\n")
    }

    func aTeamHasFinishedWorking(team: Team) {
        if team.taskDuration < 7 {
            print("\(name): Congratulations, \(team.name), work done in \(team.taskDuration) seconds.\n")
        } else {
            print("\(name): Really, \(team.name)? You can do better than \(team.taskDuration) seconds.\n")
        }

    }   
}
```

## Le délégué

Notre équipe sera capable de commencer à travailler selon les ordres du boss en adoptant et en se conformant au protocole `CanBuildHouses` qui exige une méthode `startWorking`.

L'équipe utilise également une variable `delegate` qui est un optionnel `CanManageTeams` et permettra de communiquer avec le chef qui aura adopté ce protocole.

Comme cette variable ne sert qu'à ça, nous la nommerons en fait `reportsTo` ("reporte à").

Et un simple nombre généré au hasard servira pour créer une période de "travail" pour l'équipe.

La classe équipe :

```swift
class Team: CanBuildHouses {

    var name: String

    var reportsTo: CanManageTeams?

    var taskDuration:UInt32 = 0

    init(name: String) {
        self.name = name
    }

    func startWorking() {
        if let announce = reportsTo {
            print("\(name): We're going to start in an instant, let's tell the boss...\n")
            announce.aTeamHasStartedWorking(self)
        } else {
            print("\(name): No boss in sight, let's just start working.\n")
        }
        dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0)) {
            self.taskDuration = arc4random_uniform(10)+2
            sleep(self.taskDuration) // "working" for some time
            dispatch_async(dispatch_get_main_queue()) {
                if let announce = self.reportsTo {
                    print("\(self.name): We're finished, let's tell the boss!\n")
                    announce.aTeamHasFinishedWorking(self)
                } else {
                    print("\(self.name): We're finished! No boss in sight, let's just have a beer.\n")
                }

            }
        }
    }

}
```

## Let's go

On colle tout ça dans un Playground, et on crée nos objets, un employeur et deux équipes :

```swift
let boss = Contractor(name: "BOSS")
let teamJohn = Team(name: "JOHN")
let teamJane = Team(name: "JANE")
```

Pour permetter aux équipes de communiquer avec le boss, on le leur attribue comme délégué :

```swift
teamJohn.reportsTo = boss
teamJane.reportsTo = boss
```

Bon, pour le moment le boss, lui, n'a pas encore de délégué(s).

Que se passe-t-il s'il demande à un délégué de travailler ?

```swift
boss.giveOrders()
```

Rien. Car sa variable `employee` est `nil`. Notre boss va alors s'exclamer qu'aucune équipe n'est en vue.

> No new team in sight.

Créons maintenant une séquence qui va mettre en valeur le rôle de la délégation.

Nous allons attribuer une équipe au boss puis lancer le travail, puis recommencer avec l'autre équipe - et pour finir nous allons enlever le délégué du boss et demander quand même de lancer le travail.

```swift
boss.employee = teamJane
boss.giveOrders()

boss.employee = teamJohn
boss.giveOrders()

boss.employee = nil
boss.giveOrders()
```

Et voici la séquence qui va se dérouler dans la console :

> BOSS: Ah! Let's give some work to this team...
> 
> JANE: We're going to start in an instant, let's tell the boss...
> 
> BOSS: Ok JANE, see you later today!
> 
> BOSS: Ah! Let's give some work to this team...
> 
> JOHN: We're going to start in an instant, let's tell the boss...
> 
> BOSS: Ok JOHN, see you later today!
> 
> BOSS: No new team in sight.
> 
> JANE: We're finished, let's tell the boss!
> 
> BOSS: Congratulations, JANE, work done in 2 seconds.
> 
> JOHN: We're finished, let's tell the boss!
> 
> BOSS: Really, JOHN? You can do better than 7 seconds.

Maintenant, pour vraiment finir de tout comprendre, amusez-vous dans le Playground à varier les séquences : un seul employé pour le boss, deux équipes mais une seule a un boss délégué, etc. Genre :

```swift
teamJohn.reportsTo = boss
// teamJane.reportsTo = boss

boss.employee = teamJane
boss.giveOrders()

boss.employee = teamJohn
boss.giveOrders()

boss.employee = nil
boss.giveOrders()
```

ou

```swift
teamJohn.reportsTo = boss
teamJane.reportsTo = boss

boss.employee = teamJane
boss.giveOrders()

// boss.employee = teamJohn
boss.giveOrders()

boss.employee = nil
boss.giveOrders()
```

etc.

Et comme nous utilisons GCD, n'oubliez pas d'inclure ceci en haut du Playground :

```swift
import XCPlayground
XCPlaygroundPage.currentPage.needsIndefiniteExecution = true
```

pour autoriser l'exécution des background threads.

_Le code du Playground pour cet exemple est [disponible dans ce Gist](https://gist.github.com/ericdke/d8dfa7f01f1a52feaa7c)._

# Conclusion

Tout ce qui peut être fait par délégation peut aussi être effectué différemment.

La délégation n'est qu'un paradigme parmi d'autres - mais il a l'avantage d'offrir des avantages puissants sans s'encombrer de complexités particulières.

Certes le concept même peut paraître obscur au premier abord, mais Apple avec Swift a facilité les choses de par la syntaxe très claire des protocoles.

Et j'espère également que ce tutoriel vous aura ouvert les portes de la perception dans le cas où vous aviez encore des doutes à propos de ces `delegate` que l'on voit souvent dans du code source dédié aux plateformes d'Apple. :)
