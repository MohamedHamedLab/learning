# Organizing the Code Base
## components
- create the following folders:

1. **atoms**: These are the most basic components that we will ever write in our code base. Sometimes, they act as a **wrapper** for standard HTML elements such as button, input, and p, but we can also add **animations**, **color palettes**, and so on, to this category of components.
2. **molecules**: These are a small group of atoms combined to create slightly more complex structures with a minimum of utility. The **input** atom and the **label** atom together can be a straightforward example of what a molecule is.
3. **organisms**: Molecules and atoms combine to create complex structures, such as a registration **form**, a **footer**, and a **carousel**. 
4. **templates**: We can think of templates as the **skeleton** of our pages. Here, we decide where to put organisms, atoms, and molecules together to create the final page that the user will browse.
5. 
 ## utilities
```jsx
utilities/
  time.js
  localStorage.js
  jwt.js
  logs.js
```

## assets

```tsx
assets
 js
 css
 icons
 images
```

## lib
```jsx
lib/
    - graphql/
      - index.js
      - queries/
        - query1.js
        - query2.js
      - mutations/
        - mutation1.js
        - mutation2.js
```
