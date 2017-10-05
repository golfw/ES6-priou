# La programmation Fonctionnelle

Le paradigme de la programmation fonctionnelle dans ES6 est associé au traitement de données dans les collections. Il permet de traiter les données sans effets de bords et sans perdre modifier la donnée. Tout cela grâce à différents concepts:
transparence référentielle,
fonctions d’ordre supérieur,
évaluation paresseuse, immuabilité.

### Transparence référentielle


Dans la programmation fonctionnelle, on veut éviter les effets de bords c’est pourquoi on discerne deux types de fonctions.

> Fonction impure

La fonction impure a des effets de bord observables qu'on ne peut pas deviner en regardant sa valeur de retour. Exemple :

```
 function diviserParDeux(nombre) {
		var missile = lancerUnMissileNucleaire();
		fairePorterLeChapeauAuDrManhattan(missile);
		return nombre / 2;
}
```

> Fonction pure

La fonction impure a des effets de bord observables qu'on ne peut pas deviner en regardant sa valeur de retour. Exemple :


```
function nukeSomeCity(nombre) {
    return nombre + 5;
}
```

### Fonctions d'ordre supérieur

En JS, les fonctions sont des objets de première classe (first-class citizen).
Une fonction d’ordre supérieur est une fonction qui possède au moins l'une des propriétés suivantes :
  * elle accepte au moins une autre fonction en paramètre
  * elle retourne une fonction en résultat.

Exemple :
```
	// Accepte une fonction en paramètre
	function appliquerDeuxFois(f, x) {
      return f(f(x));
  }

  function foisTrois(x) {
      return x * 3;
  }

  appliquerDeuxFois(foisTrois, 7);
  // --> (7 * 3) * 3 = 63
```

Concernant l'intérêt des fonctions d'ordre supérieur, il faut bien séparer les différentes tâches effectuées par nos fonctions ainsi qu'écrire des fonctions composables, modulables, paramétrables.

Exemple d'opération sur les tableaux en JS :

> Map

Map gère le parcours du tableau et nous gérons la transformation
```
var numbers = [1, 2, 3]

var newNumbers = numbers.map(function(number){
    return number * 2;
})

// newNumbers => [2, 4, 6]
```

> Filter


```
var numbers = [1, 2, 3, 4];

var newNumbers = numbers.filter(function(number){
    return (number % 2 !== 0);
}

// newNumbers => [1, 3]
```

> Reduce
```
var numbers = [1, 2, 3, 4];

var totalNumber = numbers.reduce(function(total, number){
    return total + number;
}, 0);

// totalNumbers => 10
```

### Évaluation paresseuse


### Immuabilité
