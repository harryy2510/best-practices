# 👁️ Style Guide

When we work with large projects, it's important that we remain consistent throughout the codebase and follow the best practices. To guarantee the quality of our codebase, we need to analyze different levels of the applications code.

## Clean Code

This is the most abstract level of code standardization. It's related to the implementations independent of the programming language. It will help the readability of our code.

[Clean Code Javascript](https://github.com/ryanmcdermott/clean-code-javascript)

### Naming

One of the most important points of the Clean Code is how we name our functions, variables, components, etc. Use this amazing guide to understand how to write better variable names.

[Naming Cheatsheet](https://github.com/kettanaito/naming-cheatsheet)

## Kebab Case For File And Folder Names

This is what Next.js uses by default. [Angular included it in its coding styleguide](https://angular.io/guide/styleguide#separate-file-names-with-dots-and-dashes).

Here is a great [article](https://profy.dev/article/react-folder-structure#kebab-case-for-file-and-folder-names) for the reason behind choosing kebab-case

- Instead of `MyComponent.tsx` write `my-component.tsx`.
- Instead of `useMyHook.ts` write `use-my-hook.ts`.

![image](https://media.graphassets.com/xAtfNqfsQbKdHZ19f6Bf)

## Named exports only

- Instead of `export default MyComponent` write `export { MyComponent }`.
- Instead of `export default useMyHook` write `export { useMyHook }`.

### Better DX

Default exports don’t export any name i.e. symbol that can be easily associated with an exported value. Named exports, on the other hand, are all about having a name (pretty obvious right 😂) . This makes possible for IDEs to find and import dependencies for us automatically, which is a huge productivity boost.

![image](https://miro.medium.com/max/1252/1*k7kSQJw1Pb-8DkyEhE-BHw.gif)

### Refactoring

Default exports make large-scale refactoring impossible since each importing site can name default import differently (including typos).

```javascript
// in file exports.js
export default function () {...}
// in file import1.js
import doSomething from "./exports.js"
// in file import2.js
import doSmth from "./exports.js"
```

On the contrary, named exports make such refactoring trivial.

### Better tree shaking

Sometimes we can be tempted to export one huge object with many properties as default export. This is an anti-pattern and prohibits proper tree shaking:

```javascript
// do not try this at home
export default {
  propertyA: 'A',
  propertyB: 'B',
};
// do this instead
export const propertyA = 'A';
export const propertyB = 'B';
```

Using named exports can reduce your bundle size when you don’t use all exported values (especially useful while building libs).

### Summary

Default exports were introduced mostly for easier interoperability with thousands CommonJS modules that were exporting single values like:

```javascript
module.exports = function() {...}
```

They don’t bring many benefits when used internally in our codebase, so please avoid them and thus make world a better place 😁
