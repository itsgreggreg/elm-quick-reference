# Elm 0.18 Quick Reference
A quick reference for the Elixir programming Language and standard library.<br>
AKA Elm Cheat Sheet

Elm Website: http://elm-lang.org/<br>
Elm Api Documentation: http://package.elm-lang.org/packages/elm-lang/core/latest/<br>
Elm Core Source: https://github.com/elm-lang/core<br>
Try Elm Online: http://elm-lang.org/try<br>
Online Elm IDE: https://ellie-app.com/new<br>
This Document: https://github.com/itsgreggreg/elm_quick_reference/<br>

- [Basic Types](#basic_types)
 - [Float](#float)
 - [Int](#int)
 - [String](#string)
 - [Char](#char)
 - [Bool](#bool)
- [Collection Types](#collection_types)
 - [List](#list)
 - [Record](#record)
 - [Dict](#dict)
- [Modules](modules)
- [Functons](functions)
- [Type Signatures](#type_signatures)
- [Ports](#ports)
  - [inbound](#inbound)
  - [outbound](#outbound)

## Basic Types
### Float
 - Can be expressed literally as: `<digit(s)>.<digit(s)>[e<digit(s)>]`
 - Can have an optional exponent
```elm
> 1.5
-- 1.5 : Float
> 1.5e10
-- 15000000000 : Float
> .5
-- !! Syntax Error
```

### Int
 - Can be expressed literally as: `digit(s)`.
 - When input directly, are considered a `number` until used, meaning they can take the place of a `Float`
 - When returned from a function, are considered `Int`s and cannot take the place of a `Float`
```elm
> 5
-- 5 : number
> round(5)
-- 5 : Int
> 5 / 2
-- 2.5 : Float
> (round 5) / (round 2)
-- ! Type Mismatch, expecting Float, got Int
```

### String
 - UTF-16 encoded
 - Can be expressed literally as: `"<characters>"`
 - Can be multiline if surrounded in: `"""`
 - Can be pattern-matched on whole string only
 - Can be concatenated with `++`
 - Elm does not have string interpolation
 - Are not collections of characters


```elm
> "Hello"
-- "Hello" : String
> "☀★☂☻♞☯☭☢€→☎♫" ++ "♎⇧☮♻⌘⌛☘☊♔♕♖☦♠♣♥♦♂♀"
-- "☀★☂☻♞☯☭☢€→☎♫♎⇧☮♻⌘⌛☘☊♔♕♖☦♠♣♥♦♂♀" : String
> String.length "☀★☂☻♞☯☭☢€→☎♫♎⇧☮♻⌘⌛☘☊♔♕♖☦♠♣♥♦♂♀"
-- 30 : Int
```

#### Warnings :
 - Do not properly handle any Unicode characters that cannot be represented by a single UTF-16 code unit.
```elm
> String.length "hat: 🎩"
-- 7 : Int !! <- Should be 6
> String.toList "🎩"
-- ['�','�'] : List Char !! <- Should be ['🎩']
> String.reverse "🎩"
-- "��" : String !! <- Should be "🎩"
```

### Char
 - Can be expressed literally as: `'<character>'`
 - Can also be expressed as a hexidecimal Unicode code point like: `'\x<hex-digit(s)>'`
 - Are returned from String methods that work on single characters like `uncons` and `map`.

```elm
> 'M' == '\x4D'
-- True
> String.map Char.toUpper "hello"
-- "HELLO" : String
```

#### Warnings :
 - Do not properly handle any Unicode characters that cannot be represented by a single UTF-16 code unit.
```elm
> Char.toCode '🎩'
-- 55356 : Char.KeyCode !! <- Should be 127913
> Char.fromCode 55356 == '🎩'
-- True !! <- Should be false
```


### Bool
 - Can be expressed literally as: `True` or `False`

## Collection Types

### List
 - Are written literally as: `[]`, `[<element>,...]`
 - All elements must have the same type.
 - Are concatenated with `++`
 - Are cons'd with `::`
 - Can be pattern matched on whole list or cons'd parts
```elm
 > []
 -- [] : List a
 > [4] ++ [3.5]
 -- [4,3.5] : List Float
 > 4 :: 3.5 :: []
 -- [4, 3.5] : List Float
 > [1, "two"]
 -- !TYPE MISMATCH
```

### Record
 - Are written literally as: `{}`, `{key: value}`
 - Keys must be named the same way as [variables](#variables)
 - Values can be of any type
 - Can be pattern matched on type, individual keys, and exact values
 - Are updated with the syntax: `{ recordName | key = value}`
 - Keys cannot be programatically accessed or enumerated
```elm
> {}
-- {} : {}
> {one = "two"}
-- { one = "two" } : { one : String }
> a = {one = "two"}
> { a | one = "three"}
-- { one = "three" } : { one : String }
```

## Modules
 - Organize code into namespaces
 - Public functions must be specifically exported
```elm
module Math exposing (add)
 
{-| This is a public function,
it is exposed above -}
add : Int -> Int -> Int
add left right =
    left + right
   
{-| This is a private function,
it is not exposed. -}
subtract : Int -> Int -> Int
subtract left right =
    left - right
```

## Functions
### Named Functions
 - Can only be defined inside a module
 - Must always take the exact number of arguments specified
 - Arguments cannot have default values
 - May optionally (but strongly recomended) have a type signature
 - May have a docstyle comment above them
 - A function body can have only one expression
 - You may set up intermediate values in a `let` block then place your function body in an `in` block.
 ```elm
 -- inside some module
 
{-| This is a doc style comment for greet
-}
 greet : String -> String
 greet name =
     "Hello " ++ name ++ "!"
     
{-| fibonacci takes the number of fibonacci numbers
to generate
-}
fibonacci : Int -> List Int
fibonacci count =
    -- a "let" block defines intermediate functions
    let
        -- Intermediate functions may have type declarations
        sumOfFirstTwo : List Int -> Int
        sumOfFirstTwo =
            List.sum << List.take 2

        fibs count nums =
            if count <= 0 then
                nums
            else
                fibs (count - 1) (sumOfFirstTwo nums :: nums)
    -- an "in" block may contain only 1 expression
    in
    fibs (count - 2) [ 1, 1 ]
        |> List.take count
 ```
### Anonymous Functions
## Type Signatures


## Ports
__Ports__ are Elm's mechanism for interacting with Javascript. Any communication with Javascript must happen through a __port__
### Inbound

### Outbound
