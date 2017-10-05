# Syntax object & nouvelles méthodes

### Sommaire

* [Introduction](#introduction)
* [Construction](#construction)
* [Object.assign](#object.assign)
* [Class](#class)
* [Accesseurs](#accesseurs)
* [Array](#array)
* [Methods](#methods)


<br><br><br>
## Introduction

La syntaxe d'objet a bien évolué, et a surtout était simplifié.


## Construction
La construction d'un objet se fait comme l'exemple ci-dessus avec des raccourcis de noms de propriétés :

```js

// Object structure

const full_name = 
{
	// Plus besoin d'utiliser le mot clé *function*
	getFullName(firstName, lastName)
	{
		return firstName + ' ' + lastName;
	}	
};
```

```js
// la clé porte le même nom que la variable

const firstName = 'Eric';
const lastName = 'Priou';

return {
	firstName, 
	lastName,
}

// output : {firstName : 'Eric', lastName: 'Priou'}
```
<hr>

## Object.assign()
L'`Object.assign()` sert à copier les valeurs de toutes les propriétés direct d'un objet.

```js
const obj = { full_name: 'Eric Priou' };
const copie = Object.assign({age: 25}, obj);
console.log(copie);
// output: { full_name: 'Eric Priou', age: 25 }
```
<hr>

## Class
Les classes sont juste des fonctions spéciales, utilisées pour simplifier et rendre le code plus lisible.

```js

class Person {
    constructor(name) {
        this.name = name;
    }
}

let eric = new Person('Eric');
console.log(eric.name); // Output: Eric
```
<hr>

## Accesseurs get et set
La syntaxe `get` permet de lier une propriété d'un objet à une fonction qui sera appelée lorsqu'on accédera à la propriété.

La syntaxe `set` permet de lier une propriété d'un objet à une fonction qui sera appelée à chaque tentative de modification de cette propriété.

Si je reprend la variable `full_name` :

```js

const full_name = 
{
	// Plus besoin d'utiliser le mot clé *function*
	get full_name(firstName, lastName)
	{
		return firstName + ' ' + lastName;
	}
	
	set full_name(firstName, lastName)
	{
		if((! firstName || value == ''))
			throw new Error('invalid firstName');
		
		if((! lastName || lastName == ''))
			throw new Error('invalid lastName');
			
		this.full_name = full_name
	}	
};

```
<hr>

## Array
Nouvelles méthodes ajoutées à Array :


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
<hr>

## Methods
Une méthode est une fonction qui est une propriété d'un objet.


```js
class Person {
    constructor(name) {
        this.name = name;
    }
         
    speak() {
        console.log(this.name + ' is speaking.');
    }
}
         
let eric = new Person('Eric');
console.log(eric);
// output 'Eric is speaking'
```
