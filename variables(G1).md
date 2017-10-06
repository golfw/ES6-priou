# Nouvelles déclarations des variables

## var
On déclare une variable, éventuellement en initialisant sa valeur. Il permet de définir une variable globale ou locale à une fonction (sans distinction des blocs utilisés dans la fonction).


## let
On déclare une variable dont la portée est celle du bloc courant, éventuellement en initialisant sa valeur.

```javascript
function varTest() {
  var x = 31;
  if (true) {
    var x = 71;  // c'est la même variable !
    console.log(x);  // 71
  }
  console.log(x);  // 71
}

function letTest() {
  let x = 31;
  if (true) {
    let x = 71;  // c'est une variable différente
    console.log(x);  // 71
  }
  console.log(x);  // 31
}
```

## const
On déclare une constante nommée, dont **la portée est celle du bloc courant**, accessible en lecture seule. C’est aussi une **variable immuable**, c’est à dire que la variable ne peut pas être déclarée ou assignée de nouveau, cela concerne la variable et non son contenu assigné. 

Par exemple, si le contenu est un objet ou un tableau, le contenu peut être altéré. Généralement, par convention , les constantes sont en majuscules.

```javascript
// toute tentative de redéclaration renvoie une erreur
const MA_FAV = 20;

// le nom ma_fav est réservé par la constante ci-dessus cette déclaration échouera donc également
var MA_FAV = 20; 

// cela renvoie également une erreur 
let MA_FAV = 20;
// const fonctionne également avec les objets
const monObjet = {"clé": "valeur"};

// Écraser l'objet échouera comme précédemment
monObjet = {"autreClé": "valeur"};

// En revanche, les clés d'un objet ne sont pas protégés et on peut donc, de façon valide, avoir :
monObjet.clé = "autreValeur";
```

## Temporal Dead zone

La notion de **temporal dead zone** représente un endroit où nous ne pouvons pas accéder à une variable avant qu’elle soit définie.

```javascript
console.log(x); // renvoie une erreur bloquante
// la ‘temporal dead zone’ se situe ici
let x = 5; // n'est pas exécuté 
```

Dans le cas de `var`, nous pouvons y accéder même lorsqu’elle n’a pas été défini car on suppose que la variable a pu être créée avant mais on ne peut pas accéder à sa valeur actuelle. Ainsi, `var` avant sa déclaration, renvoie `undefined`. Donc ce n’est pas **erreur bloquante**.

En revanche, dans les cas de `let` ou de `const`, la variable qui n’est pas définie renvoie une erreur bloquante sous forme de `ReferenceError`.

```javascript
console.log(x); // renvoie undefined
var x = 5; // assigne 5 à x
console.log('oui'); // affiche oui

console.log(x); // renvoie une erreur bloquante
let x = 5; // n'est pas exécuté 
console.log('oui'); // n'est pas exécuté
```

## Sources
 - https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Instructions/const
 
 - https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Instructions/let
 
 - https://developer.mozilla.org/fr/docs/Web/JavaScript/Guide/Types_et_grammaire
 
 - http://es6-features.org/#Constants
