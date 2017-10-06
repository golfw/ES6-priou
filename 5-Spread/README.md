# #5 spread, opérateur (...)

Le spread operator sert à eclater un tableau en liste finie de valeur.
Exemple:
```javascript
//pour la création de nouveaux tableaux
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
arr3 = [...arr1, ...arr2]; //  [0,1,2,3,4,5]
```
Sur ES5 **.concat** est utilisé pour concatener les tableaux.
Exemple:
```javascript
//pour la création de nouveaux tableaux avec .concat
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
arr3 = = arr1.concat(arr2);
```

# Utiliser la décomposition dans les objets
La décomposition d'objets permet de lier des variables à partir des différentes propriétés d’un objet.

```javascript
var array1 = { toto: 'Tata', x: 42 };
var array2 = { tata: 'Toto', y: 13 };

var clone = { ...array1 }; // Object { toto: 'Eric', x: 42 }

var fusion = { ...array1, ...array2 }; // Object { toto: 'Toto', x: 42, tata: 'Tata' y: 28 };
```

# La décomposition ne s'applique qu'aux itérables Array -> [], Object -> {}
```javascript
var obj = {"clé1" : "valeur1"};
function maFonction(x) {
  console.log(x); // undefined
}
maFonction(...obj);
var args = [...obj];
console.log(args, args.length) //[] 0
```
Pour rappel : l'opération de décomposition ne s'applique qu'aux objets itérables :

# Utiliser la décomposition dans les déclaration de fonction

On peut utiliser le Spread pour déclarer une fonction avec un nombre infini de paramètres

Exemple:
```javascript
var maFn = function(...args) {
// ma fonction
}

# Utiliser la décomposition dans les appels de fonction

Avec ES6, il est désormais possible de passer des arguments à une fonction avec le spread :

```javascript
function f(x, y, z) { }
var args = [0, 1, 2];
f(...args);
```

On peut également décomposer grâce à l'opérateur et l'opérateur peut donc utiliser plusieurs arguments :

```javascript
function f(v, w, x, y, z) { }
var args = [0, 1];
f(-1, ...args, 2, ...[3]);
```
