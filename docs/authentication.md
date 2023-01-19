# 🔐 Authentication

Authentication is a process of identifying if the user is logged in and who the user is. We rely on 3rd party authentication server to do all the hard work, [okta](https://okta.com). During logging in we receive a token that okta store in localstorage, and then on each authenticated request we send the token in the header along with the request.

#### Handling user data

User info is considered a global piece of state which should be available from anywhere in the application.

[Auth Configuration Example Code](../src/lib/auth.tsx)

[User Info Example Code](../src/components/master/user-popover.tsx)

The application will assume the user is authenticated if okta sdk has the state `isAuthenticated`.

[Authenticated Route Protection Example Code](../src/routes/index.tsx)
