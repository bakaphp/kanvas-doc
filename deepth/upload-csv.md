# Upload CSV

- [Description](#description)
- [Requirements](#requirements)
- [Usage](#usage)
  - [Upload a CSV file](#upload-a-csv-file)
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

To upload a CSV file to the server, you can use the `uploadFileCsv` method from the `filesystem` module. This method receives the file path and the file name as parameters.

```js
   await filesystem = kanvas.filesystem.uploadFileCsv('path/to/file.csv');
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
        name: 'Product Mapper',
        system_module_id: '107',
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
            "attributes"
        ],
        mapping: {
            "name": "name",
            "productSlug": "productSlug",
            "description": "description",
            "sku": "sku",
            "slug": "slug",
            "regionId": "regionId",
            "price": "price",
            "discountPrice": "discountPrice",
            "quantity": "quantity",
            "isPublished": "isPublished",
            "files": "files",
            "productType": "productType",
            "warehouse": "warehouse",
            "categories": "categories",
            "customFields": "customFields",
            "attributes": "attributes"
        },
        configuration: {
            "delimiter": ",",
            "quote": "\"",
            "escape": "\\",
            "skip_lines": 0,
            "header": true
        }
    })
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
        regions_id: 'ID',
        filesystem_mapper_id: 'ID',
        filesystem_id: 'ID'
    });
```