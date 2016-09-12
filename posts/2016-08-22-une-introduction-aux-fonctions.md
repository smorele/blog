---
title: Une introduction aux fonctions
---

Parler des fonctions avec Haskell c'est comme de parler du pape pour l'église catholique, on est obligé vu que c'est la base. On a quand meme de la chance parce que les fonctions c'est vraiment pas compliqué à comprendre 

## Qu'est ce qu'une fonction 
Pour faire simple, une fonction c'est un bloc de code qui porte un nom, qui a potentiellement des paramètres et qui renvoit une valeur.  

Prenons un exemple simple et écrivons ce code dans un fichier qu'on appelera par exemple intro_fonction.hs
```haskell
direBonjour = "Bonjour toi"
```
On a donc définit une fonction qui s'appelle `direBonjour`, qui ne prend aucun paramètre et qui retourne `"Bonjour toi"`
Lancons désormais ghci pour tester notre fonction. Dans un terminal tapez la commande `ghci` depuis le repertoire qui contient votre fichier `intro_fonction.hs`. Une fois lancé tapez `:l intro_fonction` afin de charger notre script.

![fig1. Notre première fonction Haskell](/images/1.png)


Ajoutons désormais un paramètre à cette fonction, par exemple un prénom:
```haskell
direBonjour prenom = "Bonjour " ++ prenom
```

![fig2. Notre première fonction Haskell avec un paramètre](/images/2.png)

Pour les habitués des langages comme Python, Java, C, etc. on remarquera l'absence de parenthèses pour passer les paramètres. En fait avec Haskell, on separe les arguments par un simple espace, du coup le code est allégé, la syntaxe est plus claire.

