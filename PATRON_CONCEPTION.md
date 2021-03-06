
# Les patrons de conception

<br />

<div class="center">
    <img src="img/lego3-selection.jpg" />
</div>

---

# Introduction


---

## Pourquoi faire des efforts de conception?

Il faut avoir en tête la seule constante du développement : Le changement !

* Modification des fonctionnalités et modèles
* Changement de cible (desktop, serveur, mobile, etc.)
* Augmentation des volumes de données (parallélisation, etc.)
* Obsolescence des outils
* Choix politique (base de données, etc.)
* ...

---

## Quels sont les critères qualités d'un programme?

On vise (et on priorise !) plusieurs critères :

* Fiabilité
* Maintenabilité
* Performance
* Evolutivité
* Réutilisabilité
* Portabilité
* Testabilité
* ...


---

## Les patrons de conception dans tout ça?

C'est ce que nous allons voir!

Nous allons ballayer un ensemble de prérequis pour bien les comprendre :

* Rappel sur les bases de la P.O.O.
* Rappel sur les principes de conception

Nous verrons quelques mauvaises pratiques à travers les anti-patterns. Puis,
nous nous attarderons sur les bonnes pratiques en parcourant les design pattern.

---

# Plan

* Introduction
* Les bases de la P.O.O.
* Les principes de conception
* Les anti-patterns
* Les designs patterns
* Les patrons de création
* Les patrons de structure
* Les patrons de comportement
* A vous maintenant!
* Annexe
* Bibliographie

---

# Les bases de la P.O.O.

---

## Les concepts de base (1/3)

* Classe et objet
* Méthode et constructeur
* Encapsulation (getter, setter, visibilité)
* Abstraction

---

## Les concepts de base (2/3)

Par rapport aux aggrégats de variables (struct en C), on dispose d'outils
permettant d'assurer la cohérence des variables formant l'aggrégat

* Constructeurs : Fonction init que l'on est obligé d'appeler
* Getter/Setter : Protection des variables de l'aggrégat

---

## Les concepts de base (3/3)

On dispose aussi d'outils pour des modélisations complexes :

* Les relations (composition, aggrégation)
* Polymorphisme et héritage
* Classe abstraite et interface

Généralement, ces outils sont plutôt bien maîtrisés pour modéliser
des données (objet de domaine).

Nous verrons ici comment on peut les exploiter efficacement pour faire varier le comportement d'un programme.

---

## Bien comprendre l'intérêt de ces concepts!

* Il ne suffit pas de connaître vaguement ces concepts pour bien programmer en P.O.O.
* Les patrons de conception font appel à des utilisations avancées de ces concepts.

=> [Méditons quelques exemples](ex_base_poo.html)

---

## Les concepts avancés

Les langages ont leurs spécificités qui doivent être prises en compte dans la conception :

* Property (getter/setter "magiques")
* Garbage collector
* Programmation générique/template
* Introspection et réflexion

---

# Les principes de conception

Les patrons de conception que nous allons bientôt voir sont (entre autres) une
mise en pratique de principes de conception qui s'ajoutent aux principes
de base de la P.O.O. (abstraction, encapsulation, etc.) et qu'il faut avoir en tête.

---

## SOLID (1/2)

### (S)ingle Responsibility

Une classe remplit une fonction et une seule.

### (O)pen Closed

Une classe est ouverte à l’extension, mais fermée aux modifications.

---

## SOLID (2/2)

### (L)iskov Substitution Principle

Lorsqu’une classe se substitue à une autre, le programme continue de fonctionner.

### (I)nterface Segregation

Préférer plusieurs interfaces spécifiques pour chaque client plutôt qu'une seule interface générale.

### (D)ependency Inversion

Il faut dépendre des interfaces, pas des implémentations (classe concrète).

---

## DRY : Don't Repeat Yourself

Le copier/coller n'est pas une méthode acceptable de réutilisation des codes.

Quand on veut réutiliser un code, on le met en facteur.


## YAGNI : you ain't gonna need it

On ne code que ce qui est utile. On n'ajoute pas des codes en se disant que ça
servira un jour.

---

## Identifier et encapsuler ce qui varie (1/2)

Cas d'école : J'identifie le besoin d'écrire mes logs dans la console
ou dans un fichier...

```
class MaClasse {

    public void faireUnTruc(){
        System.out.println("Je fais un truc");
        // ...
    }

}
```

---

## Identifier et encapsuler ce qui varie (2/2)

... je fais abstraction sur l'écriture des logs

```
class MaClasse {

    private Logger logger ;

    public void faireUnTruc(){
        logger.info("Je fais un truc");
    }

}
```


---

## Préférer la composition à l'héritage

