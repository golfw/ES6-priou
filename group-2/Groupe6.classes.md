# Classes ES6, le nouvel objet javaScript

langages orientés objet : C#, C++, Python, Java, PHP… 

### Exemple : 
* La classe : Humain
* L'objet : Un humain 
* Propriétés de l'objet : Cheveux, bras, jambes... 
* Méthodes : Marcher(), parler()... 

#### Instanciation via le constructeur : 
* Femme : Hérite de la classe Humain

## Fonctionnement de la programmation orientée objet en JavaScript

### LA CLASSE: 

**ES5 :** 
La classe en es5 était une fonction basique étant donné que le Js est un langage qui utilise les prototypes.  
Il possède en effet  un typage dynamique et ne fournit pas d'implémentation de classe avant ECMAScript 2015.

En matière d'héritage, le JavaScript n'utilise qu'un seul concept les objets. 
Chaque objet possède ainsi un lien interne vers un autre objet, appelé **prototype.**

```javascript
var Humain = function () { }
```

**ES6 :** 
En es6, on obtient enfin la possibilité d’utiliser le mot clé class pour définir une classe. 

```javascript
class Humain { }
```

__________________________


### L’OBJET & INSTANCIATION : 

L’objet est une instance de classe. L’objet est instancié de la même manière en es5 et en es6.
Le nouvel objet ainsi crée hérite des propriétés de la classe. 

**ES5 :** 

```javscript 
var Jean = new Humain();
```

**ES6 :** 

```javascript
var Jean = new Humain();
```


________________

### PROPRIÉTÉS : 

Les propriétés sont des variables appartenant à un objet. Elles peuvent être définies au sein du prototype afin que tous les objets qui en héritent les possèdent. 
On définit ainsi une propriété lors de l’instanciation de l’objet. 


**ES5 :** 

```javascript
function Humain(taille) {
	this.taille = taille;
}

var personne1 = new Humain('1m70');
var personne2 = new Humain('1m80');
```


Humain correspond ici à l’objet Humain. 

Taille est une propriété de l’objet humain. 

Personne 1 hérite de la propriété taille de l’objet Humain tout en lui ayant attribué une valeur lors de l’instanciation.


**ES6 :**

```javascript
class Humain {
  constructor(taille) {
   this.taille = taille;
   }

const Humain = new Humain(10);
```


__________________


### MÉTHODES : 

Les méthodes sont les “fonctions” d’un objet. Une fois appelées elles permettent d'exécuter les actions qu’elles contiennent.
L’appel à une méthode se fait de la même manière que pour l’accès à une propriété.


**ES5 :** 
Déclaration d’une “méthode” en es5:

```javascript
function Humain() {
	
}

Humain.prototype.marcher = function(){
	console.log('Je marche');
	}

var pierre = new Humain();

pierre.marcher();
// Je marche
```

**ES6 :** 
Déclaration d’une méthode en es6:

```javascript
class Humain {
	marcher(){
		console.log('Je marche');
	}
}
const pierre = new Humain();
```

```javascript
pierre.marcher();
// Je marche
```

### Mixins : 


```javascript
Object.prototype.mixin = function( o )
{
    for( var i in o )
    {
        this[i] = o[i];
    }
}
```

* Soit un objet une fonction de paramètre l'objet o. 
* Dans la boucle for, pour tout objet o, o[i] est assigné à this.i
* On modifie ainsi l'objet générique de JavaScript


On crée un nouvel objet 

```javascript
var humain = {}

```

```javascript
var vie ={
   poumons : 2
   , respire : function()
    {
       console.log( this.poumons + "respire" );
    }
}
```
On crée l'objet vie 

```javascript
humain.mixin(vie)
```

On ajoute l'objet à humain 

```javascript
console.log(humain)

//humain
{poumons: 2, respire: ƒ, extend: ƒ}
```

Et à l'inverse... 

```javascript
Object.prototype.unmixin = function(o)
{
   for( var i in o )
   {
       delete this[i];
   }
 
}
```

```javascript
humain.unmixin(vie)
```

```javascript
console.log(humain)

//humain
{}
```


### NOUVEAUTÉS ES6

**CONSTRUCTEUR** 

La méthode constructor est une méthode spéciale qui permet de créer et d'initialiser les objet créés avec une classe. Il ne peut y avoir qu'une seule méthode avec le nom "constructor" pour une classe donnée.

```javascript 
class Humain { 
  constructor(nom) {
    this.nom = nom;
  } 
}
```

**EXTENDS**

Le mot-clé extends, utilisé dans les déclarations ou les expressions de classes, permet de créer une classe qui hérite d'une autre classe (on parle aussi de « sous-classe » ou de « classe-fille »).

```javascript
class Humain { 
}
```

```javascript
class Sportif extends Humain {
}
```

**MÉTHODE STATIC**

Le mot-clé static permet de définir une méthode statique pour une classe. Ainsi, la méthode est appliqué à la classe elle meme et non ses instances. C'est pour cela qu'elle est surtout utilisée dans le cas de fonctions dites "utilitaires". 
```javascript
	class Humain {
		static vivre(){
		console.log('Je suis vivant!');
		}
	}
```

```javascript
Humain.vivre();
//Je suis vivant!
```

```javscript
const pierre = new Humain();
pierre.vivre();
```

```javascript
Uncaught TypeError: pierre.vivre is not a function at <anonymous>
```

Attention, les méthodes statics ne sont pas accessibles via le mot-clé this. 
Elles doivent être appelées via le nom de la classe (ici Humain) comme suit : 

```javascript
	class Humain {
		console.log(Humain.vivre()); 
   		 // 'appel de la méthode statique' 
        
    		console.log(this.constructor.vivre()); 
   		 // 'appel de la méthode statique' 
    
		static vivre(){
		console.log('Je suis vivant!');
		}
	}
```

**SUPER**

Le mot-clé super est utilisé pour appeler les fonctions rattachées à un objet parent.

```javascript
class Humain { 
  constructor(nom) {
    this.nom = nom;
  }
```
  
```javascript
marcher() {
    console.log(this.nom + ' marche.');
  }
}
```

```javascript
class Sportif extends Humain {
  courir() {
    super.marcher();
    console.log(this.nom + ' cours.');
  }
}
```

### VIDÉO : 

Vidéo complémentaire pour le cours sur l'es6 par Graphikart:

https://www.youtube.com/watch?v=5146X8FSBUQ


### Source :
https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Classes
Cerveau d'Artium, source inépuisable de savoirs
