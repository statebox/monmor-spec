# Exchange format for morphisms in Monoidal Categories

> Date: 18-2-2020 <br>
> Status: *draft specification*

This document attempts to describe a interchange format for morphisms of monoidal categories.

## Motivation

Categories are algebraic structures that allow you to "compose" *maps* (also called *morphisms*).

A *map* is a thing with a certain *source* and *target* type (called *domain* and *co-domain*). This can be graphically depicted as a box with *input* and *output* wires.

![](map-f-ab.png)

Composing a map is only possible if the *target* of one map is the *source* of the other. Graphically:

![](map-compose.png)

*Monoidal* categories (also called *tensor categories*) are categories with a *tensor* composition operation. Graphically this amounts to putting boxes next to eachother.

![](tensor-1.png) 

Which itself can be interpreted as a box.

![](tensor-2.png)

There is *no meaning assigned to the boxes*! This is what makes monoidal categories a useful language to describe many different systems, all of them using the same base language of boxes and wires.

There are many different flavours of monoidal category: braided, symmetric, etc.

We don't attempt to capture each such category out there, but this draft specification is an attempt to address the most common of those.

## Terms


### Generator / Box 📦

A box has a *name* (can be any unicode string, also emoji's of course), *domain* and *codomain*.

![](generator.png)

```json
{
	"type": "generator",
	"outputTypes": ["c", "d", "e"],
	"name": "😎",
	"inputTypes": ["a", "b"]
}
```

### Spiders 🕷️

Spiders 

![](white-spider.png)


```json
{
	"typeParam": "α",
	"type": "spider",
	"outputs": 5,
	"name": "g",
	"inputs": 4,
	"color": "white"
}
```

### Cups/Caps 🏆/🧢

```json
{"typeParam":"α*","type":"cup","name":"("}
```

## Example

Consider this string diagram.

![](example.png)

This could be represented as a term,

    f ; (h * g)

(`;` is actually called "compose")

In this format, that would be represented as.

```json
{
	"type": "compose",
	"terms": [{
		"type": "generator",
		"outputTypes": ["b", "c"],
		"name": "f",
		"inputTypes": ["a"]
	}, {
		"type": "tensor",
		"terms": [{
			"type": "generator",
			"outputTypes": ["e"],
			"name": "h",
			"inputTypes": ["b"]
		}, {
			"type": "generator",
			"outputTypes": ["f"],
			"name": "g",
			"inputTypes": ["c"]
		}]
	}]
}
```

## Combinators

We have `compose` and `tensor`. Compose works in semicolon order.

The `terms[]` array should contain at least two terms.

## Syntax

```
root ::= term
term ::= unit | tensor | identity | compose | generator | permutation | spider | cup | cap

type ::= string

unit ::= 
  { "type": "unit"
  , "inputTypes": type[]
  , "outputTypes": type[] 
  }

tensor ::= 
  { "type": "tensor"
  , "terms": term[]
  , "inputTypes": type[]
  , "outputTypes": type[] 
  }

identity ::= 
  { "type": "identity"
  , "inputTypes": type[]
  , "outputTypes": type[] 
  }

compose ::= 
  { "type": "compose"
  , "terms": term[]
  , "inputTypes": type[]
  , "outputTypes": type[] 
  }

generator ::=
  { "type": "generator"
  , "name": string
  , "inputTypes": type[]
  , "outputTypes": type[] 
  }

permutation ::=
  { "type": "permutation"
  , "name": string,
  , "permutation": number[]
  , "inputTypes": type[]
  , "outputTypes": type[] 
  }

spider ::=
  { "type": "spider"
  , "name": string
  , "inputs": number
  , "outputs": number
  , "color": "white" | "black"
  , "typeParam": type
  , "inputTypes": type[]
  , "outputTypes": type[] 
  }

cup ::=
  { "type": "cup"
  , "name": string
  , "typeParam": type
  , "inputTypes": type[]
  , "outputTypes": type[] 
  }

cap ::=
  { "type": "cap"
  , "name": string
  , "typeParam": type
  , "inputTypes": type[]
  , "outputTypes": type[] 
  }
```
