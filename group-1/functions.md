# Nouvelles déclaration des fonctions




## Sommaire


#### EcmaScript courant:

* Définition d’une fonction

* Les fonctions EcmaScript courantes

	
* Usage du this

* “Use Strict”	


#### Nouveautés ES6:
##### Les fonctions fléchées (Arrow Functions)

* Besoin	

* Syntaxes

* Spécificité du ```this```

##### Les paramètres par défaut 

* Problématique ES5

* Syntaxe

#### Liens:

___



# EcmaScript courant

	

## Définition d’une fonction 



Une fonction est une procédure/suite d’instruction jouant un rôle précis dans le code Javascript. Elles peuvent par exemple permettre de retourner une ou plusieurs valeur(s), selon ce qu’elle retourne et ses paramètres. 



Pour définir une fonction,  il suffit de commencer par le mot function.


##### Exemple: 
```

function carré(nombre) {

  return nombre * nombre;

};

```



## Les formes de fonctions courantes



### Fonctions courantes



Ce qu’on appelle l’expression de fonction et le fait de déclarer une fonction dans une variable. Afin d’avoir un code le plus propre possible, il faut donner un nom à la fonction en la déclarant dans la variable.


##### Exemple: 
```

var carré = function (nombre) { 

    return nombre * nombre 

};

```


Ou sinon, il suffit de commencer par  ```function``` puis le nom de la fonction.

##### Exemple: 

```
function carré(nombre) {
  return nombre * nombre;
};
```


### Les fonctions anonymes & IIFE



Les fonctions dites anonymes, sont des fonctions qui ne sont pas nommées, et donc, qui ne comportent pas de noms. Ce genre de fonctions est souvent utilisé pour les fonctions anonymes auto-instanciées ou IIFE pour Immediately Invoked Function Expression. Ce type de fonctions permet de ne pas prendre en compte les variables globales. Cette fonction est appelée tout de suite après la fermeture de celle-ci.


##### Exemple: 
```
function() {}   // Fonction anonymes

( function ( x, y ) {

    return x + y; // IIFE

} ) ( );

```



### Closures



Une closure est une fonction interne qui utilise les variables locales dans la fonction dans laquelle elle est imbriquée. La closure accepte trois portées de variables : il a accès à ses propres variables (entre ses accolades), aux variables de la fonction dans laquelle il est imbriqué, et les variables globales.


##### Exemple: 
```

function creerFonction() {

  var nom = "Mozilla";

  function afficheNom() {

    console.log(nom);

  }

  return afficheNom;

}



var maFonction = creerFonction();

maFonction();

```





### Usage du *this* 



Dans les trois cas d’usages du ```this``` en EcmaScript, au sein d’un objet et array, d’une classe ou d’une fonction, le contexte ne réagit pas pareil. Dans un objet ou un array, dans les classes, l’appel du ```this``` fais bien référence au contexte du bloc dans lequel il est préparé. Ce n’est pas le cas dans une fonction classique où le contexte va faire référence à l’objet global. 



De plus, on peut changer la portée du ```this``` avec la fonction apply() ou call(), ce qui peut représenter un risque de maintenabilité. Avec ECMAScript 3/5, ce problème a pu être résolu en affectant la valeur de ```this``` à une autre variable 


##### Exemple: 

```

function Personne() {

  var that = this; 

  that.age = 0;



  setInterval(function grandir() {

    // La fonction callback se réfère à la variable `that`

    // qui est le contexte souhaité

    that.age++;

  }, 1000);

}

```



Nous verrons qu’en ES6, cette problématique a été prise en compte.






### “Use Strict”





Pour répondre à un besoin de sécurité et d’optimisation des scripts. Il est possible en EcmaScript 5 de choisir une variante restrictive de JavaScript. Cette variante est invoquée en début de script de la sorte: 



"use strict";





Il permet de supprimer toutes les erreurs silencieuses, corrige les erreurs qui font qu'il est difficile pour les moteurs JavaScript d'effectuer des optimisations, et interdit les mot-clés susceptibles d'être définis dans les prochaines versions de ECMAScript.

Ceci implique entre autre pour les fonctions de savoir si les paramètres sont ajoutés plusieurs fois entre les parenthèses de la fonction. 

L’usage du ```this``` est notamment impacté par cette variante, il est impossible de faire référence à l'objet window du navigateur grâce à ```this``` au sein d'une fonction en mode strict.




___


# Nouveautés ES6:
## Les fonctions fléchées

	

Le but des fonctions fléchées ( Arrow function en anglais) est de résoudre les problèmes courants de l'expression fonctionnelle traditionnelle:



```
function myFunction(arguments) {
	// Le code que la fonction va devoir exécuter
}

```



L’un des objectifs de cette nouvelle fonction est de réduire la taille syntaxique de la déclaration de variable pour en simplifier sa lecture et son usage.



Mais un autre avantage réside en la gestion du ```this``` du scope courant, qui en ES5 n’est pas conservé à l'intérieur de la déclaration.



