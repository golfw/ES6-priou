# La Programmation fonctionnelle 

## Introduction

La programmation fonctionnelle est un paradigme de programmation (au même titre que la programmation procédurale ou objet). Elle devient très populaire ses derniers temps en raison de la présence de large volumes de données, là ou la syntaxe dite "Orientée Objet" montre certaines limites à en traiter d'aussi grandes quantités.

Le javascript n'est pas un véritable langage de programmation fonctionnelle (au même titre qu'`Erlang`, `Haskell`, `Elm`, `Elixir` ou encore `Scala`) cependant il intègre la plupart des concepts de programmation fonctionnelle.

## Concepts

### Immutabilité

Un variable n’est jamais mutée, cela permet de ne pas souffrir d’**effets de bord** (c.a.d la variable n’est pas mutée à notre insu).
en programmation fonctionnelle, x = x + 1 est illégal. **Il n'y a pas de variables dans la programmation fonctionnelle**.
Les valeurs stockées sont encore nommées des variables du fait de leur fonctionnalité historique au sein de la machine virtuelle ecmascript, mais elles doivent être utilisées plutôt comme des **constantes** ; c'est-à-dire une fois que x prend une valeur, cette dernière restera invariante.

```javascript
var toto = [ “titi”, “tata”]
// on recrée une variable pour éviter de muter la variable originale
var bibi = toto.push(“toto”)
// on peut aussi faire ca avec l'opérateur de decomposition es6
var bibi = [...toto, “toto”]
```
#### Comparaison avec Elixir:

> **Note** Une petite explication serait la bienvenue…

```elixir
map_set = MapSet.new
MapSet.put(map_set, "foo") # MapSet<["foo"]>
# Pipe Operateur <3
map_set
  |> MapSet.put("foo")
  |> MapSet.put("foo") # MapSet<["foo"]>
```

#### La librairie [Immutable.js](https://facebook.github.io/immutable-js/)

Les données définies à partir de _Collections_ d'immutable.js ne peuvent pas être modifiées une fois créées, ce qui permet un développement d'applications sans effet de bord.

La librairie propose les structures non mutables suivantes : `List`, `Stack`, `Map`, `OrderedMap`, `Set`, `OrderedSet` et `Record`.

```javascript
// importe l'objet Map de immutable.js
const { Map } = require('immutable')
// on peut faire toto ou "toto"
let lol = Map({ toto: "omg" })
console.log( Map.isMap(lol) )//true
console.log( lol.get("toto") )//omg
lol.set( {"immutable" : "mwai"} )
console.log( lol )// <--- Map { "toto": "omg" } !!
```
Avec l'objet Map, les valeurs sont uniquement accessibles via un getter

```javascript
const { OrderedMap } = require('immutable')
let hi = OrderedMap({un: "one"})
let jh = OrderedMap({deux: "two"})
let azerty = hi.concat(jh)
azerty // OrderedMap {size: 2, _map: Map, _list: List, __ownerID: undefined, __hash: undefined}
azerty.map(x => console.log(x)) // one, two
```

Une `Map` garanti également que l'ordre d'itération des clés entrées sera dans le même ordre que lors de leur insertion via la méthode `set()`.

### Les fonctions pures

Une fonction pure est une fonction qui remplit les 2 conditions suivantes :

* Elle prend au moins un argument (voir plus loin)
* Le résultat de la fonction ne dépend que des arguments et d'aucun contexte extérieur
* La fonction n'a pas d'effets de bords / d'effets secondaires

> **Hint** D'une certaine façon, les fonctions pures poursuivent le même concept d’immutabilité des variables, cette fois attribué aux opérations.**

> **Note** Exemples pas très convaincants 
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

> **Warning** La fonction *justTen* est pure, et peut seulement retourner une constante, car elle ne prend aucun paramètre et en vertu de l'immutabilité, elle ne peut accéder qu'à ses propres paramètres, c'est-à-dire à son contexte lexical propre, seule une constante pourra être retournée.
Voilà pourquoi, les fonctions pures sans paramètre ne sont pas du tout utiles.

&nbsp;
> **Hint** Notion Avancée :
[lambda, filter , map et reduce en Javascript](https://www.youtube.com/watch?v=woySeSNBL3o)

### 3. Récursivité

En programmation, la `récursivité` consiste à créer une méthode ou une procédure qui s’invoque elle-même.

En `Haskell` par exemple les boucles n’existent pas, il faut donc utiliser la récursivité pour faire un nombre d’operations données.
Cependant cette pratique n'est pas toujours recommandée en Javascript du fait de l'abscence du *Tail Call* , on parlera plus de [feature instable](https://nodejs.org/en/docs/es6/) avec les dernieres version de node.js  

:grey_exclamation: **Notion Avancée :**
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

## Sources

#### Articles en anglais :

- [un article de ouf sur Medium](https://medium.com/@cscalfani/so-you-want-to-be-a-functional-programmer-part-1-1f15e387e536)  
- [Le must de la programmation function en es6](https://leanpub.com/javascriptallongesix/read)
- [Série d'articles suivre](https://medium.freecodecamp.org/functional-programming-in-js-with-practical-examples-part-1-87c2b0dbc276)
- [Un article de fond qui avait disparu (merci la wayback machine)](
https://web.archive.org/web/20170202023826/https://medium.com/@xilefmai/efficient-javascript-14a11651d563)
- [Introduction à la programmation fonctionnelle en ecmascript](https://medium.com/@chetcorcos/functional-programming-for-javascript-people-1915d8775504)

#### En français :
 
[La programmation fonctionnelle, Grafikart](https://www.grafikart.fr/tutoriels/divers/programmation-fonctionnelle-878)

#### Langages :
 
[Elixir](https://elixir-lang.org/docs.html)  


## Participants

[Constantin Guidon](https://github.com/zelazna)
[Chloé Echasseriau](https://nemeditpasquetunaspasdecomptegithub.pasnet)
