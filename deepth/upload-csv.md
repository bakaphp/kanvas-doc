# Upload CSV

- [Description](#description)
- [Requirements](#requirements)
- [Usage](#usage)
  - [Upload a CSV file](#upload-a-csv-file)
    - [Client-side (Browser)](#client-side-browser)
    - [Server-side (Node.js)](#server-side-nodejs)
    - [Next JS Server Actions](#next-js-server-actions)
  - [Mapper data](#mapper-data)
  - [Get all mappers](#get-all-mappers)
  - [Upload data](#upload-data)

## Description

This use case allows users to upload a CSV file to the server using filesystem api. Then the user can be do a mapper data and save it to database. This is a nice feature because it allows to user import data from the olds systems to the Ecosystem.

## Requirements

Same that the [Filesystem](), we must have a axios instance to upload file to the ecosystem via SDK. Next you can see a example of how to upload a file to the server.

```js
const {
  default: KanvasCore,
  genericAuthMiddleware,
  authAxiosMiddleware,
} = require("../dist");
const fs = require("node:fs");
const getKey = () => {
  return Promise.resolve("Token");
};
const interceptor = (config) => {
  config.headers["Authorization"] = `Bearer ${token}`;
  return config;
};
const kanvas = new KanvasCore({
  url: "https://graphapidev.kanvas.dev/graphql",
  key: "key",
  middlewares: [genericAuthMiddleware(getKey)],
  authAxiosMiddleware: interceptor,
});
```

## Usage

**Note: The following examples is using with fake data you must replace with your own data. 😊**

### Upload a CSV file

To upload a CSV file to the server, use the uploadFileCsv method from the filesystem module. This method can handle both File objects (in the browser) and Buffers (in Node.js).

### Client-side (Browser)

```javascript
const fileInput = document.getElementById("csvFileInput");
fileInput.addEventListener("change", async (event) => {
  const file = event.target.files[0];
  try {
    const result = await kanvas.filesystem.uploadFileCsv(file);
    console.log("Upload result:", result);
  } catch (error) {
    console.error("Upload error:", error);
  }
});
```

### Server-side (Node.js)

```javascript
const fs = require("fs").promises;
const path = require("path");

async function uploadCsvFromServer() {
  try {
    const filePath = path.join(__dirname, "path/to/your/file.csv");
    const file = fs.createReadStream(filePath);

    let buffer = Buffer.alloc(0);
    for await (const chunk of file) {
      buffer = Buffer.concat([buffer, chunk]);
    }

    const result = await kanvas.filesystem.uploadFileCsv(buffer);
    console.log("Upload result:", result);
  } catch (error) {
    console.error("Upload error:", error);
  }
}

uploadCsvFromServer();
```

### Next JS Server Actions

```typescript
app / page.tsx;
import { app } from "@/services/kanvas/init";
import FileInput from "./_file-input";

async function uploadFile(formData: FormData) {
  "use server";
  const file = formData.get("file") as File;
  const bytes = await file.arrayBuffer();
  const buffer = Buffer.from(bytes);
  if (!file) {
    throw new Error("No file provided");
  }

  const formDataToUpload = new FormData();
  formDataToUpload.append("file", file);

  try {
    const result = await app.filesystem.uploadFileCsv(buffer);
    console.log(result);
    return { success: true, data: result };
  } catch (error) {
    console.error("Upload failed:", error);
    return { success: false, error: "Upload failed" };
  }
}

export default function Home() {
  return (
    <main className='p-8'>
      <h1 className='text-2xl font-bold mb-4'>CSV File Uploader</h1>
      <form action={uploadFile}>
        <FileInput />
        <button
          type='submit'
          className='mt-4 bg-green-500 text-white px-4 py-2 rounded'
        >
          Upload
        </button>
      </form>
    </main>
  );
}

//_file-input.tsx

("use client");

import React, { useState } from "react";
import { useFormStatus } from "react-dom";

export default function FileInput() {
  const [fileName, setFileName] = useState<string | null>(null);
  const { pending } = useFormStatus();

  const handleFileChange = (event: React.ChangeEvent<HTMLInputElement>) => {
    const file = event.target.files?.[0];
    if (file) {
      setFileName(file.name);
    }
  };

  return (
    <div>
      <input
        type='file'
        onChange={handleFileChange}
        accept='.csv'
        name='file'
        style={{ display: "none" }}
        id='fileInput'
        disabled={pending}
      />
      <label
        htmlFor='fileInput'
        className={`cursor-pointer bg-blue-500 text-white px-4 py-2 rounded ${
          pending ? "opacity-50" : ""
        }`}
      >
        Select CSV File
      </label>
      {fileName && <p className='mt-2'>Selected file: {fileName}</p>}
    </div>
  );
}
```

You gonna receive a response like this

```json
{
  "filesystem_id": 107,
  "row": {
    "name": "Product A",
    "productSlug": "product-a",
    "description": "Feature 1, Feature 2",
    "sku": "A123",
    "slug": "product-a",
    "regionId": "US",
    "price": "100.0",
    "discountPrice": "90.0",
    "quantity": "10",
    "isPublished": "True",
    "files": "http://example.com/a",
    "productType": "Type 1",
    "warehouse": "388",
    "categories": "Style 1",
    "customFields": "[]",
    "attributes": "[]"
  },
  "header": [
    "name",
    "productSlug",
    "description",
    "sku",
    "slug",
    "regionId",
    "price",
    "discountPrice",
    "quantity",
    "isPublished",
    "files",
    "productType",
    "warehouse",
    "categories",
    "customFields",
    "attributes"
  ]
}
```

The header from your csv file and the first row of the file.

### Mapper data

Once you uploaded the csv , the user should be able to map the data with the columns from csv and the ecosystem fields. This is possible using the method `createFilesystemMapper` from `filesystemMapper` module.

The method received a object with the following properties:

- name: string;
- system_module_id: string;
- file_header: any;
- mapping: any;
- configuration: any;

For create a new mapper you can use the following code:

```js
kanvas.filesystemMapper.createFilesystemMapper({
  name: "Product Mapper",
  system_module_id: "107",
  file_header: [
    "name",
    "productSlug",
    "description",
    "sku",
    "slug",
    "regionId",
    "price",
    "discountPrice",
    "quantity",
    "isPublished",
    "files",
    "productType",
    "warehouse",
    "categories",
    "customFields",
    "attributes",
  ],
  mapping: {
    name: "name",
    productSlug: "productSlug",
    description: "description",
    sku: "sku",
    slug: "slug",
    regionId: "regionId",
    price: "price",
    discountPrice: "discountPrice",
    quantity: "quantity",
    isPublished: "isPublished",
    files: "files",
    productType: "productType",
    warehouse: "warehouse",
    categories: "categories",
    customFields: "customFields",
    attributes: "attributes",
  },
  configuration: {
    delimiter: ",",
    quote: '"',
    escape: "\\",
    skip_lines: 0,
    header: true,
  },
});
```

### Get all mappers

If you want to get all mappers you can use the method `getFilesystemMappers` from `filesystemMapper` module.

```js
const mappers = await kanvas.filesystemMapper.getFilesystemMapper();
```

### Upload data

For upload the data to the database you can use the method `filesystemImport` from `filesystemMapper` module. It received the object with the following properties:

- regions_id # The region id
- filesystem_mapper_id # The filesystem mapper id created in the previous step
- filesystem_id # The filesystem id created in the first step

```js
await kanvas.filesystemMapper.filesystemImport({
  regions_id: "ID",
  filesystem_mapper_id: "ID",
  filesystem_id: "ID",
});
```
