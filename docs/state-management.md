# 🗃️ State Management

There is no need to keep all of our app state in a single centralized store. There are different needs for different types of state that can be split into several types:

## Component State

This is the state that only a component needs, and it is not meant to be shared anywhere else. But we can pass it as prop to children components if needed. Most of the time, we want to start from here and lift the state up if needed elsewhere. For this type of state, we will usually need:

- [useState](https://reactjs.org/docs/hooks-reference.html#usestate) - for simpler states that are independent
- [useReducer](https://reactjs.org/docs/hooks-reference.html#usereducer) - for more complex states where on a single action we want to update several pieces of state

[Component State Example Code](../src/components/master/splash-screen.tsx)

## Application State

This is the state that controls interactive parts of an application. Opening modals, notifications, changing color mode, etc. For best performance and maintainability, keep the state as close as possible to the components that are using it. Don't make everything global out of the box.

Application State Solution we are using:

- [zustand](https://github.com/pmndrs/zustand)

[UI State Example Code](../src/features/industry-insights/stores/index.ts)

## Form State

This is a state that tracks users inputs in a form.

Depending on the needs, they might be pretty complex with many fields which require validation.

Although it is possible to build any form using only React, there are pretty good solutions out there that help with handling forms. Here is what we are using:

- [React Hook Form](https://react-hook-form.com/)

We also integrate validation libraries with the mentioned solutions to validate inputs on the client. Here is what we are using:

- [yup](https://github.com/jquense/yup)

[Form And Validation Example Code](https://github.com/aicadium-products/sustainable-finance-ui/blob/b0f8bfd7dbae0bbb05565d9158daad93c1d6bf1f/src/pages/Login/components/LoginForm.tsx)
