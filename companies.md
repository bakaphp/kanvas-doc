## Companies Module

This is a list of method available in the Kanvas Core JS SDK for Companies module.

## Methods

- [Get Companies](#get-companies)
- [Get Companies User](#get-companies-user)
- [Get Company Settings](#get-company-settings)
- [Create Company](#create-company)
- [Update Company](#update-company)
- [Delete Company](#delete-company)
- [Add User To Company](#add-user-to-company)
- [Remove User From Company](#remove-user-from-company)

## Get Companies

The method getCompanies fetch all companies associates to the user. It returns a [CompanyData]() interface.

```js
Kanvas.companies.getCompanies(): CompanyData
```

**Example:**

```js
const companies = Kanvas.companies.getCompanies();
```

## Get Companies User

The method getCompaniesUser fetch all users associates to the current company. It returns a [UserData](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/users.ts#L86) interface array.

```js
Kanvas.companies.getCompaniesUser(): UserData[]
```

**Example:**

```js
const users = Kanvas.companies.getCompaniesUser();
```

## Get Company Settings

The method getCompanySettings fetch all settings associates to the current company. It returns a [CompanySettings]()
interface.

```js
Kanvas.companies.getCompanySettings(): CompanySettings
```

**Example:**

```js
const settings = Kanvas.companies.getCompanySettings();
```

## Create Company

The method createCompany is used to create a new company. It recieves a [CompanyInput]() interface. It returns a [CompanyInterface]() interface.

```js
Kanvas.companies.createCompany(companyInput: CompanyInput): CompanyInterface
```

**Example:**

```js
const newCompany = Kanvas.companies.createCompany({
  name: "My new company",
  domain: "mynewcompany.com",
  website: "https://mynewcompany.com",
  address: "",
  zipcode: "",
  email: "",
  language: "",
  timezone: "",
  phone: "0000000000",
  country_code: "do",
  files: [],
});
```

## Update Company

The method updateCompany is used to update a company. It recieves a [CompanyInput]() interface and id of the company. It returns a [CompanyInterface]() interface.

```js
Kanvas.companies.updateCompany(id: string,companyInput: CompanyInput): CompanyInterface
```

**Example:**

```js
const updatedCompany = Kanvas.companies.updateCompany(1, {
  name: "My new company",
  domain: "mynewcompany.com",
  website: "https://mynewcompany.com",
  address: "",
  zipcode: "",
  email: "",
  language: "",
  timezone: "",
  phone: "0000000000",
  country_code: "do",
  files: [],
});
```

## Delete Company

The method deleteCompany is used to delete a company. It recieves the id of the company. It returns a boolean.

```js
Kanvas.companies.deleteCompany(id: string): boolean
```

**Example:**

```js
const deletedCompany = Kanvas.companies.deleteCompany(1);
```

## Add User To Company

The method addUserToCompany is used to add a user to a company. It recieves the id of the user and the id of the company. It returns a boolean.

```js
Kanvas.companies.addUserToCompany(id: string, user_id: string): boolean
```

**Example:**

```js
const addedUser = Kanvas.companies.addUserToCompany(1, 1);
```

## Remove User From Company

The method removeUserFromCompany is used to remove a user from a company. It recieves the id of the user and the id of the company. It returns a boolean.

```js
Kanvas.companies.removeUserFromCompany(id: string, user_id: string): boolean
```

**Example:**

```js
const removedUser = Kanvas.companies.removeUserFromCompany(1, 1);
```
