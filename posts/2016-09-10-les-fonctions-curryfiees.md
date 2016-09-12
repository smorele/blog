---
title: Les fonctions curryfiées
---
La curryfication (ou currying pour les anglosaxons) n'est pas un principe propre à Haskell mais bel et bien à la programmation fonctionnelle.

Je laisse volontairement la définition de la curryfication en page de l'article, reprenons d'abord les choses dans l'ordre, depuis le début.

```
add x = 1 + x
```

La définition de cette première fonction est diablement simple. On prend un paramètre `x` et l'applique à 1.

La signature de cette fonction est:

```
add :: (Num a) :: a -> a
```

On lira cette signature comme ceci:  
La fonction `add` prend un paramètre a de type *Num* et retourne (la ->) un élement `a` de même type.
On peut tester cette fonction dans ghci:

```
prelude> add 1
2
prelude> add 5
6
prelude> add 100
101
```
> On se rappelle qu'avec Haskell, les paramètres sont séparés par des espaces

Modifions désormais notre fonction pour qu'elle prenne 2 paramètres et retourne leur somme:

```
add' x y = x + y
```

La signature de cette fonction sera alors:

```
add' :: (Num a) => a -> a -> a
```

Rien n'a vraiment changé dans la signaure si ce n'est l'ajout d'un nouveau paramètre. On lira alors: La fonction *add'* prend **2 paramètres** `a` de type *Num* et retourne un élément `a` de même type.  
De nouveau, on peut jouer un peu avec notre fonction:

```
prelude> add' 1 2
3
prelude> add' 2 4
6
prelude> add' 100 1
101
```

> On se rappelle qu'avec Haskell, les paramètres sont séparés par des espaces

Pour ceux qui ont suivi jusque la, je vais être franc avec vous, je vous raconte n'importe quoi depuis le début. Enfin presque !  
En fait, toutes **les fonctions Haskell ne prennent toujours qu'un seul et unique paramètre**. Comment est-ce possible ? Explications !

Je vous ai dit que les paramètres passés à une fonction sont séparés par un espace. Mettre un espace entre 2 choses revient à mettre en relation ces 2 choses, on dit alors que **l'espace joue le rôle d'un opérateur**. Donc si j'ai 2 paramètres séparés par 2 espaces, j'ai ... 2 fonctions.  
Les 2 appels suivants sont alors équivalents:

```
prelude> add' 3 4
7
prelude> (add' 3) 4
7
```
On peut définir la signature de la facon suivante:

```
add' :: (Num a) => a -> (a ->a)
```

On lira alors: La fonction `add'` prend un élément `a` de type *Num* et **retourne une fonction** qui prend un `a` et retourne un `a`.
Le contrat est donc remplit:  

* notre fonction prend **un unique paramètre** `a` et retourne une fonction  
* cette deuxieme fonction prend **un unique paramètre** `a` et retourne un `a`

On a parlé ici de 2 paramètres, mais les choses fonctionnent de la même facon si on ajoute de nouveaux paramètres. Par exemple la signature d'une fonction `add'' x y z = x + y + z` sera `add'' :: (Num a) => a ->(a->(a->a))` et se lira de la facon suivante: La fonction `add''` prend un paramètre `a` et retourne une fonction qui prend en paramètre un `a` et retourne une fonction qui prend un `a` et retourne un `a`.  

Vous l'aurez donc compris, la **curryfication** désigne la facon dont on découpe une fonction à **plusieurs paramètres** en une fonction à **paramètre unique** qui retourne une **fonction sur l'ensemble des paramètres restants**.

Toute la question maintenant c'est de savoir à quoi ca sert. Et bien toute la puissante de Haskell repose sur ce principe de fonctions qui prend ou qui retourne d'autres fonctions. On parle alors de **fonction d'ordre supérieure**.  
J'ai mis pas mal de temps à comprendre ce qu'est la curryfication, c'est pour cela que je vais m'arreter la pour le moment. Il faut bien prendre le temps de comprendre ce principe avant d'aller plus loin, on est ici sur des fondamentaux.