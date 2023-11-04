# Kanvas Core JS
## Introduction
Welcome to the documentation for the Kanvas SDK, a TypeScript SDK designed exclusively to seamlessly connect with the Kanvas Niche ecosystem. This SDK is crafted to enhance the development of headless applications by providing easy-to-use interfaces for interacting with various modules within the Kanvas Niche ecosystem.

## Table of Contents

## Getting Started
### Prerequisites
You should have the KANVAS APP KEY to use Kanvas core, for get one, write to max@mctekk.com or you can run your own ecosystem cloning the repo from [Github](https://github.com/bakaphp/kanvas-ecosystem-api)
### Installation
To install the Kanvas SDK, simply run the following command in your project directory:
```bash
    npm i @kanvas/core
```
### Usage
```js
import  KanvasCore, {genericAuthMiddleware} from '@kanvas/core';
 function App() {
     ...
         const kanvas = new KanvasCore({
           url: 'https://graphapidev.kanvas.dev/graphql',
           key: '7d0488b2-632e-4045-9d2d-370d9161644a',
           middlewares: [genericAuthMiddleware(
             () => {
               return Promise.resolve(
                 localStorage.getItem("token")        
               )
             }
           )]
         });
     ...
 }
```

### Next Steps
Now that you have the SDK installed and configured, you can begin to use the SDK to interact with the Kanvas Niche ecosystem. the next step is to create a [user](./auth.md#sign-up)