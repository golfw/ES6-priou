# Littéraux de gabarits/modèle (Template strings)


## Historique

Les chaînes de caractères ont été historiquement limité en terme de compatibilité. ES6 Template Strings à changé la façon de définir les caractères avec une meilleure :

1. Interpolation
2. Expressions imbriquées
3. Multilignes
4. Formatting
5. HTML echappé sécurisé


## Interpolation/substitution d'expressions

Historiquement, pour concaténer variables et chaînes de caractères, il était nécessaire de noter chacune des chaînes entre __guillements__ (simples `'` ou doubles `"`) et d'utiliser l'__opérateur de concaténation__ (`+`).

```javascript
const dog = {name : 'Milou', age : 8};
console.log(dog.name + " a " + (dog.age * 7) + " années humaines.");

/*
Milou a 56 années humaines.
*/
```

Avec l'arrivée d'ES6, il suffit d'utiliser les __accents graves__ (`` ` ``) en lieu et place des guillemets et de noter les expressions entre`${` et `}` comme suit :

```javascript
const dog = {name : 'Milou', age : 8};
console.log(`${dog.name} a ${dog.age * 7} années humaines.`);

/*
Milou a 56 années humaines.
*/
```



Permet aussi les calculs et opérations avec le placeholder : 
```javascript
    var age = 10
    var capitaine = 50
    console.log(`Age du capitaine : $(age+capitaine)`);
    // Age du capitaine : 60
    
    console.log(`Avec 2 capitaines : $(2*(age+capitaine)`);
    // Avec 2 capitaines : 120
```

Ils s'utilisent aussi dans les fonctions : 
```javascript
    function yo(){ return "--Flipidi flop Wesh 82--";}
    console.log(`La fonction old school : $(yo)} c'est sympa`;
```

Pour ajouter des accents graves dans votre placeholder : 
```javascript
    var coucou = `\`Yo\` tout le monde c'est Hetic `;
    // "`Yo` tout le monde c'est Hetic "
```  
### Gestion du multiligne

Plusieurs solutions existent pour faire du multilignes : 

- Antislash : 

```javascript
        var coucou = "Salut \ 
        tout le monde";
``` 
- Addition : 

      
        
```javascript
  var coucou = "Salut" + 
        " tout le monde";
```
        
- Retour à la ligne : 

     
        
```javascript
console.log(`Salut les héticiens et les
           héticiennes`);
```

## Multi-lignes

En ES5 et inférieur, il était nécessaire d'utiliser le __caractère d'échappement__ (`\`) en fin de ligne ou de __concaténer__ plusieurs chaînes pour qu'une variable soit multi-lignes. Autrement vous obtiendriez une erreur de syntaxe.

```javascript
//Avec caractère d'échappement "\"
const multi1 = "ligne 1 \n\
ligne 2 \n\
ligne 3";

//Avec opérateur de concaténation "+"
const multi2 = "ligne 1 \n" +
"ligne 2 \n" +
"ligne 3";
```

Tous les caractères de saut de ligne insérés dans la source font partie du littéral de gabarits. Ainsi, pour obtenir le même effet vous pouvez maintenant écrire :

```javascript
const multi = `ligne 1
ligne 2
ligne 3`;
```

Exemple d'utilisation :

```javascript
const dog = {name : 'Milou', age : 8};

const markup = `
<section>
    <h1>${name}</h1>
    <p>${age} ans</p>
</section>
`;

document.body.innerHTML = markup;

/*
<section>
    <h1>Milou</h1>
    <p>8 ans</p>
</section>
*/
```

## Imbrication

Il est possible d'imbriquer des templates afin d'avoir une syntaxe plus concise et moins verbeuse.

```javascript
const dogs = [
{name : 'Milou', age : 8},
{name : 'Rintintin', age : 12},
{name : 'Rex', age : 5}
];

const markup = `
<ul>
    ${dogs.map(dog => `
    <li>${dog.name} - ${dog.age * 7} années humaines (${dog.age})</li>
    `).join('')}
</ul>
`;

document.body.innerHTML = markup;

/*
<ul>
    <li>Milou - 56 années humaines (8)</li>
    <li>Rintintin - 84 années humaines (12)</li>
    <li>Rex - 35 années humaines (5)</li>
</ul>
*/
```

## Les littéraux de gabarits étiquetés (Tagged Template)

Un modèle étiqueté transforme un littéral de gabarits en plaçant un __nom de fonction au début__ de ce dernier. Par exemple :

```javascript
maFonction`Bonjour ${firstname} ${name}, vous semblez être en forme.`
```

La sémantique des littéraux étiquetés diffère de littéraux standards. Ils sont assimilables à un __appel de fonction__ particulier. Cette "fonction" aura pour __premier paramètre un tableau composé de chaînes de caractères__, ensuite tous les paramètres correspondant aux valeurs interpolées qui auront déjà été évaluées. Ainsi, le littéral étiqueté précédent pourrait se "décomposer" comme suit :

```javascript
maFonction(["Bonjour ", " ", ",vous semblez être en forme."], firstname, name);
```

Exemple :

```javascript
const dog = {name : 'Milou', age : 8};

const monEtiquette = (strings, ...values) => {
    let str = '';
    for(const [index, string] of strings.entries()){
        str += string + (values[index] || '');
    }
    return str;
}

const sortie = monEtiquette`${dog.name} a ${dog.age * 7} années humaines.`;

console.log(sortie);

/*
Milou a 56 années humaines.
*/
```

## Sources

* https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Litt%C3%A9raux_gabarits
* https://developers.google.com/web/updates/2015/01/ES6-Template-Strings
