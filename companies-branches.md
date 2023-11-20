# Companies Branches Modules

## Methods

## Get Companies Branches

The method getCompanyBranches fetch all branches associates to the current company. It returns a [CompanyBranchInterface]() interface array.

```js
Kanvas.companies.getCompanyBranches(): CompanyBranchInterface[]
```

**Example:**

```js
const branches = Kanvas.companies.getCompanyBranches();
```

## Get Company Branches Users

The method getCompanyBranchUsers fetch all users associates to the current company branches. It returns a [UserData]() interface array.

```js
Kanvas.companies.getCompanyBranchUsers(): UserData[]
```

**Example:**

```js
const users = Kanvas.companies.getCompanyBranchUsers();
```

## Create Company Branch

The method createCompanyBranch is used to create a new company branch. It recieves a [CompanyBranchInput]() interface. It returns a [CompanyBranchInterface]() interface.

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

The method updateCompanyBranch is used to update a company branch. It recieves a [CompanyBranchInput]() interface and id of the company branch. It returns a [CompanyBranchInterface]() interface.

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
      url: "https://mynewcompanybranch.com",
      name: "My new company branch",
    },
  ],
});
```

## Delete Company Branch

The method deleteCompanyBranch is used to delete a company branch. It recieves the id of the company branch. It returns a boolean.

```js
Kanvas.companies.deleteCompanyBranch(id: string): boolean
```

**Example:**

```js
const deletedCompanyBranch = Kanvas.companies.deleteCompanyBranch(1);
```

## Add user to Company Branch

The method addUserToBranch is used to add a user to a company branch. It recieves the id of the user and the id of the company branch. It returns a boolean.

```js
Kanvas.companies.addUserToBranch(id: string, user_id: string): boolean
```

**Example:**

```js
const addedUserToBranch = Kanvas.companies.addUserToBranch(1, 1);
```

## Remove user from Company Branch

The method removeUserFromBranch is used to remove a user from a company branch. It recieves the id of the user and the id of the company branch. It returns a boolean.

```js
Kanvas.companies.removeUserFromBranch(id: string, user_id: string): boolean
```

**Example:**

```js
const removedUserFromBranch = Kanvas.companies.removeUserFromBranch(1, 1);
```
