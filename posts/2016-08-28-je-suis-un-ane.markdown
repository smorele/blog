---
title: Je suis un âne !
---

Sous ce titre volontairement provocateur se cache quand même une part de vérité. Dans un bout de code j'avais à comparer une valeur par rapport à deux autres, le truc con quoi mais pourtant j'ai eu une belle erreur que je n'attendais pas. Merci les habitudes.  
Illustrons le contexte avec un bout de code:
```haskell
getImc :: Float -> Float -> String
getImc size weight 
    | imc < 16 = "Anorexie"
    | 16.5 < imc 18.5 = "Maigreur"
    | 18.5 < imc < 25 = "normale"
    | 25 < imc < 30 = "surpoids"
    | 30 < imc < 35 = "obesite #1"
    | 35 < imc < 40 = "obesite #2"
    | imc > 40 = "obesite morbide"    
    where imc = weight / (size * size)
```  
Faisons abstractions des guardiens qui permettent de tester des conditions (les `|` en début de ligne) le problème ici ce sont les encadrements de la variable imc entre 2 valeurs comme par exemple `18.5 < imc < 25`  
Si on essaie de jouer avec cette fonction dans ghci par exemple, on aura l'erreur suivante:
```haskell
Precedence parsing error
        cannot mix ‘<’ [infix 4] and ‘<’ [infix 4] in the same infix expression
```

## Fonctions Infixes et fonctions prefixes
Avec Haskell, les fonctions sont majoritairement dites *préfixes*, c'est à dire que l'on place le nom de la fonction puis on y ajoute les paramètres séparés par des espaces.
Quelques exemples:
```haskell
succ 8 -- permet d'avoir l'élement suivant du paramètre
min 3 4 -- retourne le paramètre le plus petit
```

On peut aussi mettre les fonctions sous forme *infixe* c'est à dire séparer les arguments par le nom de la fonction. Pour cela, on entoure le nom de la fonction avec un accent grave. En reprenant notre fonction `min`, ca nous donne donc:
```haskell
3 `min` 4
```

Revenons donc à notre fonction `getImc`. Les plus malins d'entres vous auront peut-être trouvé le problème, les autres ouvrez ghci et tapez:
```haskell
:t (<)
```
Et oui, l'opérateur < est en fait une fonction qui prend deux éléments du même type `Ord` et qui retourne un `Bool`. Si on regarde comment `<` est utilisé dans le code, on voit clairement que :  

1. ca ne correspond pas du tout à la signature de la fonction
2. j'utilise un style infixe de la mauvaise facon puisque le nom de la fonction n'est pas entouré des accents. 

En somme, du grand n'importe quoi !  
C'est une erreur classique lorqu'on a l'habitude d'écrire du code dans un autre language comme Python, Java, PHP puisque cette syntaxe serait tout à fait acceptable.
Avec Haskell comme pour les autres languages fonctionnels, il ne faut pas oublier que les `<`, `>` sont des fonctions tout comme `+`, `-`, `*`  etc. En cas de doute, il ne faut donc pas hésiter à vérifier la signature des éléments avant de les utiliser.  
Pour clore ce sujet, voici comment corriger le problème. C'est une facon de faire, il y en a d'autres comme par exemple définir une fonction pour y tester les paramètres. 

```haskell
getImc :: Float -> Float -> String
getImc size weight 
    | imc < 16 = "Anorexie"
    | 16.5 < imc && imc < 18.5 = "Maigreur"
    | 18.5 < imc && imc < 25 = "normale"
    | 25 < imc && imc < 30 = "surpoids"
    | 30 < imc && imc < 35 = "obesite #1"
    | 35 < imc && imc < 40 = "obesite #2"
    | imc > 40 = "obesite morbide"    
    where imc = weight / (size * size)
```




