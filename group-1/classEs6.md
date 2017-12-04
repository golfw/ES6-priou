# Les classes ES6

#### Participants :

+ [Denis Masot](https://github.com/DenisMasot)
+ [Clara Fourcade](https://github.com/Tretiakoff)
+ [Maxime Ferraille](https://github.com/maximeferraille)
+ [Valentin Chevreau](https://github.com/valentinch)
+ [Marie Gellez](https://github.com/gellezmarie)

#### Introduction
En programmation orienté objet, une classe déclare des propriétés commune à un ensemble d’objet. C’est à dire des attributs qui représentent l’état des objets et des méthode qui représentent leur comportements. c’est donc une catégorie d’objet. C’est comme une « boite à outil » qui permet de fabriquer un objet. 

Par exemple on crée un plan de construction d’une maison qui réunit les instructions destinés à la construction. Mais le plan n’est pas la maison. La maison c’est l’objet instance à partir de la classe (qui est le plan ici). 
A partir du plan (la classe) on peut construire une autre maison (l’objet). 
En fait, la classe c’est le modèle, et la maison une instance.

## Déclaration d'une classe
On utilise le mot-clé “class” suivi du nom qu’on veut lui donner.
```javascript
class Toto
{
 // Contenu de la classe
}
```
Pour utiliser une classe, on appelle la classe par son nom précédé de “new” à l'intérieur d’une variable. Il est nécessaire de déclarer la classe avant de l’instancier (on ne peut pas instancier une classe qui n’existe pas) sinon on recevra l’erreur `Reference Error`.
```javascript
var classe_toto = new Toto();
```
Actuellement, notre “classe_toto” va nous renvoyez “undefined” car la classe est vide. 

## Le corps d'une classe
Le corps d’une classe est la partie contenue entre les accolades. C’est dans cette partie que l’on définit les propriétés d’une classe comme ses méthodes et son constructeur.

Le corps d’une classe est exécuté par défaut en **mode strict**. Ce mode **élimine quelques erreurs silencieuses** de JavaScript en les changeant en erreurs explicites (une exception sera levée). 
Il corrige les erreurs qui font qu'il est difficile pour les moteurs JavaScript d'effectuer des optimisations.
Le **code sera exécuté plus rapidement** en mode strict, sans en changer une seule ligne. Et il interdit les mot-clés susceptibles d'être définis dans les futures versions de ECMAScript.

Les méthodes d'une classe sont **l’ensemble des propriétés qui constitue la classe** : le constructeur, les différentes fonctions. Les getter et les setters. Il existe plusieurs types de fonctions au sein d’une classe : les méthodes static et de prototypes. 

#### Le constructeur
Le constructeur est une méthode qui permet de créer les objets et d’initialiser les paramètres utiliser par la classe.
Il ne peut y avoir qu'une seule méthode avec le nom "constructor" pour une classe donnée. Si la classe contient plusieurs occurrences d'une méthode constructor, cela provoquera une erreure **SyntaxError**.

```javascript
class Toto
{
    constructor (year, gender)
    {
        this.year = year
        this.gender = gender
    }
}
```
Désormais on peut donc instancier notre classe avec des paramètres :
```javascript
var classe_toto = new Toto(1997, 'other');
```

#### Les méthodes statique
Les méthodes statiques sont utilisées lorsque la **méthode ne s'applique qu'à la classe elle-même et pas à ses instances**. Les méthodes statiques sont généralement utilisées pour créer des fonctions utilitaires.
Pour utiliser une méthode statique il faut utiliser le mot clé : ```static```

```javascript
class Toto
{
     static ageFormat ()
     {
        // Contenu de la méthode...
     }
}
```

#### Les méthodes de prototype
La quasi-totalité des objets Javascript descendent de `object` . Ici aussi les classes en javascript descendent de `object` et recevera donc les propriétés de `Object.prototype`. Tel que les getter et les setter.
#### Setter et Getter
Ces éléments présents dans la classe permettent de définir les variables et de les afficher.
`set` récupère le contenu des variables qui ont été saisis tandis que `get` permet de retourner le contenu voulu.
```javascript
class Toto
{
    constructor (year,gender) 
    {
        this._year = year
        this.gender = gender
    } 
    get age() 
    {
        return this.calcAge()
    }
    
    set name(name)
    {
      this._name = name   
    }
    
    calcAge() 
    {
        var currentTime = new Date() 
        var currentYear = currentTime.getFullYear()
        return currentYear - this._year
    }
}
```
Pour instancier notre classe : 
```javascript
var classe_toto = new Toto(1997,'other');
classe_toto.name('Toto') // On donne à la variable name la valeur "Toto"
console.log(classe_toto.age) // Renverra l'âge de Toto
```

## Héritage

Le constructeur ainsi déclaré peut utiliser le mot-clé “super” afin d'appeler le constructeur de la classe parente.
L’héritage permet d’associer un objet avec n’importe quelle constructeur. On peut faire communiquer les classes entre elles, c’est la notion de l’héritage. On peut faire hériter une classe fille de tous les attributs et méthodes d’une classe mère. 

Nous allons citer des exemples afin de mieux comprendre. Il existe trois manières de faire hériter des classes en JavaScript. La première se base sur le constructeur de la classe mère, la seconde sur le prototype de la classe mère et la troisième est la combinaison des deux. 

* Héritage par le constructeur de la classe mère : Cela consiste à faire une “recopie” du constructeur de la classe mère vers une méthode de la classe fille. Quant on appellera cette méthode, elle va s’initialiser en se fondant sur le constructeur de la classe mère. 
Le code :
```javascript
function classeMere() 
{
    this.attribut = attribut1;
}
classeMere.prototype.methodeA() = function() 
{
    // code
}

classeMere.prototype.methodeB() = function() 
{
    // code
}
function classeFilleExtendsMere() 
{
classeMere.call(this); // Héritage
```
Correspond à :
```javascript
    this.parent = classeMere; // Héritage
    this.parent();
}
```

* Héritage par le prototype de la classe mère : Il existe deux manières de réaliser un héritage en se basant sur le prototype de la classe mère.
```javascript
function classeMere()
{
    this.attribut = attribut1;
}
classeMere.prototype.methodeA() = function() 
{
    // code
}
classeMere.prototype.methodeB() = function() 
{
    // code
}
function classeFilleExtendsMere() {
}
// Recopie des éléments au moyen d'une simple boucle
 
for (var element in classeMere.prototype )
{
    classeFilleExtendsMere.prototype[element] = classeMere.prototype[element]
}
```
#### Sous classes
Depuis l'ecma script 6 nous pouvons hérité une classe à une autre grâce au mot clé `extends`. On appel cela aussi **une sous classe**

```javascript
class Animal 
{ 
  constructor(nom) {
    this.nom = nom;
    }
  
  parle() {
    console.log(this.nom + ' fait du bruit.');
  }
}

class Chien extends Animal
{
  parle() {
    console.log(this.nom + ' aboie.');
  }
}
```
Si nous voulons utiliser une méthode de la classe parente dans notre classe fille. Donc dans l'exemple ci-dessus utilisé la méthode parle dans la classe `Chien` sans devoir en récréer une nouvelle comme nous venons de faire, il faudra utilisé le mot clé `super`.
Ce qui va nous donner : 
```javascript
class Animal 
{ 
  constructor(nom) {
    this.nom = nom;
    }
  
  parle() {
    console.log(this.nom + ' fait du bruit.');
  }
}

class Chien extends Animal
{
  parle() {
    super.parle // utilise la méthode parle de la classe Animal
    console.log(this.nom + ' aboie.');
  }
}
```
Si on instancie notre classe et qu'on regarde ce que fais parle on aura : 
```javascript
    var mon_chien = new Chien('Nolan');
    mon_chien.parle // Renverra deux console log "Nolan fait du bruit" et "Nolan aboie": 
```

## Sources
+ http://es6-features.org/#ClassDefinition
+ https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Classes