* On hérite d'une classe seulement si on peut dire "EST-UN"
* On n'hérite pas d'une classe dans le but de réutiliser ses méthodes !
* On préfère les états aux classes dérivées (rôle d'utilisateur)

(Nous verrons en détail pourquoi quand nous aborderons le patron [Strategy](behavior/Strategy.html))

---

# Les anti-patterns

Avant de mettre un nom sur des modèles de conception, on va mettre un nom sur des erreurs de conception courrantes : Les anti-pattern !

---

## Principe des anti-patterns

* Nommer des erreurs de conception classiques
* Faciliter l'identification des erreurs de conception

---

## Réinventer la roue carrée

Ne pas s'appuyer sur une solution existante.

---

## Programmation spaghetti

Le rôle des différents éléments du système n'est pas identifiable. Il est difficile de modifier une partie du code sans en altérer le fonctionnement.

---

## Objet divin

L'objet divin porte un trop grand nombre de responsabilités.

---

## Abstraction inverse

Un composant ne fournit pas les abstractions nécessaires, mais seulement les méthodes
les plus compliquées.

Les abstractions sont effectuées dans les clients.

---

## Marteau doré

Avec un bon marteau, tous les problèmes sont des clous!

<div class="center">
    <img src="img/golden-hammer.jpg" alt="Marteau d'or" />
    <br />
    (En vente sur
    <a href="http://www.engravingawardsgifts.com/sledgehammers.html">engravingawardsgifts.com</a>)
</div>

Un outil est placé comme solution à tous les problèmes. Il peut être question
d'une bibliothèque, d'une base de données, d'une suite de logiciel, etc.

---

## Coulée de lave

Un code non finalisé est mis en production. Il n'est plus possible de le refactorer.

Ce problème peut concerner aussi bien des bibliothèques que des API.

---

## Premature Optimisation (1/2)

"Premature optimization is the root of all evil" (Donald Knuth)

* Gaspillage d'énergie pour des gains médiocres (voire négatifs).
* Complexité rendant impossible les optimisations globales.
* Complexité mettant en péril la qualité du logiciel (stabilité, maintenabilité, portabilité, etc.)

Exemple : 

* Optimiser le parcours séquentiel d'un tableau au point qu'il devient impossible d'exploiter un indexe.
* "Je n'ai pas besoin des arcs entrants pour cet algorithme, je fais un graphe dédié qui consommera moins de mémoire!" : Qu'importe si le programme réel passe son temps à faire des copies...

---

## Premature Optimisation (2/2)

"Premature optimization is the root of all evil" (Donald Knuth)

mais...

* Il ne faut pas en conclure qu'on doit ignorer l'optimisation dans la conception!
* Il faut rester prudent sur cette affirmation pour les bibliothèques de bas niveau!
* Parfois, on prévilégie la performance à la portabilité.

Proposition de méthode :

* Se concentrer sur les optimisations globales (structure efficace, indexation, gestion des caches, etc.) dans la conception.
* Coder en mettant en place des tests et des benchs.
* Profiler et réaliser les optimisations locales sur les fonctions souvent appelées.

---

# Les designs patterns

On y est! Alors, les patrons de conception, Quésako?

---

## Définition

Le concept de patron de conception a été défini par le « Gang of Four » (Erich Gamma, Richard Helm, Ralph Johnson et John Vlissides) dans le livre "Design Patterns -- Elements of Reusable Object-Oriented Software" (1994).

Un design pattern est la description d'une solution réutilisable pour un problème de conception.

---

## Famille de patrons de conception du GoF

* Les patrons de création (creational patterns) qui décrivent des techniques
d'initialisation des objets.
* Les patrons de structure (structural patterns) qui décrivent des organisations
classiques de classes.
* Les patrons de comportement (behavioral patterns) qui décrivent des méthodes
de communications entre objets au sein d'une application.

---

## Autres familles de patrons de conception

* Les patrons architecturaux qui traitent des styles d'architecture de logiciel (MVC, micro-service, etc.)
* Des familles de patrons spécifiques à des domaines d'application (cloud computing, etc.)
* Des familles de patrons spécifiques à des frameworks (spring, etc.)

---

## Formalisme des design patterns

* Un nom
* Un problème
* Une solution
* Des conséquences (avantages et inconvénients)

---

## Intérêts des design patterns (1/2)

* Utiliser un vocabulaire commun
* Trouver de l'inspiration dans la recherche d'une solution
* Uniformiser la conception (MVC, IoC, MQ, etc.)
* Faciliter la compréhension des codes

---

## Intérêts des design patterns (2/2)

En pratique, vous retrouverez plus facilement vos petits en Java et dans les frameworks orientés objet :

* Connaissance du vocabulaire commun (```*Builder, *Factory, *::getInstance, addChild, etc.```).
* Compréhension des architectures par identification des patterns.

Aussi, vous pourrez rechercher des solutions aux problèmes classiques que vous rencontrez :

* Comment faire un interpréteur?
* Comment faire un undo/redo?
* Est-ce qu'il y a un framework MVC pour ce langage?

---

# Les patrons de création

* [Singleton](creational/Singleton.html)
* [Prototype](creational/Prototype.html)
* [Factory (Fabrique)](creational/Factory.html)
* [FactoryMethod](creational/FactoryMethod.html)
* [Builder (Monteur)](creational/Builder.html)
* [AbstractFactory (Fabrique abstraite)](creational/AbstractFactory.html)

---

# Les patrons de structure

* [Facade (Façade)](structural/Facade.html)
* [Decorator (Décorateur)](structural/Decorator.html)
* [Composite (Objet composite)](structural/Composite.html)
* [Adapter (Adaptateur)](structural/Adapter.html)
* Bridge (Pont)
* Proxy
* Flyweigth (Poids-mouche)

---

# Les patrons de comportement

* [Iterator (Itérateur)](behavior/Iterator.html)
* [Strategy (Stratégie)](behavior/Strategy.html)
* [Visitor (Visiteur)](behavior/Visitor.html)
* Chain of responsability (Chaîne de responsabilité)
* Command (Commande)
* Interpreter (Interpréteur)
* Mediator (Médiateur)
* Memento (Mémento)
* [Observer (Observateur)](behavior/Observer.html)
* State (État)
* Template Method (Patron de méthode)

* [Null Object (objet null)](behavior/NullObject.html)

---

# Les patrons de conception architecturaux

---

## Quelques exemples de patrons de conception architecturaux

* Architecture en couche
* Architecture micro-service
* [MapReduce](architectural/MapReduce.html)
* [Model-View-Controller (MVC)](architectural/MVC.html)
* [Inversion de contrôle (IoC)](https://github.com/mborne/spring-ioc-principe)
* Event-Driven architecture/Message Oriented Middleware (MOM)

Et bien d'autres en fonction des domaines (réseau, cloud computing, etc.)

---

## Les stacks applicatives

Dans la mesure où les composants remplacent les bibliothèques, les stacks 
applicatives traduisent des patrons de conception architecturaux.

* RabbitMQ/ActiveMQ

Utilisation de pile de message pour les traitements asynchrones, distribués, sur 
des systèmes hétérogènes.

* Service de stockage de fichier (Amazone S3, Ceph, etc.)

Utilisation de serveur dédiés au stockage de fichiers téléchargeables.

* Stockage clé valeur (memcached, redis, etc.)

Stockage des sessions, des caches, etc.

---

# A vous maintenant!

---

## Comment progresser?

* Comprendre et apprendre les principaux patrons de conception

* Identifier les patrons de conception dans les codes existants : Rechercher les fabriques, les monteurs, les stratégies, les décorateurs, etc.

* Expérimenter!

* Concevoir des codes en pensant règle de conception et patron de conception

* Concevoir des codes en les testant unitairement (on ne peut pas tester des codes qui sont mal conçus)

* Comprendre des architectures : Pourquoi stocker des sessions PHP dans memcached et des fichiers dans des serveurs tiers?

---

# Annexe

* [TP - Mise en oeuvre des patterns sur des Geometry](https://github.com/mborne/tp-pattern-geometry)
* [Les grands principes du refactoring de code](refactoring.html)
* [Outils pour la gestion des dépendances (Java, PHP, NodeJS, JavaScript, C++)](dependances.html)

---

# Bibliographie

* Design Patterns: Elements of Reusable Object-Oriented Software (Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides)

* Tête la première dans les Design Patterns, O'Reilly

Présente les designs patterns à travers des problématiques concrètes de conception. Le style 
d'écriture rend la lecture plus agréable que le parcours d'un catalogue.

* Design Patterns, Catalogue de modèles de conceptions réutilisables, Vuibert

* Microsoft Application Architecture Guide, 2nd Edition

Disponible gratuitement au format PDF, ce guide initialement rédigé à l'attention
des développeurs DotNet traite des problématiques générales sur l'architecture logicielle :
Principes de conception, critères qualités, styles d'architecture, etc.

---

# Bibliographie

* WIKIBOOK, Patrons de conception/Patrons du « Gang of Four »
[https://fr.wikibooks.org/wiki/Patrons_de_conception](https://fr.wikibooks.org/wiki/Patrons_de_conception)

* [Design Patterns sur sourcemaking.com](https://sourcemaking.com/design_patterns)

Catalogue des principaux patrons de conception avec des exemples dans plusieurs langages.

* [AntiPatterns sur sourcemaking.com](https://sourcemaking.com/antipatterns)

Catalogue des principaux anti-pattern.

* [Design Patterns du Gang of Four appliqués à Java, Régis POUILLER, developpez.com](http://rpouiller.developpez.com/tutoriel/java/design-patterns-gang-of-four/)

Explication de l'intérêt des patterns du GoF et implémentation en Java.



