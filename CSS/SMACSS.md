# CSS and SASS Organisation with with SMACSS (Smacks)


SMACSS has the following 5 basic concepts.

1. Base
2. Layout
3. Modules
4. State
5. Themes


### Layout 

- Classes are used anywhere in the application. 
- Prefix these to avoid collissions.
- These are 'general-purpose' components and features to be used anywhere.

```
.pull-right
.pull-left
```

### Modules 

- These are reusable components
- Try to follow single-responsibility-principle

### State

- Use `is-` as a prefix to list state
- Use state to modify the behaviour or view of Layouts and Modules

```
.card.is-hovering
```

### Namespaces in Modules with BEM

- Namespacing helps in lowering CSS specificity. 
- Therefore 'flat' CSS rules are better than a long chain of nested elements.
- This is also better for performance.

- Use `__` for nested elements. (i.e. descendant) 
- Use `--` for a differant version of a module.

```
// instead of the following
.card .card-label

// use
.card__label
.card__label--reversed

```

The word before `__` element modifier is the namespace.

eg
```
// namespace is `card`
.card__label

// namespace is `card-items`
.card-items__label
```

### General Tips

- Use flat selectors whereever possible.
- Don't use #id selectors for CSS styling.
- If you have to nest, try to keep the nested level for 3 items.
- You can write scemantic classes without bootstrap (or another framework), and [replace it later](https://coderwall.com/p/wixovg/bootstrap-without-all-the-debt).
- Use SASS for all imports and better code organization.

#### References

- https://en.bem.info/
- https://coderwall.com/p/wixovg/bootstrap-without-all-the-debt
- https://www.youtube.com/watch?v=IKFq2cSbQ4Q
- https://www.youtube.com/watch?v=6co781JgoqQ
