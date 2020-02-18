# Exchange format for morphisms in Monoidal Categories

> Date: 18-2-2020 <br>
> Status: *draft specification*

This document attempts to describe a interchange format for morphisms of monoidal categories.

## Example

Consider this string diagram.

![](example.png)

This could be represented as a term,

    f `compose` (h `tensor` g)

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