### Syntaxes



Cette nouvelle syntaxe intègre une simplification de la syntaxe en retirant le mot clé function et en généralisant l’usage du () pour définir une fonction. 



Ainsi, une fonction fléchée vide se déclare comme l’exemple ci-dessous, vide, elle retourne undefined:


##### Exemple: 
```
let empty = () => {};

```

 

Pour faire encore plus simple il est possible, dans le cas d’un seul paramètre et d’une expression simple de retirer les () et les {}, même dans le cas d’une expression de priorité inférieure, pour une multiplication dans cet exemple, :


##### Exemple: 
```
let identity = x => x;

let square = x => x * x;

```



Dans le cas cas ou l’on veut retourner un objet littéral, la présence des accolades {} ne permet pas directement de déclarer l’objet entre accolades {{key:value}} par soucis de lisibilité. Il est donc possible de mettre entre parenthèse le bloc d’expression pour retourner un objet littéral:


##### Exemple: 
```
let key_maker = x => ({key: x});

```



Dans le cas d’une fonctionne anonyme, la syntaxe reste la même: 



```
() => {
  // instructions
}

```



Et de même, si l’on veut faire une IIFE en ES6 avec une fonction fléchée c’est possible en appliquant la syntaxe et en ajoutant ():

##### Exemple: 

```
()=> {
  // instructions
}()
```

En outre, pour la fonction fléchée, il n’est plus nécessaire de spécifier un return la fonction va systématiquement retourner une valeur. 



### Traitement du *this*



La problématique de contexte du ```this``` dans une fonction fléchée a été gérée, le ```this``` va faire référence au contexte de déclaration de la fonction et non à l’objet global ( windows par exemple)

##### Exemple: 

```
const obj = {
  method: function () {
    return () => this;
  }
};

```



## Paramètres par défaut

	

L'absence de paramètres par défaut dans les version précédentes d’EcmaScript rendait la déclaration de fonctions plus verbeuse. L’avantage est d’éviter des structures de type ```if (typeof x === 'undefined') x = defaultValue```, grâce à l’usage de l’opérateur <kbd> = </kbd> directement dans les paramètres.


### Syntaxe



L’usage des paramètres par défaut permet d'initialiser des paramètres lors de l'appel de la fonction si aucune valeur n'est passée ou si c'est la valeur undefined qui est passée.

Cela permet de simplifier la syntaxe. 



Avant, avec ES5, nous devions vérifier que la valeur du paramètre n’était pas “undefined”, et lui affecter une valeur choisie le cas échéant.

Grâce aux paramètres par défaut qui existent depuis ECMAScript 6, on peut se passer de cette vérification et alléger le code de la fonction



##### Exemple avant ES6: 

```
function multiplier(a, b) {
  var b = (typeof b !== 'undefined') ? b : 1;
  return a * b;
}

```



##### Exemple ES6 : 

```
function multiplier(a, b = 1) {
  return a * b;
}

```



#### Différents cas possibles 



* Passer “Undefined” en paramètre : cela prendra automatiquement la valeur par défaut



* Les paramètres par défaut utilisés une fois, peuvent être utilisés.



```
function singulierAutoPluriel(singulier, pluriel = singulier+"s", message = pluriel + " BOOU :) !!!") {

  return [singulier, pluriel, rallyingCry ]; 
}

```



* Les fonctions définies dans le corps d'une fonction : Les paramètres par défaut sont exécutés en premier, les déclarations de fonctions présentes dans le corps de la fonction sont évaluées ensuite

* Paramètre par défaut et décomposition des paramètres



```
function f([x, y] = [1, 2], {z: z} = {z: 3}) {
  return x + y + z;
}

f(); // 6

```

___


# Liens:


Arguments ES6:

* [https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Fonctions/arguments](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Fonctions/arguments)

Fonctions Fléchées:

* [https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Fonctions/Fonctions_flechees documentation](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Fonctions/Fonctions_fl%C3%A9ch%C3%A9es documentation)


* [http://putaindecode.io/fr/articles/js/es2015/arrow-functions/](http://putaindecode.io/fr/articles/js/es2015/arrow-functions/)


* [http://tc39wiki.calculist.org/es6/arrow-functions/ ](http://tc39wiki.calculist.org/es6/arrow-functions/ )



Valeur par défaut:

* [https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Fonctions/Valeurs_par_d%C3%A9faut_des_arguments](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Fonctions/Valeurs_par_d%C3%A9faut_des_arguments)

Use strict:

* [https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Strict_mode](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Strict_mode)


Arrow Functions:

* [http://tc39wiki.calculist.org/es6/arrow-functions/](http://tc39wiki.calculist.org/es6/arrow-functions/)


-----
Participants:  [Lucille Delmas](https://github.com/lucilledelmas), [Wladimir Delenclos](https://github.com/wdelenclos), [Jérémy Bourel](https://github.com/JrBour)

