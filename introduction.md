# Kanvas: Headless App APIs

Kanvas provides a comprehensive set of GraphQL APIs for common headless app requirements:

- Authentication
- Multi-tenancy management
- Customer management (CRM)
- Inventory management
- Social interactions
- Workflows

By handling these core functionalities, Kanvas allows you to focus on your app's unique business logic.

## Getting Started

This guide will walk you through:

1. Installing the Kanvas Core SDK
2. Configuring the SDK in your project
3. Basic usage examples

Let's begin!

## Requirements
Node 12 or higher.

## Installation
You need a KANVAS APP KEY to use Kanvas Core. At this moment kanvas is in a close beta if you want to try it out, signup to our newsletter at [kanvas.dev](https://kanvas.dev)

You could also run your own ecosystem by cloning the repository for [Kanvas Ecosystem API](https://github.com/bakaphp/kanvas-ecosystem-api) and following the installation instructions

## Installation
To install the SDK simply run the following command in your project directory:

### NPM
```bash
    npm instal @kanvas/core --save
```
or
```bash
    yarn add @kanvas/core
```

## Usage

The package needs your app key and ecosystem url . You can get both from your app dashboard.

```js
import  KanvasCore, { genericAuthMiddleware } from '@kanvas/core';

function App() {
  const Kanvas = new KanvasCore({
    url: '{{GRAPHQL_URL}}',
    key: '{{KEY}}',
    middlewares: [
      genericAuthMiddleware(() => {
        return Promise.resolve(
          localStorage.getItem("token")
        )
      }),
    ],
  });
 }
```

## Next Steps
Now that you have the SDK installed and configured, you can begin to use it to interact with the Kanvas Niche Ecosystem. The next step is to [user management](./auth.md#sign-up).