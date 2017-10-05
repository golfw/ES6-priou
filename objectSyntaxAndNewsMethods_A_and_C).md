# Syntax object & nouvelles méthodes
<hr>

### Sommaire

* [Introduction](#introduction)
* [Construction](#construction)
* [Object.assign](#object.assign)
* [Class](#class)
* [Accesseurs](#accesseurs)
* [Array](#array)
* [Methods](#methods)


<br><br><br>
## Introdcution

Le JavaScript se voit évoluer depuis longtemps, et a été mis en second plan dans la conception des pages web. Aujourd'hui, c'est une autre histoire, on parle d'application web, qui son entièrement contrôlées par du code JavaScript. Ce language s'est refait une beauté en juin 2015 : ECMAScript 6, alias JavaScript 2015.

## Syntaxe ES6

### Construction

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

### Object.assign()

```js
const obj = { full_name: 'Eric Priou' };
const copie = Object.assign({}, obj);
console.log(copie);
// output: { full_name: 'Eric Priou' }
```

### Class

```js

class Person {
    constructor(name) {
        this.name = name;
    }
}

let eric = new Person('Eric');
console.log(eric.name); // Output: Eric
```

### Accesseurs

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

### Array

Nouvelles méthodes ajoutées à Array :


##### Array.from()
```js
const example = Array.from("example");
console.log(example);
// output:  ["e", "x", "a", "m", "p", "l", "e"];
```

##### Array.of()
```js
const example = Array.of(1, 2, 3);
console.log(example);
// output: [1, 2, 3]
```

##### Array.prototype.keys() 
```js
const arr = ["a","b","c"];
const example = arr.keys(); 
console.log(example);
// output: [0, 1, 2]
```

##### Array.prototype.entries() 
```js
const arr = ["a","b","c"];
const exmple = arr.entries(); 
console.log(example);
// output: Array Iterator [[0, "a"], [1, "b"], [2, "c"]]
```

##### Array.prototype.find() 
```js
const arr = [{id:1, label:"hello"}, {id:2, name: "world"}]
const found = arr.find(item => item.id === 2)
const notfound = arr.find(item => item.id === 3)
console.log(found, notfound)
// output : {id:2, name: "worl"}, undefined
```

##### Array.prototype.fill() 
```js
const arr = Array(3).fill(1)
console.log(arr)
// output [1,1,1]
```

##### Array.prototype.copyWithin()
```js
const arr = ["hello","alice", "my", "name", "is" "bob"]
console.log(arr.copyWithin(1, 5)])
// output  "hello","bob", "my", "name", "is" "bob"]
```


### Methods

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