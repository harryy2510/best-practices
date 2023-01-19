# 🚄 Performance

### Code Splitting

Code splitting is a technique of splitting production JavaScript into smaller files, thus allowing the application to be only partially downloaded. Any unused code will not be downloaded until it is required by the application.

Most of the time code splitting should be done on the routes level, but can also be used for other lazy loaded parts of application.

Do not code split everything as it might even worsen our application's performance.

[Code Splitting Example Code](../src/routes/index.tsx)

### Component and state optimizations

- Do not put everything in a single state. That might trigger unnecessary re-renders. Instead, split the global state into multiple stores according to where it is being used.

- Keep the state as close as possible to where it is being used. This will prevent re-rendering components that do not depend on the updated state.

- If we have a piece of state that is initialized by an expensive computation, use the state initializer function instead of executing it directly because the expensive function will be run only once as it is supposed to. e.g:

```javascript
// instead of this which would be executed on every re-render:
const [state, setState] = useState(myExpensiveFn());

// prefer this which is executed only once:
const [state, setState] = useState(() => myExpensiveFn());
```

### Web vitals

Since Google started taking web vitals in account when indexing websites, we should keep an eye on web vitals scores from [Lighthouse](https://web.dev/measure/) and [Pagespeed Insights](https://pagespeed.web.dev/).
