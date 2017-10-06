
Template literals
===================

> **Note:**
> Documentation écrite dans le cadre du cours de JavaScript avancé.
> Par Laetitia Belail, Victor BM, Cyril Bécret


Les templates literaux sont apparus dans la norme EcmaScript2015 et permettent de déclarer des variables de type strings de manière plus puissante que la précédente notation.

Ils s'écrivent à l'aide de **back-ticks** contrairement aux strings originelles :
```
// ES5
var maStringES5 = "J'aime les strings de vieilles"
```
```
// ES6
const maStringES6 = `J'aime les strings de jeunes`
```


Syntax multilignes
-------------
Les templates littéraux simplifient l'écriture de strings sur plusieurs lignes. Alors qu'il fallait avant jouer avec la concaténation ou autres subterfuges pour gérer le multiligne, cette nouvelle syntax gère automatiquement le saut de ligne de manière transparente.
```
// ES5
var multilignesES5 = "Voici un saut\n" + "de ligne"
```
```
// ES6
const multilignesES6 = `Un autre saut
de ligne`
```


Tagged template literals
-------------
L'utilisation de variables ou calculs au milieu de strings pouvait être lourde à écrire en ES5 mais a été grandement facilité en ES6 grâce aux tagged templates. Ils s'utilisent en ajoutant une expression entre **${ }** qui sera interpolée avant d'être affichée.
```
// ES5
var operation = "addition"
var expressionES5 = "Voici une " + operation + " : " + 1+1 + " !"
```
```
// ES6
let operation = "addition"
const expressionES6 = `Voici une ${operation} : ${1+1} !`
```


Echappement
-------------
Cette forme de template permet d'utiliser des simples ou doubles quotes dans des strings et évite l'utilisation du backslash pour échapper ces caractères. En revanche cette mécanique est utilisée pour afficher des backticks : 
```
`\``
> '\'
```
De même, l'expression de ${ doit être échappé s'il n'est pas utilisé dans un tagged template :
```
`${`
> Syntax error
```
```
`\${`
> '${'
```


Saut de lignes
-------------
Les sauts de lignes sont standardisés en Line Feed (LF) dans les templates littéraux. La condition suivante vaut donc true en ES6 :
```
(`Saut
ligne` === 'Saut\nligne)
```

Sources
-------------
- https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Litt%C3%A9raux_gabarits
- https://developers.google.com/web/updates/2015/01/ES6-Template-Strings
- http://exploringjs.com/es6/ch_template-literals.html