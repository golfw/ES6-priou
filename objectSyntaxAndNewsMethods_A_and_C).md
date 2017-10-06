# Syntax object & nouvelles méthodes

### Sommaire

* [Attribute declaration](#attribute-declaration)
* [Super](#super)
* [Object Destructuring](#array-and-object-destructuring)
* [Accessors get and set](#accessors-get-and-set)
* [Object assign](#object-assign)
* [Generators](#generators)
* [New Array Methods](#new-array-methods)
* [Sources](#sources)

## Attribute declaration

La clé porte le même nom que la variable.

```js
const firstName = 'Eric';
const lastName = 'Priou';

return {
	firstName, 
	lastName,
}

// output : {firstName : 'Eric', lastName: 'Priou'}
```
[code](https://jsfiddle.net/KylianLM/39r2n4tj/)

## Super

Le super permet d'appelé une méthode dans le parent.

```js

const parent = {
    foo() {
        console.log("Hello from the Parent");
    }
}

const child = {
    foo() {
        super.foo();
        console.log("Hello from the Child");
    }
}

// Créer de l'héritage
Object.setPrototypeOf(child, parent);
child.foo(); // Hello from the Parent
			   // Hello from the Child
			   

```

## Array and Object Destructuring

```js
// for array
function foo() {
    return [1, 2, 3];
}
let arr = foo(); // [1,2,3]

let [a, b, c] = foo();
console.log(a, b, c); // 1 2 3


// for object
function bar() {
    return {
        x: 4,
        y: 5,
        z: 6
    };
}
let { x: a, y: b, z: c } = bar();
console.log(a, b, c); // 4 5 6

```

```js
var a = 1;
var b = 3;

[a, b] = [b, a];
console.log(a); // 3
console.log(b); // 1

```

## Accessors get and set


La syntaxe `get` permet de lier une propriété d'un objet à une fonction qui sera appelée lorsqu'on accédera à la propriété.

La syntaxe `set` permet de lier une propriété d'un objet à une fonction qui sera appelée à chaque tentative de modification de cette propriété.


```js
var person = {
  get getName() {
    return this.firstName;
  },
  firstName: "",
  
  set setName(text) {
  	this.firstName = text;
  }
}

console.log(person.getName); // ""
person.setName = 'Charles-Henri-Edouard';
console.log(person.getName); // "Charles-Henri-Edouard"
```

## Object assign

L'`Object.assign()` sert à copier les valeurs de toutes les propriétés direct d'un objet.

```js
const name = { firstName: 'Eric' };
const person = {age: 25, lastName: 'Priou'}
const copie = Object.assign(person, name);
console.log(copie);  // { age: 25, firstName: 'Eric', lastName: 'Priou' }
```

## Generators

L'objet `Generator` est renvoyé par une fonction génératrice, c'est à la fois un `itérateur` (cela définit une façon standard pour reproduire une suite de valeurs) qui implémente next() et un `itérable` (quelque  chose qui peut être parcourue).

La différence avec une fonction classique, est que les fonctions classiques commencent par `function`, alors que les fonctions génératrices commencent par `function*`.



```js
function* foo() { 
  yield 1;
  yield 2;
  yield 3;
}

const f = foo();
console.log(f.next()); // {value: 1, done: false}
console.log(f.next()); // {value: 2, done: false}
console.log(f.next()); // {value: 3, done: false}
console.log(f.next()); // {value: undefined, done: true}


```

Dans une fonction génératrice, `yield` est un mot-clé, avec une syntaxe similaire à return. La différence est que, tandis qu’une fonction (même un générateur) ne peut utiliser return qu’une seule fois, un générateur peut utiliser yield plusieurs fois. L’expression yield suspend l’exécution du générateur, qui peut donc être reprise plus tard.


## New Array Methods

### Array.from()
La méthode `from()` permet de créer une nouvelle instance d'Array à partir d'un objet itérable ou semblable à un tableau.


```js
const example = Array.from("example");
console.log(example);
// output:  ["e", "x", "a", "m", "p", "l", "e"];
```
<hr>

### Array.of()
La methode `of()` permet de créer une nouvelle instance d'objet Array avec un nombre variable d'argument, quels que soient leur nombre ou leur type.

```js
const example = Array.of(1, 2, 3);
console.log(example);
// output: [1, 2, 3]
```
<hr>

### Array.prototype.keys()
La méthode `keys()` renvoie un nouvel objet Array Iterator qui contient les clefs pour chaque indice du tableau.

```js
const arr = ["a","b","c"];
const example = arr.keys(); 
console.log(example);
// output: [0, 1, 2]
```
<hr>

### Array.prototype.entries() 
La méthode `entries()` renvoie un nouvel objet de type  Array Iterator qui contient le couple clef/valeur pour chaque éléments du tableau.

```js
const arr = ["a","b","c"];
const exmple = arr.entries(); 
console.log(example);
// output: Array Iterator [[0, "a"], [1, "b"], [2, "c"]]
```
<hr>

### Array.prototype.find() 
La méthode `find()` renvoie la valeur du premier élément trouvé dans le tableau qui respecte la condition donnée par la fonction de test passée en argument. Sinon, la valeur undefined est renvoyée.

```js
const arr = [{id:1, label:"hello"}, {id:2, name: "world"}]
const found = arr.find(item => item.id === 2)
const notfound = arr.find(item => item.id === 3)
console.log(found, notfound)
// output : {id:2, name: "worl"}, undefined
```
<hr>

### Array.prototype.fill() 
La méthode `fill()` remplit tous les éléments d'un tableau entre deux index avec une valeur statique.

```js
const arr = Array(3).fill(1)
console.log(arr)
// output [1,1,1]
```
<hr>

### Array.prototype.copyWithin()
La méthode `copyWithin()` effectue une copie superficielle d'une partie d'un tableau sur ce même tableau et le renvoie, sans modifier sa taille.

```js
const arr = ["hello","alice", "my", "name", "is" "bob"]
console.log(arr.copyWithin(1, 5)])
// output  "hello","bob", "my", "name", "is" "bob"]
```


## Sources

<a href="https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Opérateurs/Initialisateur_objet">Mozilla : Initialisateur d'objet</a>

<a href="https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Array/from">Mozilla : Array.from()</a>

<a href="https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Array/keys">Mozilla : Array.prototype.keys()</a>

<a href="https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Array/entries">Mozilla : Array.prototype.entries()</a>

<a href="https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Array/find">Mozilla : Array.prototype.find()</a>

<a href="https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Array/fill">Mozilla : Array.prototype.fill()</a>

<a href="https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Array/copyWithin">Mozilla : Array.prototype.copyWithin()</a>

<a href="https://tech.mozfr.org/post/2015/05/23/ES6-en-details-%3A-les-generateurs">ES6 en détails :  les générateurs</a>

<a href="https://learn-anything.xyz/programming/programming-languages/javascript/es6">Learn-anything Javascript ES6</a>

