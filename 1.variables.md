Déclaration de variables
===================


<kbd>const</kbd> vous permet de déclarer une variable à assignation unique bindée lexicalement. Bon, ça fait un peu pompeux, alors pour les devs au fond de la salle à côté du radiateur, ça veut simplement dire que vous pouvez déclarer une variable qui ne contiendra qu'une valeur et qui sera scopée au niveau du bloc. Ce ne sont pas des vraies constantes au sens valeur de variable. Ce sont des constantes au niveau référence. C'est à dire que le contenu d'un tableau ou d'un objet déclaré avec <kbd>const</kbd> bloque la réassignation de la variable, mais ne rend pas la valeur immuable.



    function fn() {
      const foo = "bar"
      if (true) {
        const foo // SyntaxError, la variable a besoin d'être assignée
        const foo = "qux"
        foo = "norf" // SyntaxError, la variable ne peut pas être réassignée
        console.log(foo)
        // "qux", la variable appartient au scope de son bloc (le "if")
      }
      console.log(foo)
      // "bar", la variable appartient au scope de la fonction "fn"
    }

Le fonctionnement <kbd>const</kbd> peut être utilisé de manière cool dans le cas d'itérables :

    function fn() {
      const arr = [1, 2, 3]
      for (const el of arr) {
        console.log(el)
      }
    }

En effet, on pourrait croire qu'un <kbd>let</kbd> doit être utilisé ici, mais la déclaration est évaluée à chaque passage de l'itérateur, <kbd>const</kbd> est donc un meilleur choix !

let
---

<kbd>let</kbd> vous permet de faire pareil que <kbd>const</kbd> mais sans la contrainte d'assignation unique. Vous devriez donc instinctivement voir que les cas d'utilisation pour <kbd>let</kbd> sont les mêmes que ceux de <kbd>var</kbd>, son ancêtre. D'ailleurs, vous entendrez souvent : <kbd>let</kbd> est le nouveau <kbd>var</kbd>. C'est en partie vrai car il est capable de faire les mêmes choses, mais en mieux, car il a cette caractéristique d'être scopé au bloc courant.

    function fn() {
      let foo = "bar"
      var foo2 = "bar"
      if (true) {
        let foo // pas d'erreur, foo === undefined
        var foo2
        // Attention, les déclarations "var" ne sont pas scopées au niveau bloc
        // foo2 est en réalité écrasé !
        foo = "qux"
        foo2 = "qux"
        console.log(foo)
        // "qux", la variable appartient au scope de son blocs (le "if")
        console.log(foo2)
        // "qux"
      }
      console.log(foo)
      // "bar", la variable appartient au scope de son bloc (la fonction "fn")
      console.log(foo2)
      // "qux"
    }

Vous pouvez par exemple utiliser <kbd>let</kbd> pour vos boucles, la variable servant à l'itération est désormais scopée au niveau de cette boucle et n'entrera pas en conflit avec votre code autour. Plus de problème de <kbd>i</kbd> déjà pris !

    function fn2() {
      let i = 0
      for (let i=i; i<10; i++) {
        console.log(i)
      }
      console.log(i)
      // 0
    
      for (let j=i; j<10; j++) {}
      console.log(j)
      // j is not defined
    }
    fn2() // 0, 1, 2, 3, 4, 5, 6, 7, 8, 9

var
---

On a vu <kbd>const</kbd>, on a vu <kbd>let</kbd>. Avec ces deux nouveaux outils, il ne reste pas de grande place pour <kbd>var</kbd>. À mon avis, le seul cas d'utilisation valable pour <kbd>var</kbd> est lors de l'utilisation de <kbd>try</kbd>/<kbd>catch</kbd>, et ce n'est pas dans le cadre d'un bug, mais juste de syntaxe et de préférence (exemple).

----------