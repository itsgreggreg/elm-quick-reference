# Elm 0.18 Quick Reference
A quick reference for the Elixir programming Language and standard library.<br>
AKA Elm Cheat Sheet

Elm Website: http://elm-lang.org/<br>
Elm Api Documentation: http://package.elm-lang.org/packages/elm-lang/core/latest/<br>
Elm Core Source: https://github.com/elm-lang/core<br>
Try Elm Online: http://elm-lang.org/try<br>
Online Elm IDE: https://ellie-app.com/new
This Document: https://github.com/itsgreggreg/elm_quick_reference/<br>

- [Basic Types](#basic_types)
- [Collection Types](#collection_types)
- [Ports](#ports)
  - [inbound](#inbound)
  - [outbound](#outbound)

## Basic Types
### Float
 - Must follow the format of `digit(s)`-`decimal`-`digit(s)`
 - Can have an exponent
```elm
> 1.5
1.5 : Float
> 1.5e10
15000000000 : Float
> .5
! Syntax Error
```

### Int
 - Must follow the format of `digit(s)`.
 - When input directly, are considered a `number` until used, meaning they can take the place of a `Float`
 - When returned from a function, are considered `Int`s and cannot take the place of a `Float`
```elm
> 5
5 : number
> round(5)
5 : Int
> 5 / 2
2.5 : Float
> (round 5) / (round 2)
! Type Mismatch, expecting Float, got Int
```


## Collection Types


## Ports
__Ports__ are Elm's mechanism for interacting with Javascript. Any communication with Javascript must happen through a __port__
### Inbound

### Outbound
