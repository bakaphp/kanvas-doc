# Companies Branches Modules

## Methods

## Get Companies Branches

The getCompanyBranches method retrieves all branches associated with the current company. It returns an array of [CompanyBranchInterface interfaces](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/companies-branches.ts#L21).

```js
Kanvas.companies.getCompanyBranches(): CompanyBranchInterface[]
```

**Example:**

```js
const branches = Kanvas.companies.getCompanyBranches();
```

## Get Company Branches Users

The getCompanyBranchUsers method fetches all users associated with the current company branches. It returns an array of [UserData interfaces](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/users.ts#L5).

```js
Kanvas.companies.getCompanyBranchUsers(): UserData[]
```

**Example:**

```js
const users = Kanvas.companies.getCompanyBranchUsers();
```

## Create Company Branch

The createCompanyBranch method is used to create a new company branch. It receives a [CompanyBranchInput interface](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/companies-branches.ts#L7). It returns a [CompanyBranchInterface interface](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/companies-branches.ts#L21).

```js
Kanvas.companies.createCompanyBranch(companyBranchInput: CompanyBranchInput): CompanyBranchInterface
```

**Example:**

```js
const newCompanyBranch = Kanvas.companies.createCompanyBranch({
  name: "My new company branch",
  companies_id: 1,
  is_default: false,
  website: "https://mynewcompanybranch.com",
  address: "",
  zipcode: "",
  email: "",
  country_code: "do",
  language: "es",
  timezone: "",
  phone: "0000000000",
  files: [
    {
      url: "https://mynewcompanybranch.com",
      name: "My new company branch",
    },
  ],
});
```

## Update Company Branch

The updateCompanyBranch method is used to update a company branch. It receives a [CompanyBranchInput interface](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/companies-branches.ts#L7) and the id of the company branch. It returns a [CompanyBranchInterface interface](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/companies-branches.ts#L21).

```js
Kanvas.companies.updateCompanyBranch(id: string,companyBranchInput: CompanyBranchInput): CompanyBranchInterface
```

**Example:**

```js
const updatedCompanyBranch = Kanvas.companies.updateCompanyBranch(1, {
  name: "My new company branch",
  companies_id: 1,
  is_default: false,
  website: "https://mynewcompanybranch.com",
  address: "",
  zipcode: "",
  email: "",
  country_code: "do",
  language: "es",
  timezone: "",
  phone: "0000000000",
  files: [
    {
      url: "https://mynewcompanybranch.com/image.jpg",
      name: "My new company branch",
    },
  ],
});
```

## Delete Company Branch

The deleteCompanyBranch method is used to delete a company branch. It receives the id of the company branch. It returns a boolean.


```js
Kanvas.companies.deleteCompanyBranch(id: string): boolean
```

**Example:**

```js
const deletedCompanyBranch = Kanvas.companies.deleteCompanyBranch(1);
```

## Add user to Company Branch

The addUserToBranch method is used to add a user to a company branch. It receives the id of the user and the id of the company branch. It returns a boolean.

```js
Kanvas.companies.addUserToBranch(id: string, user_id: string): boolean
```

**Example:**

```js
const addedUserToBranch = Kanvas.companies.addUserToBranch(1, 1);
```

## Remove user from Company Branch

The removeUserFromBranch method is used to remove a user from a company branch. It receives the id of the user and the id of the company branch. It returns a boolean.

```js
Kanvas.companies.removeUserFromBranch(id: string, user_id: string): boolean
```

**Example:**

```js
const removedUserFromBranch = Kanvas.companies.removeUserFromBranch(1, 1);
```
