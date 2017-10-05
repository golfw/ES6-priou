## La modularité
5 oct. 2017 à 16:20
- - - -
Source : [16. Modules](http://exploringjs.com/es6/ch_modules.html)

::**Introduction**::

La modularité correspond à découper son code en plusieurs parties.
Avant ES6, il y avait deux façon de modularité son code en utilisant Common.JS module et Asynchronous Module Définition (AMD).

**Voici un exemple d’une des méthode (Common.JS) :**

```
//——— a.js ------
var b = require(‘b’);
function foo() {
    b.bar();
}
exports.foo = foo;

//------ b.js ------
var a = require(‘a’); // (i)
function bar() {
    if (Math.random()) {
        a.foo(); // (ii)
    }
}
exports.bar = bar;
```

Avec les grosses applications qui utilise JavaScript, nous nous heurtons à problèmes inhérents à la cohabitation de bibliothèques JavaScript et d’autres script personnels.
C’est pour cette raison que la modularisation à été introduite en ES6. Plus besoin d’utiliser des librairies comme Common.JS ou AMD.


::**Corpus**::

Bien que JavaScript n’ai jamais eu de module intégré, la communauté EcmaScript a décidé pour l’ES6 de converger vers un style simple de module.

En effet, chaque déclaration dans un module reste locale à celui-ci.
Chaque module peut être appelé par un autre. Ce dernier est un morceau de code qui est exécuté une fois que le module est chargé.
On parle également de « singleton » : c’est à dire que même si il est importé plusieurs fois dans un projet, il ne sera instancié qu’une seule fois.

Grâce à la modularité, _adieu les variables globales !_

Le modules permettent d’arrêter la solution du namespace, en rendant privé les espaces correspondant à chaque module.

**Types d’exports :**

Il y a deux sortes d’exports, par nom et par module. Il est possible d’utiliser les deux en même temps, mais il est préférable de les séparer.

• Exports par nom :

- [ ] Argumenter - courte introduction

```
//------ lib.js ------
export const sqrt = Math.sqrt;
export function square(x) {
    return x * x;
}
export function diag(x, y) {
    return sqrt(square(x) + square(y));
}

//------ main.js ———
import { square, diag } from 'lib';
console.log(square(11)); // 121
console.log(diag(4, 3)); // 5
```

Nous pouvons aussi importer tout le module et faire référer les noms des exports à l’export générale de celui-ci.

Exemple :

```
//------ main.js ------
import * as lib from ‘lib’;
console.log(lib.square(11)); // 121
console.log(lib.diag(4, 3)); // 5
```

• Exports de type « défaut » :

Ce type d’export est très utile pour affecter un module à une fonction directement ou à une classe.

Exemple pour une fonction :

```
//------ myFunc.js ------
export default function ()
{
	console.log('hello')
}

//------ main1.js ------
import myFunc from ‘myFunc’;
myFunc(); // hello
```

Exemple pour une classe :

```
//------ MyClass.js ------
export default class {} // no semicolon!

//------ main2.js ------
import MyClass from ‘MyClass’;
const inst = new MyClass();
```


**Structure des imports et des exports**

La structure de l’ES6 étant statique, nous ne pouvons pas importer et exporter dans des boucles conditionnelles. Ils doivent se faire au plus haut niveau du module.




