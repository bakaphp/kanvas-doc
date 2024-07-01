# Users Module

The Users module in the Kanvas Core SDK provides comprehensive functionality for user management, including registration, profile updates, invitations, and role management.

## Key Features

- User registration
- Profile management
- User invitations
- Role assignment
- Social login integration
- Account deletion requests

## Usage

Access the Users module through the `users` property on your KanvasCore instance:

```typescript
const kanvas = new KanvasCore({...});
const users = kanvas.users;
```

## Core Methods

### register(userData: UserInterface | CreateUserParams): Promise<CreatedUser>

Registers a new user in the system.

```typescript
const newUser = await users.register({
  email: 'newuser@example.com',
  firstname: 'John',
  lastname: 'Doe',
  password: 'securePassword123',
  password_confirmation: 'securePassword123'
});
console.log(newUser.user.id); // New user ID
```

Returns a `CreatedUser` object containing user details and authentication tokens.

### getUserData(): Promise<UserData>

Retrieves the current user's data.

```typescript
const currentUser = await users.getUserData();
console.log(currentUser.displayname);
```

Returns a `UserData` object with comprehensive user information.

### updateUserData(id: number, updatedUser: UpdateUserParams): Promise<UserData>

Updates a user's profile information.

```typescript
const updatedUser = await users.updateUserData(123, {
  firstname: 'Jane',
  lastname: 'Smith',
  phone_number: '+1234567890'
});
console.log(updatedUser.displayname); // Jane Smith
```

Returns the updated `UserData` object.

## Invitation Methods

### invite(inviteInput: InviteParams): Promise<InviteData>

Sends an invitation to a new user.

```typescript
const invitation = await users.invite({
  email: 'invite@example.com',
  firstname: 'Invited',
  lastname: 'User',
  role_id: 2
});
console.log(invitation.invite_hash);
```

Returns `InviteData` containing the invitation details.

### getInvite(hash: string): Promise<InviteData>

Retrieves invitation details by hash.

```typescript
const inviteDetails = await users.getInvite('invitationHashHere');
console.log(inviteDetails.email);
```

### processInvite(input: InviteProcessParams): Promise<InviteProcessData>

Processes a user invitation, completing the registration.

```typescript
const processedInvite = await users.processInvite({
  invite_hash: 'invitationHashHere',
  firstname: 'John',
  lastname: 'Doe',
  password: 'newSecurePassword123'
});
console.log(processedInvite.token); // New user's access token
```

Returns `InviteProcessData` with authentication tokens.

## Role Management

### getRoleIdByName(name: string): Promise<RoleData>

Retrieves a role's ID by its name.

```typescript
const roleData = await users.getRoleIdByName('Admin');
console.log(roleData.roles.data[0].id);
```

### isAdmin(user: UserData): boolean

Checks if a user has admin privileges.

```typescript
const isUserAdmin = users.isAdmin(currentUser);
console.log(isUserAdmin); // true or false
```

## Other Functionality

### switchCompany(id: number): Promise<any>

Switches the user's active company.

```typescript
await users.switchCompany(456);
```

### socialLogin(input: SocialLoginParams): Promise<SocialLoginData>

Handles social media login.

```typescript
const socialLoginResult = await users.socialLoging({
  token: 'socialMediaTokenHere',
  provider: 'google'
});
console.log(socialLoginResult.token);
```

### requestDeletedAccount(): Promise<any>

Initiates an account deletion request.

```typescript
await users.requestDeletedAccount();
```

## Best Practices

1. Validate user input thoroughly before sending to the API.
2. Implement proper error handling for all user operations.
3. Use strong password policies for user registration and updates.
4. Limit the number of invitation attempts to prevent abuse.
5. Implement rate limiting for user-related operations.
6. Always use HTTPS for transmitting user data.
7. Regularly audit user roles and permissions.

## Troubleshooting

- **Registration Failures**: Check for existing email addresses or invalid input formats.
- **Invitation Issues**: Ensure the invitation hash is valid and not expired.
- **Role Assignment Problems**: Verify that the role exists and the user has permission to assign it.
- **Social Login Errors**: Confirm that the social media token is valid and not expired.

## Error Handling

Wrap all user operations in try/catch blocks for proper error handling:

```typescript
try {
  await users.updateUserData(userId, updatedData);
} catch (error) {
  console.error('Failed to update user:', error.message);
  // Handle error (e.g., show user feedback, log error)
}
```

Common error scenarios:
- Email already in use
- Invalid input data
- Unauthorized access
- Network failures

## Security Considerations

1. Implement multi-factor authentication for sensitive operations.
2. Regularly review and update user permissions.
3. Log all significant user actions for audit purposes.
4. Implement account lockout after multiple failed login attempts.
5. Use secure password reset mechanisms.

## Integration Tips

1. Combine with the Authentication module for a complete user management system.
2. Utilize custom fields for storing additional user information.
3. Implement webhook listeners for important user events (e.g., registration, role changes).
4. Use the filesystem module in conjunction with user updates for handling profile pictures.

## Advanced Usage

### Batch Invitations

For inviting multiple users efficiently:

```typescript
async function batchInvite(invites: InviteParams[]) {
  const results = await Promise.all(invites.map(invite => users.invite(invite)));
  return results.filter(result => result !== null);
}
```

### Custom User Flows

Implement custom registration flows by combining methods:

```typescript
async function customRegisterAndAssignRole(userData: CreateUserParams, roleName: string) {
  const newUser = await users.register(userData);
  const roleData = await users.getRoleIdByName(roleName);
  await users.updateUserData(newUser.user.id, { role_ids: [roleData.roles.data[0].id] });
  return newUser;
}
```

By leveraging the Users module effectively, you can create robust user management systems in your Kanvas-powered applications, handling everything from registration to complex role-based access control.
