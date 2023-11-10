## User Module

This is a list of method available in the Kanvas Core JS SDK for User module.

## Methods

- [Get User Data](#get-user-data)
- [Update User](#update-user)
- [Invite User](#invite-user)
- [Switch Company](#switch-company)
- [Get by Role ID](#get-role-by-id)


## Get User Data

The method `getUserData` fetches data from the logged in user. It returns a [UserData](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/users.ts#L86) interface.

```js
Kanvas.users.getUserData(): UserData
```

**Example:**
```js
const userData = Kanvas.users.getUserData();
```

## Update User

The method `updateUserData` allows you to update a user in the Kanvas ecosystem. It recieves the user's ID and a [UpdateUserParams](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/users.ts#L121) interface. It returns a [UserData](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/users.ts#L86) interface.

```js
Kanvas.users.updateUserData(
  id: number,
  updatedUser: UpdateUserParams
): UserData
```

**Example:**
```js
const dataToUpdate = {
  'James',
  'Smith',
  'james.smith',
}

const updatedUserData = Kanvas.users.updateUserData(1, dataToUpdate);
```

## Invite User

The method `invite` is used to invite new users into a company. It recieves a [InviteUserParams](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/users.ts#L133) interface. It returns a [InviteUserData](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/users.ts#L141) interface.

```js
Kanvas.users.invite(inviteInput: InviteUserParams): InviteUserData
```

**Example:**
```js
const invitedUser = Kanvas.users.invite({
  'jane.doe@domain.com',
  'Jane',
  'Doe',
});
```

## Switch Company

The method `switchCompany` changes the company the user is currently in by passing the company id the user is moving to.

```js
Kanvas.users.switchCompany(id: number): void
```

**Example:**
```js   
Kanvas.users.switchCompany(2);
```


## Get Role By ID

The method `getRoleIdByName` allows you to get a role ID by name in the Kanvas Ecosystem. It returns a [RoleData](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/users.ts#L147) interface.

```js
Kanvas.users.getRoleIdByName(name: string): RoleData
```

**Example:**
```js
const roleData = Kanvas.users.getRoleIdByName('admin');
```
