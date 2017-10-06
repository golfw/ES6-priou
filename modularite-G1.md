# Modularité en Javascript

##Introduction :

### Définition d’une programmation modulaire:

Un module est un simple fichier JS, généralement une function ou un objet qui est exporté pour le rendre utilisable par d’autres ficiher JS. On dit qu’on exporte un module et qu’on importe un module.
Par convention, on limite un module par fichier.

La modularité __n’existe pas nativement__ dans le JavaScript.

La notion import et d’export a été intégré dans ES6. Pour cela, il faut s'aider de l'ibrairies externes.

###Quel est l'intérêt de la modularité ?

Pour comprendre les avantage de la modularité moderne, il faut d’abord revenir sur les méthodes utilisés auparavant. 

Avant l’arrivé des modules-bundler (Gulp, Webpack, Browserify ..), pour séparer son code JS en plusieur fichiers, il fallait les importer à la suite des balises \<script\> dans le fichier HTML.
Cela était fastidieux, de plus avec cette méthode, on était obligé de respecter un ordre défini car on devait respecter les dépendances entre les scripts. Aujourd’hui avec les utilisations des modules bundler on peut gérer les dépendances plus facilement dans un seul fichier JavaScript. 

Grâce aux modules bundler, les développeurs peuvent tester leur codes et déceler les erreurs de codes plus facilement.

Avec des modules, il est alors plus facile de partager son code. Vu qu’une fonction/module est réparti dans un fichier, les développeurs pourront trouver le module qui les intéressent sans devoir à en modifier une grande partie. 

La modularité facilite le travail open-source via des plateformes comme Github. Le fait de séparer son code en module, offre une structure beaucoup plus maintenable et agréable au quotidien pour le développeur.

Javascript ne supportant pas nativement les modules, la communauté s’est chargé de créer des solutions pour pallier à ce manque. Les deux standards les plus populaires sont :

* CommonJS : Implémenté dans Node.js et Browserify, il se caractérise par :
  * Un design adapté au chargement synchrone

Exemple de syntaxe CommonJS: 



```js
  var a = require('moduleA');
  var b = require('moduleB');
  // j'utilise a et b
  module.exports = maFonctionTresUtile;
```

* AMD (Asynchronous Module Definition) : Implémenté dans RequireJS, caractérisé par :

 * Une syntaxe légèrement plus complexe

 * Un design adapté au chargement asynchrone

Exemple de syntaxe AMD:

```js
define(['moduleA', 'moduleB'], function(a, b) {
 // j'utilise a et b
 return maFonctionTresUtile;
});
```

L’objectif d’ES6 est donc de combiner les avantages de ces deux standards

* Comme dans CommonJS, possède une syntaxe compacte et supporte les dépendances cycliques

* Comme dans AMD, supporte le fonctionnement asynchrone

ES6 possède aussi l’avantage d’être compatible avec CommonJS, ainsi, il est possible avec ES6 d’importer un module CommonJS sans risque.

* Partager ses modules avec la communauté :

### Node Package Manager (NPM): 

Travailler en module offre un autre avantage, et des moindre.

En effet, grâce à des “Package Manager” il est possible de rendre disponible à la communauté ses propres module (aussi appelés packages). 

Il est possible d’utiliser au sein de ses projets des modules développé et maintenue par d’autre développeur. 

Cela sans rien débourser, les joies du Open Source !

### Conclusion

Tant que les autres navigateurs n’intègrent pas la gestion de modules nativement, il faudra passer par ces solutions de model-builder.

Sources:

<https://ponyfoo.com/articles/es6-modules-in-depth>

<https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Instructions/import>

<http://2ality.com/2014/09/es6-modules-final.html>

<https://jakearchibald.com/2017/es-modules-in-browsers>



