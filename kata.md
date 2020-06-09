
# KATA

Daily exercises ([kata](https://en.wikipedia.org/wiki/Kata)) of increasing difficulty. Purposefully, touching upon several concepts in Elm.  

They ought to be practised for at least a month, executed at least once every twenty four hours.  
  
Ichi, ni, san, shi, go, roku are Japanese numbers coresponding to one, two, three, four, five, and six.  
  
Happy practising!


## ICHI
Update a record.

```elm
samurai = 
    {id=0, weapon="katana"}
    |> (\s -> {s | weapon = "no-dachi"})  -- {id=0, weapon="no-dachi"}
```

## NI
List: find.

```elm
List.filter (\person -> person == "John") ["Mary", "Yousef", "John", "Mark"]  -- ["John"]
```

## SAN
List: insert.

```elm
{name="John"} :: [{name="Jane"}, {name="Larry"}]  -- [{name="John"}, {name="Jane"}, {name="Larry"}]
```

## SHI
List: update.

```elm
List.map 
    (\task -> 
        if task.id == 0 then
            {task | done = True}
        else
            task
    ) 
    [{id=0, done=False}, {id=1, done=False}, {id=2, done=False}]  
    -- [{id=0, done=True}, {id=1, done=False}, {id=2, done=False}]
```

## GO
List: remove.

```elm
List.filter 
    (\(_, maybeEntity) -> maybeEntity /= Nothing) 
    [(0, Just Entity "Adam"), (1, Just Entity "Lilith"), (2, Nothing)]  
    -- [(0, Just Entity "Adam"), (1, Just Entity "Lilith")]
```

## ROKU
Complex data.

```elm
type Langs = Elm | Elixir | Clojure | Haskell | Erlang | Lisp

data = { status = 200 , response = { data = { langs = [ { id = 0, name = Elm, year = 2012, creator = "Evan Czaplicki", inspiredBy = Haskell } , { id = 1, name = Elixir, year = 2011, creator = "José Valim", inspiredBy = Erlang } , { id = 2, name = Clojure, year = 2007, creator = "Rich Hickey", inspiredBy = Lisp } ] } } }

data 
|> .response 
|> .data 
|> .langs 
|> List.map (\{id, name, year, creator, inspiredBy} -> 
        let
            strFromLang lang = 
                case lang of
                    Elm -> "Elm"
                    Elixir -> "Elixir"
                    Clojure -> "Clojure"
                    Haskell -> "Haskell"
                    Erlang -> "Erlang"
                    Lisp -> "Lisp"
            idStr =
                case id of
                    0 -> "First"
                    1 -> "Second"
                    2 -> "Third"
                    _ -> ""
        in
        "The " ++ idStr ++ "functional language is " ++ strFromLang name ++ ". It was created in " ++ String.fromInt year ++ " year by " ++ creator ++ ". It is inspired by " ++ strFromLang inspiredBy ".\n "
    )
|> List.foldr (++) ""
|> String.trimRight

-- "The first functional language is Elm. It was created in 2012 year by Evan Czaplicki. It is inspired by Haskell.\n The second functional language is Elixir. It was created in 2011 year by José Valim. It is inspired by Erlang.\n The third functional language is Clojure. It was created in 2007 year by Rich Hickey. It is inspired by Lisp.\n"
```
