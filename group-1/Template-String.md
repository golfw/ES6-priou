# 1/ String
Récapitulons ce que nous savons déjà au sujet des chaînes de caractères :

  - Une valeur de type chaîne (string) permet de représenter un texte.
  - En JavaScript, on définit une chaîne en plaçant un texte entre guillemets simples ('je suis une chaîne') ou entre guillemets doubles ("je suis une chaîne").
  - On peut insérer dans une chaîne certains caractères spéciaux en utilisant le caractère\ ("antislash" ou "backslash") suivi d'un autre caractère. Par exemple,\n définit un retour à la ligne.

```
"Ceci est une chaîne \n Sur plusieurs lignes"
```

```
"Ceci est une chaîne
Sur plusieurs lignes"
```

Source : [openclassrooms.com](https://openclassrooms.com/courses/apprenez-a-coder-avec-javascript/manipulez-les-chaines-de-caracteres)


# 2/ Concaténation de chaîne de caractère
Le terme "concaténer" signifie joindre deux chaînes bout à bout pour n'en former qu'une seule.
Source : [commentcamarche.net](http://www.commentcamarche.net/faq/16306-javascript-concatenation-de-chaines-de-caracteres)

Appliqué à des chaînes de caractères, l'opérateur "+" déclenche la concaténation (jointure) des deux valeurs.

```
"Bon"+"jour"
"Bonjour"
```

Voici un exemple de concaténation avec variable :
```
const name = "myName"
const myString = 'Je suis ' + name + ' !'
```

# 3/ Template string
ES2015 ajoute le support des template strings qui va permettre de se simplifier la vie lorsqu'on doit manipuler des chaînes de caractères.

Pour définir une chaîne en JavaScript, il faut utiliser soit des single quotes, soit des double quotes. Malheureusement ces délimiteurs posent quelques problèmes lorsque justement la chaîne contient un single quote ou une double quote.

Ainsi, les template strings utilisent le caractère back-tick pour délimiter les chaînes de caractères. On peut maintenant directement utiliser les variables dans une template string si on les insère dans un placeholder qui s'écrit ${variable}.

Source : [putaindecode.io](http://putaindecode.io/fr/articles/js/es2015/template-strings/)

Voici un exemple de concaténation avec variable en ES5 :
```
const name = "myName"
const myString = 'Je suis ' + name + ' !'
```

Voici un exemple de concaténation avec variable en ES6 :
```
const name = "myName"
const myString = 'Je suis ${myName} !'
```

# 4/ Template strings multi-lignes
Grâce à ES6 et aux templates string, nous pouvons bénéficier du support multi-lignes.

Ici nous écrivons un texte sur plusieurs lignes en ES5 :
```
const multiLignes = 'Salut, \n je \n suis \n Pedro'
```
Alors que grâce à ES6 et aux templates string nous pouvons écrire sur plusieurs lignes sans utiliser de "\n" :
```
const multiLignes = `Salut
je
suis
Pedro`
```

# 5/ Ternaire
Le code intégré dans les templates string est interprété. Nous pouvons donc y insérer des ternaires. 
```
const classe = ['Pedro', 'Carlos']
const finalText = Coucou ${classe.length > 1 ? 'tout le monde' : classe[0]} !
```

# 6/ Les regex dans les Templates String

Les regex (expressions régulières) sont une écriture compacte pour représenter un ensemble (peut-être infini) de séquences de caractères semblables.

Source : [http://edutechwiki.unige.ch](http://edutechwiki.unige.ch/fr/Expression_r%C3%A9guli%C3%A8re)
```
const email = 'email@domaine.com'
const emailRegex = /.+\@.+\..+/

const finalText = `Cet email est ${emailRegex.test(email) ? 'valide' : 'invalide'}`
```

# 7/ Les avantages des templates string

- L’interpolation est très utile au quotidien — elle facilite la lecture.
- Le code présent dans les Templates String est interprété ce qui nous permet d'y inclure des ternaires par exemple.
- Les Templates String supportent le multi-lignes.
- Le code est plus léger car les Templates String utilisent moins de caractères.

# 8/ L'inconvénient des templates string

- Les Templates String ne sont pas compatibles sur les navigateurs ne prenant pas en charge ES6. L'utilisation de Babel est vivement conseillée pour la compatibilité avec les anciens navigateurs.


### Participants

+ [Julien Da Silva](https://github.com/juliendasilva)
+ [Véronique Choquet](https://github.com/Henka-nk)
+ [Esther de Saint Blanquat](https://github.com/Taster9)