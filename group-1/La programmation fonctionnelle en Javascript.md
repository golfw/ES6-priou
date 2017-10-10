# La Programmation fonctionnelle

***auteurs : Constantin Guidon , Chloé Echasseriau***  

## Table des Matieres
  1. [Immutabilité](#1-immutabilité)  
  2. [Fonctions Pures](#2-les-fonctions-pures)  
  3. [Récursivité](#3-récursivité)   
  4. [Immutable.js](#4-Immutable.js)

## Introduction

La programmation fonctionnelle est un paradigme de programmation (au même titre que la programmation procédurale ou objet). Elle devient tres populaire ces derniers temps en raison de la précense de larges volumes de données, la ou la programmation dite "Orientée Object" montrant ses limites a traiter d'aussi grandes quantités de données 

Le javascript n'est pas un véritable langage de programmation fonctionnelle (au même titre qu'`Erlang`, `Haskell`, `Elm`, `Elixir` ou encore `Scala`) cependant il intègre la plupart des concepts de programmation fonctionnelle.

## Concepts

### 1. Immutabilité

Un variable n’est jamais mutée, cela permet de ne pas souffrir d’`effets de bord` (c.a.d la variable n’est pas mutée à notre insu).
en programmation fonctionnelle, x = x + 1 est illégal. **Il n'y a pas de variables dans la programmation fonctionnelle**.
Les valeurs stockées sont toujours appelées variables à cause de l'historique mais elles sont des **constantes**, c'est-à-dire une fois que x prend une valeur, c'est cette valeur pour la vie.

```javascript
var toto = [ “titi”, “tata”]
// on recrée une variable pour éviter de muter la variable originale
var bibi = toto.push(“toto”)
// on peut aussi faire ca avec les nouvelle fonctionnalités javascript
var bibi = [...toto, “toto”]
```
**Elixir:**

```elixir
map_set = MapSet.new
MapSet.put(map_set, "foo") # MapSet<["foo"]>
# Pipe Operateur <3
map_set 
  |> MapSet.put("foo") 
  |> MapSet.put("foo") # MapSet<["foo"]>
```

### 2. Les fonctions pures

Une fonction pure est une fonction qui remplit les 2 conditions suivantes :

* Elle prennent au minimum un seul argument (voir plus loin)
* Le résultat de la fonction ne dépend que des arguments et pas du contexte extérieur
* La fonction n'a pas d'effets de bords / d'effets secondaires

On suit encore avec les fonctions pures le concept de l’immutabilité des variables:

```javascript
// Cette fonction est pure car elle n'a pas d'effet de bords et ne dépend de rien d'autre que ses arguments
let push = function (tableau, clef) {
 return [...tableau, clef]
}
// Ces fonctions ne sont pas pures, car le résultat varie et ne dépend pas des arguments
Date.now()
Math.rand()
```

Un autre Exemple 

```javascript
function justTen() {
    return 10;
}
```

La fonction *justTen* est pure, et peut seulement retourner une constante, car elle ne prend aucun parametre et en vertu de l'immutabilité, elle ne peut accedder que a ses propres parametres, la seule chose quel peut donc retouner n'est qu'une constante.

*Vu que les fonctions pures qui ne prennent pas de parametres ne marchent pas, elles ne sont pas vraiment utiles.*

**Notion Avancée :**
[filter , map et reduce en Javascript](https://www.youtube.com/watch?v=woySeSNBL3o)

## 3. Récursivité

En programmation, la `récursivité` consiste à créer une méthode ou une procédure qui s’appelle elle-même.

En `Haskell` par exemple les boucles n’existent pas, il faut donc utiliser la récursivité pour faire un nombre d’operations données.
Cependant cette pratique n'est pas toujours recommandée en Javascript du fait de l'abscence du *Tail Call* , on parlera plus de [feature instable](https://nodejs.org/en/docs/es6/) avec les dernieres version de node.js  

**Notion Avancée :**
[*Tail call*](http://benignbemine.github.io/2015/07/19/es6-tail-calls/)
```shell 
node index.js --harmony --harmony_tailcalls
``` 

qui, en ne rentrant pas dans les details, optimise la recursivité des fonctions.

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

## Lib 

#### 4. [Immutable.js](https://facebook.github.io/immutable-js/)

Les données immutable ne peuvent pas être modifiées une fois créées, ce qui permet un développement d'applications beaucoup plus simples,et permet des techniques avancées de mémorisation et de détection de changement avec une logique simple.

```javascript
// importe l'objet Map de immutable 
const { Map } = require('immutable')
// on peut faire toto ou "toto"
let lol = Map({ toto: "omg" })
Map.isMap(lol) //true
lol.get("toto") //omg
lol.set({"immutable" : "mwai"})
```
Avec l'objet Map par exemple les valeurs sont uniquement accessibles via un getter

```javascript
const {OrderedMap} = require('immutable')
let hi = OrderedMap({un: "one"})
let jh = OrderedMap({deux: "two"})
let azerty = hi.concat(jh)
azerty // OrderedMap {size: 2, _map: Map, _list: List, __ownerID: undefined, __hash: undefined}
azerty.map(x => console.log(x)) // one, two
```

Un type de Map qui a la garantie supplémentaire que l'ordre d'itération des entrées sera l'ordre dans lequel elles ont été set().