# Kanvas Core JS

## User Module

This is a list of method available in the Kanvas Core JS SDK for User module.

## Methods

###

### Get User

The method `getUserData` allows you to get a user in the Kanvas ecosystem. this return type is [User](/types##UserData)

```js
let user = kanvas.users.getUserData();
```

### Update User

The method `updateUserData` allows you to update a user in the Kanvas ecosystem. this return type is [User](/types##UserData)

```js
    let user = kanvas.users.updateUserData(
        {
            id: number,
            updatedUser: UpdateUserParams
        }
    );
```

### Invite User

Use this method `invite` for invite users to company

```js
let user = kanvas.users.invite({
  inviteInput: InviteUserParams,
});
```

### Switch Company
This method `switchCompany` allows you to switch company in the Kanvas ecosystem.
```js   
let user = kanvas.users.switchCompany({
  id: number,
});
```


### Get Role By ID

The method `getRoleIdByName` allows you to get a role by name in the Kanvas ecosystem. this return type is [Role](/types##RoleData)

```js
    let role = kanvas.users.getRoleIdByName(
        name: string
    );
```
