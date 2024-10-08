# Kanvas SDK

Kanvas provides a robust set of GraphQL APIs designed to cover the essential features of headless applications:

- 🔐 **Authentication**: Easily manage user authentication.
- 🏢 **Multi-tenancy**: Seamlessly handle multiple tenants.
- 👥 **Customer Management (CRM)**: Manage customers, leads, and more.
- 📦 **Inventory Management**: Track and manage products and stock levels.
- 🤝 **Social Interactions**: Enable user interactions like follows, likes, and comments.
- 🔄 **Workflows**: Automate business processes with customizable workflows.

By taking care of these critical backend functionalities, Kanvas allows you to focus on building your app's unique business logic without reinventing the wheel.

## Getting Started

This guide covers the following steps:

1. Installing the Kanvas SDK
2. Setting up and configuring the SDK in your project
3. Basic examples of how to use the SDK

Let’s get started!


## Requirements

- **Node.js** version 12 or higher.
- **KANVAS APP KEY**: You need a Kanvas App Key to use the SDK. Currently, Kanvas is in closed beta. To join, sign up for our newsletter at [kanvas.dev](https://kanvas.dev).

Alternatively, you can run your own Kanvas ecosystem by cloning the [Kanvas Ecosystem API](https://github.com/bakaphp/kanvas-ecosystem-api) and following the provided setup instructions.


## Installation

To install the SDK in your project, run one of the following commands:

### NPM
```bash
npm install @kanvas/core --save
```

### Yarn
```bash
yarn add @kanvas/core
```


## Configuration

Once the SDK is installed, you'll need to configure it with your **GraphQL API URL** and **App Key**, which can be obtained from your Kanvas dashboard.

```js
import KanvasCore, { genericAuthMiddleware } from '@kanvas/core';

function App() {
  const Kanvas = new KanvasCore({
    url: '{{GRAPHQL_URL}}', // Your Kanvas GraphQL API URL
    key: '{{KEY}}', // Your Kanvas App Key
    middlewares: [
      genericAuthMiddleware(() => {
        return Promise.resolve(
          localStorage.getItem("token") // Token handling for authentication
        );
      }),
    ],
  });
}
```

### Super Admin
This is for when you want to access the Kanvas API as the super admin.

```js
import KanvasCore, { genericAuthMiddleware } from '@kanvas/core';

function App() {
  const Kanvas = new KanvasCore({
    url: '{{GRAPHQL_URL}}', // Your Kanvas GraphQL API URL
    key: '{{KEY}}', // Your Kanvas App Key
    adminKey: '{{ADMIN_KEY}}', // Your Kanvas Admin Key
    middlewares: [
      genericAuthMiddleware(() => {
        return Promise.resolve(
          localStorage.getItem("token")
        );
      }),
    ],
  });
}
```

This basic setup initializes the SDK and configures an authentication middleware to automatically attach a user token to API requests.

## Token Authentication vs. Super Admin API

When integrating with your application in Kanvas, it’s important to understand the difference between **Token Authentication** and **Super Admin API Access**:

### **Token Authentication** (Client API)

Client APIs and SDKs are designed for building user-facing applications, such as websites or mobile apps. With **Token Authentication**, users can only access the resources in **your app** that they have been granted permission to use, based on their roles and assigned permissions.

This ensures that users interact with your app in a secure and controlled way, with access limits defined by the application’s permissions structure.

### **Super Admin API** (Server API)

The **Super Admin API** is intended for backend or server-side integrations with **your app in Kanvas**, providing **full access** to all resources. Unlike Token Authentication, the Super Admin API **ignores user-specific permissions** and instead operates based on the API key’s scope, giving full administrative control over the app.

While the Super Admin API grants complete control over your app, it should **never be used on the frontend**. Its purpose is strictly for backend operations, and in the future, you’ll be able to scope API keys to allow more granular control over what parts of the app are accessible.


## Next Steps

Now that you've installed and configured the SDK, you're ready to start integrating Kanvas into your app. Head over to our [user management guide](./auth.md#sign-up) to learn how to authenticate users in your application.


## Table of Contents

1. [Authentication](./auth.md)
2. [Users](./users.md)
3. [Companies](./companies.md)
4. [Company Branches](./companies-branches.md)
5. [System Modules](./system-modules.md)
6. [Topics](./topics.md)
7. [Messages](./messages.md)
8. [Message Types](./messages-types.md)
