# ⚙️ Project Configuration

The application has been bootstrapped using `Vite` for simplicity reasons. It allows us to create applications quickly without dealing with a complex tooling setup such as bundling, transpiling etc.

Vite pre-bundles dependencies using `esbuild`. esbuild is written in `Go` and pre-bundles dependencies 10-100x faster than JavaScript-based bundlers.

[Vite Configuration Code](../vite.config.ts)

We should always configure and use the following tools:

#### ESLint

ESLint is a linting tool for JavaScript. By providing specific configuration defined in the`.eslintrc.json` file it prevents developers from making silly mistakes in their code and enforces consistency in the codebase.

We follow `airbnb` ESLint config.

[ESLint Configuration Code](../.eslintrc.json)

#### Prettier

This is a great tool for formatting code. It enforces a consistent code style across our entire codebase. By utilizing the "format on save" feature in our IDE we can automatically format the code based on the configuration provided in the `.prettierrc.json` file. It will also give us good feedback when something is wrong with the code. If the auto-format doesn't work, something is wrong with the code.

[Prettier Configuration Code](../.prettierrc.json)

#### TypeScript

ESLint is great for catching some bugs related to the language, but since JavaScript is a dynamic language ESLint cannot check data that run through the applications, which can lead to bugs, especially on larger projects. That is why TypeScript should be used. It is very useful during large refactors because it reports any issues we might miss otherwise. When refactoring, change the type declaration first, then fix all the TypeScript errors throughout the project, and we are done. One thing we should keep in mind is that TypeScript does not protect our application from failing during runtime, it only does type checking during build time, but it increases development confidence drastically anyway. Here is a [great resource on using TypeScript with React](https://react-typescript-cheatsheet.netlify.app/).

#### Husky

Husky is a tool for executing git hooks. Use Husky to run our code validations before every commit, thus making sure the code is in the best shape possible at any point of time and no faulty commits get into the repo. It can run linting, code formatting and type checking, etc. before it allows pushing the code. We can check how to configure it [here](https://typicode.github.io/husky/#/?id=usage).

[Husky Pre-Commit Configuration Code](../.husky/pre-commit)

#### Absolute imports

Absolute imports should always be configured and used because it makes it easier to move files around and avoid messy import paths such as `../../../Component`. Wherever we move the file, all the imports will remain intact. Here is how to configure it:

For TypeScript (`tsconfig.json`) projects:

```json
"compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
```

[Paths Configuration Code](../tsconfig.paths.json)

In this project we have to create another tsconfig file `tsconfig.paths.json` where we configure the paths and merge it with the base configuration.

**Note: We would also need to add path alias to our bundler config `vite.config.ts`:**

```javascript
resolve: {
    alias: {
        '@': path.resolve(__dirname, 'src'),
    },
},
```

It is also possible to define multiple paths for various folders(such as `@components`, `@hooks`, etc.), but using `@/*` works very well because it is short enough so there is no need to configure multiple paths, and it differs from other dependency modules so there is no confusion in what comes from `node_modules` and what is our source folder. That means that anything in the `src` folder can be accessed via `@`, e.g some file that lives in `src/components/MyComponent` can be accessed using `@/components/MyComponents`.
