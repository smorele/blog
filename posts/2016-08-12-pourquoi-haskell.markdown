---
title: Pourquoi Haskell
---

Truc de Geek, de matheux ou de boutonneux honnêtement j'en ai aucune idée, je sais juste que ça commence à bien me plaire cette histoire.

Début 2016 je découvre [Elm](http://elm-lang.org/), un langage fonctionnel assez sexy pour faire du front. Dans l'idée ca compile du code Elm en Javascript, ça s'apprend vite, les perfs sont bonnes donc on continue. Je Google pas mal sur le sujet et je découvre ce qu'est un langage fonctionnel (et donc la programmation fonctionnelle). Quelle bêtise ! Depuis j'arrête pas, je regarde des vidéos, lis des tutos, des articles, du code ... Bref ca me passionne et on va en parler.


Donc pour faire simple, dans un langage fonctionnel, la fonction est la grande prêtresse ! On écrit tout à base de fonctions, on définit des fonctions, on passe ces fonctions en paramètre d'autres fonctions etc.


Et Haskell dans tout ca ? Bah Haskell est un langage fonctionnel mais en plus il est dit `pure`, c'est à dire que le code que l'on écrit n'aura pas d'effet de bord. Oui oui, vous avez bien lu. Le code d'une fonction, n'aura pas d'effet sur le reste de votre code. Ca donne envie non ? C'est quand meme un peu le Graal de tout développeur de vouloir limiter les bugs potentiels parce qu'on ne maîtrise pas assez la portée de ses fonctions. Avec Haskell on ne s'en préoccupe pas, on ne peut tout simplement pas écrire une fonction qui va pourrir le reste du code.
C'est à mon sens le plus gros avantage du langage mais il y en a d'autres:

- Le typage statique
- L'inférence de type: Haskell peut évaluer lui même les types
- La paresse: Haskell n’exécutera pas une fonction tant qu'il n'est pas obligé de nous retourner un résultat
- La beauté: Oué je sais c'est subjectif mais quand même


Et pour la fin un bout de code Haskell pour quand même voir à quoi ça ressemble
```haskell
putTodo :: (Int, String) -> IO ()
putTodo (n, todo) = putStrLn (show n ++ ": " ++ todo)

prompt :: [String] -> IO ()
prompt todos = do
    putStrLn ""
    putStrLn "Current TODO list:"
    mapM_ putTodo (zip [0..] todos)
    command <- getLine
    interpret command todos

interpret :: String -> [String] -> IO ()
interpret ('+':' ':todo) todos = prompt (todo:todos)
interpret ('-':' ':num ) todos =
    case delete (read num) todos of
        Nothing -> do
            putStrLn "No TODO entry matches the given number"
            prompt todos
        Just todos' -> prompt todos'
interpret  "q"           todos = return ()
interpret  command       todos = do
    putStrLn ("Invalid command: `" ++ command ++ "`")
    prompt todos

delete :: Int -> [a] -> Maybe [a]
delete 0 (_:as) = Just as
delete n (a:as) = do
    as' <- delete (n - 1) as
    return (a:as')
delete _  []    = Nothing

main = do
    putStrLn "Commands:"
    putStrLn "+ <String> - Add a TODO entry"
    putStrLn "- <Int>    - Delete the numbered entry"
    putStrLn "q          - Quit"
    prompt []

```
