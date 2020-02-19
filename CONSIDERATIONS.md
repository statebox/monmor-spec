# Considerations

## Combinators

The `terms[]` array should contain at least two terms.

If we have some combinator over a single term, it is as if the combinator is not there.

```json
{
	"type": "compose",
	"terms": [{
		"type": "generator",
		"outputTypes": ["b"],
		"name": "f",
		"inputTypes": ["a"]
	}]
}
```

A combinator over zero terms is essentially the unit.

**Q.** Should we disallow these two cases, so `terms[]` must have at least two entries? Or do we allow empty and singleton `term[]` arrays and have some algorithm to normalize this: remove singleton `term[]` combinators and replace empty combinators with `unit`?

