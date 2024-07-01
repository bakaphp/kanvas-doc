# Authentication Module

The Authentication module provides methods for handling user authentication and authorization in Kanvas applications.

## Key Features

- User login 
- Token refresh
- Password reset
- Password change
- Social login

## Usage

To use the Authentication module, access it via the `auth` property on your KanvasCore instance:

```typescript
const kanvas = new KanvasCore({...});
const auth = kanvas.auth;
```

## Methods

### login(email: string, password: string): Promise<AuthenticationInterface>

Authenticates a user with email and password.

```typescript
const authData = await auth.login('user@example.com', 'password123');
console.log(authData.token); // Access token
console.log(authData.refresh_token); // Refresh token
```

Returns an `AuthenticationInterface` object containing:
- `id`: User ID
- `token`: Access token  
- `refresh_token`: Refresh token
- `token_expires`: Access token expiration
- `refresh_token_expires`: Refresh token expiration
- `time`: Current time
- `timezone`: User timezone

### logout(): Promise<LogoutInterface>

Logs out the current user.

```typescript
await auth.logout();
```

Returns a `LogoutInterface` with a boolean indicating success.

### refreshToken(token: string): Promise<RefreshTokenInterface>

Refreshes an expired access token.

```typescript
const refreshedToken = await auth.refreshToken(currentRefreshToken);
console.log(refreshedToken.token); // New access token
```

Returns a `RefreshTokenInterface` containing the new access token.

### resetPassword(hash_key: string, new_password: string, verify_password: string): Promise<ResetPasswordInterface>

Resets a user's password.

```typescript
await auth.resetPassword('reset_hash', 'newPassword123', 'newPassword123');
```

Returns a `ResetPasswordInterface` with a boolean indicating success.

### changePassword(current_password: string, new_password: string, new_password_confirmation: string): Promise<ChangePasswordInterface>

Changes a user's password.

```typescript
await auth.changePassword('oldPass123', 'newPass456', 'newPass456');
```

Returns a `ChangePasswordInterface` with a boolean indicating success.

### socialLogin(data: SocialLoginInputInterface): Promise<AuthenticationInterface>

Authenticates a user via social login.

```typescript
const socialAuthData = await auth.socialLogin({
  token: 'social_token_123',
  provider: 'google'
});
console.log(socialAuthData.token); // Access token
```

Returns an `AuthenticationInterface` object similar to regular login.

## Best Practices

1. Store tokens securely, preferably in HTTP-only cookies.
2. Implement token refresh logic to maintain user sessions.
3. Use HTTPS for all authentication requests.
4. Validate user input before sending authentication requests.
5. Implement proper error handling for failed authentication attempts.

## Troubleshooting

- **Invalid Credentials**: Ensure email and password are correct. Check for typos or case sensitivity issues.
- **Token Expiration**: If operations fail due to invalid token, try refreshing the token first.
- **Network Errors**: Check internet connectivity and Kanvas API endpoint accessibility.
- **CORS Issues**: Ensure your application's domain is whitelisted in the Kanvas configuration.

## Error Handling

The Authentication module methods throw errors for various scenarios. Always wrap authentication calls in try/catch blocks:

```typescript
try {
  await auth.login(email, password);
} catch (error) {
  console.error('Authentication failed:', error.message);
  // Handle error (e.g., show user feedback, log error)
}
```

Common error scenarios:
- Invalid credentials
- Account locked
- Network failures
- Rate limiting

## Security Considerations

1. Never store plain text passwords.
2. Implement multi-factor authentication for enhanced security.
3. Use strong password policies.
4. Monitor for unusual authentication patterns to detect potential security breaches.
5. Regularly rotate refresh tokens.

## Integration Tips

1. Combine with the Users module for comprehensive user management.
2. Use the `genericAuthMiddleware` for automatic token handling in requests.
3. Implement a global auth state management for consistent UI updates.

By leveraging the Authentication module effectively, you can create secure and user-friendly authentication flows in your Kanvas-powered applications.
