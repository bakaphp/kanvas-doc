# Getting Started

You need a KANVAS APP KEY to use Kanvas Core. To acquire one contact one of our developers at kanvas-support@mctekk.com. 

You could also run your own ecosystem by cloning the repository for [Kanvas Ecosystem API](https://github.com/bakaphp/kanvas-ecosystem-api).

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
```js
import  KanvasCore, { genericAuthMiddleware } from '@kanvas/core';

function App() {
  const Kanvas = new KanvasCore({
    url: 'https://graphapidev.kanvas.dev/graphql',
    key: '7d0488b2-632e-4045-9d2d-370d9161644a',
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
Now that you have the SDK installed and configured, you can begin to use it to interact with the Kanvas Niche Ecosystem. The next step is to [create a user](./auth.md#sign-up).