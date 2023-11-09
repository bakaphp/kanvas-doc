## Authentication

This is a list of method available in the Kanvas Core JS SDK for the Authentication module.

## Methods

- [Register](#register)
- [Log In](#log-in)
- [Log Out](#log-out)
- [Forgot Password](#forgot-password)
- [Reset Password](#reset-password)
- [Change Password](#change-password)

## Register

The method `register` allows you to create a new user within the Kanvas Ecosystem. It recieves a [UserInterface](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/users.ts#L5) or [CreateUserParams](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/users.ts#L73) interface. It returns a [CreatedUser](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/users.ts#L82) interface.

```js
Kanvas.users.register(
  userData: UserInterface | CreateUserParams
): CreatedUser
```

**Example:**
```js
const createdUser = Kanvas.users.register({
  email: 'john.doe@domain.com',
  firstname: 'John',
  lastname: 'Doe',
  displayname: 'john.doe',
  password: 'pass1234',
  password_confirmation: 'pass1234',
});
```

## Log In

The method `login` allows you to sign in a user into the Kanvas Ecosystem. It returns a [Authentication](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/auth.ts#L1) interface.

```js
Kanvas.auth.login(
  email: string,
  password: string
): AuthenticationInterface
```

**Example:**
```js
const signIn = kanvas.auth.login(
  'john.doe@domain.com',
  'pass1234'
);
```

## Log Out

The method `logout` allows you to sign out a user out of the Kanvas Ecosystem. It returns a [Authentication](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/auth.ts#L11) interface.

```js
Kanvas.auth.logout(): void
```

**Example:**
```js
Kanvas.auth.logout();
```

## Forgot Password

The method `forgotPassword` sends an email that allows the user to reset the password of their account within the Kanvas Ecosystem.

```js
Kanvas.user.forgotPassword(email: string): void
```

**Example:**
```js
Kanvas.user.forgotPassword(
  'john.doe@domain.com'
);
```

## Reset Password

The method `resetPassword` allows you to reset the password of a user in the Kanvas Ecosystem. It recieves a hash, the user's new password and its verification. It returns a [ResetPasswordInterface](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/auth.ts#L19) interface.

```js
Kanvas.auth.resetPassword(
  hash_key: string,
  new_password: string,
  verify_password: string
): ResetPasswordInterface
```

**Example:**
```js
const resetPassword = kanvas.auth.resetPassword(
  '3b84ece51db2d36fb58608a48422601649093811',
  '1234pass',
  '1234pass'
);
```

## Change Password

The method `changePassword` allows you to change the password of a user in the Kanvas Ecosystem. It returns a [ChangePasswordInterface](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/auth.ts#L23) interface.

```js
Kanvas.auth.changePassword(
  current_password: string,
  new_password: string,
  new_password_confirmation: string
): ChangePasswordInterface
```

**Example:**
```js
const changePassword = kanvas.auth.changePassword(
  'pass1234',
  '1234pass',
  '1234pass'
);
```
