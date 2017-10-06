## La Programmation fonctionnelle

La programmation fonctionnelle est un paradigme de programmation (au même titre que la programmation procédurale ou objet). De la même manière que la programmation objet est une évolution de la programmation procédurale, la programmation fonctionnelle est une évolution de la programmation objet. Celle ci peut être utilisée en complément de ces deux paradigmes.

Le javascript n'est pas un véritable langage de programmation fonctionnelle (au même titre qu'`Erlang`, `Haskell`, `Elm`, `Elixir` ou encore `Scala`) cependant il intègre la plupart des concepts de programmation fonctionnelle.

## Concepts

### Immutabilité :

Un variable n’est jamais muté, cela permet de ne pas souffrir d’`effets de bord` ( c.a.d la variable n’est pas mutée à notre insu ).

```javascript
var toto = [ “titi”, “tata”]
// on recrée une variable pour éviter de muter la variable originale
var bibi = toto.push(“toto”)
// on peut aussi faire ca avec les nouvelle fonctionnalités javascript
var bibi = [...toto, “toto”]
```
Lib : <https://facebook.github.io/immutable-js/>

Une foi déclarées les données ne peuvent plus être modifiés

```javascript
const { Map } = require('immutable')
const map1 = Map({ a: 1, b: 2, c: 3 })
const map2 = map1.set('b', 50)
map1.get('b') + " vs. " + map2.get('b') // 2 vs. 50
```

## Les fonctions pures

Une fonction pure est une fonction qui remplit les 2 conditions suivantes :

* Le résultat de la fonction ne dépend que des arguments et pas du contexte extérieur
* La fonction n'a pas d'effets de bords / d'effets secondaires

On suit encore avec les fonctions pures le concept de l’immutabilité des variables

```javascript
// Cette fonction est pure car elle n'a pas d'effet de bords et ne dépend de rien d'autre que ses arguments
let push = function (tableau, clef) {
 return [...tableau, clef]
}
// Ces fonctions ne sont pas pures, car le résultat varie et ne dépend pas des arguments
Date.now()
Math.rand()
```

## Récursion

En programmation, la `récursivité` consiste à créer une méthode ou une procédure qui s’appelle elle-même.

En `Haskell` par exemple les boucles n’existent pas, il faut donc utiliser la récursivité pour faire un nombre d’operations données.

```javascript
let array = [1, 2, [3, 4], 5, [6, [7,8]]];

let addOne = function(v) {
 if(v instanceof Array) {
 // on va relancer addOne() pour 3, 4, 6, 7 et 8
 return v.map(addOne)
  } else {
    return v + 1
  }
}

// retourne [2, 3, [4, 5], 6, [7, [8, 9]]]
array.map(addOne)
```
Cf : Tail call