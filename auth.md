# Kanvas Core JS

## Auth
This is a list of method available in the Kanvas Core JS SDK for Auth module.
## Methods

- [Sign Up](#sign-up)
- [Sign In](#sign-in)
- [Sign Out](#sign-out)
- [Forgot Password](#forgot-password)
- [Reset Password](#reset-password)
- [Change Password](#change-password)

### Sign Up

The method `register` allows you to create a new user in the Kanvas ecosystem. this return type is [CreatedUser](/types#CreatedUser)

```js
    let createdUser = kanvas.users.register({
        email: string;
        firstname: string;
        lastname: string;
        displayname: string;
        password: string;
        password_confirmation: string;
    });
```

### Sign In

The method `login` allows you to sign in a user in the Kanvas ecosystem. this return type is [Authentication](/types#AuthenticationInterface)

```js
    let signIn = kanvas.auth.login(
        email: string,
        password: string
    );
```

### Sign Out

The method `logout` allows you to sign out a user in the Kanvas ecosystem. this return type is [Authentication](/types#LogoutInterface)

```js
let signOut = kanvas.auth.logout();
```

### Forgot Password

The method `forgotPassword` allows you to send a email to reset the password of a user in the Kanvas ecosystem.

```js
    let forgotPassword = kanvas.user.forgotPassword(
        email: string
    );
```

### Reset Password

The method `resetPassword` allows you to reset the password of a user in the Kanvas ecosystem. This method return [ResetPasswordInterface
](/types##ResetPasswordInterface) type.

```js
    let resetPassword = kanvas.auth.resetPassword(
        hash_key: string,
        new_password: string,
        verify_password: string
    );
```

### Change Password

The method `changePassword` allows you to change the password of a user in the Kanvas ecosystem. This method return [ChangePasswordInterface
](/types##ChangePasswordInterface) type.

```js
    let changePassword = kanvas.auth.changePassword(
        current_password: string,
        new_password: string,
        new_password_confirmation: string
    );
```
