# Companies Module

The Companies module in the Kanvas Core SDK provides comprehensive functionality for managing company data, users, and settings within the Kanvas ecosystem.

## Key Features

- Company CRUD operations
- User management within companies
- Company settings management
- Branch management
- Pagination and filtering support

## Usage

Access the Companies module through the `companies` property on your KanvasCore instance:

```typescript
const kanvas = new KanvasCore({...});
const companies = kanvas.companies;
```

## Core Methods

### getCompanies(options?: CompanyQueryOptions): Promise<CreatedCompanies>

Retrieves a list of companies with optional filtering, pagination, and sorting.

```typescript
const companiesData = await companies.getCompanies({
  first: 10,
  page: 1,
  where: { column: 'NAME', operator: 'LIKE', value: '%Tech%' },
  orderBy: [{ column: 'CREATED_AT', order: 'DESC' }],
  search: 'Software'
});
console.log(companiesData.companies.data);
```

Returns a `CreatedCompanies` object containing an array of company data and pagination info.

### createCompany(input: CompanyInput): Promise<CompanyInterface>

Creates a new company.

```typescript
const newCompany = await companies.createCompany({
  name: 'New Tech Inc',
  website: 'https://newtechinc.com',
  email: 'contact@newtechinc.com',
  country_code: 'US'
});
console.log(newCompany.id);
```

Returns a `CompanyInterface` object with the created company's details.

### updateCompany({ id, input }: InputCompanyParams): Promise<CompanyInterface>

Updates an existing company's information.

```typescript
const updatedCompany = await companies.updateCompany({
  id: '123',
  input: {
    name: 'Updated Tech Inc',
    phone: '+1234567890'
  }
});
console.log(updatedCompany.name);
```

Returns the updated `CompanyInterface` object.

### deleteCompany(id: string): Promise<Boolean>

Deletes a company by its ID.

```typescript
const isDeleted = await companies.deleteCompany('123');
console.log(isDeleted); // true if successful
```

## User Management Methods

### getCompanyUsers(options?: CompanyUserQueryOptions): Promise<CreatedCompanyUsers>

Retrieves users associated with a company.

```typescript
const companyUsers = await companies.getCompanyUsers({
  first: 20,
  page: 1,
  where: { column: 'COMPANIES_ID', operator: 'EQ', value: '123' }
});
console.log(companyUsers.companyUsers.data);
```

Returns a `CreatedCompanyUsers` object with user data and pagination info.

### addUserToCompany(options: { id: string, user_id: string, rol_id?: string }): Promise<Boolean>

Adds a user to a company, optionally assigning a role.

```typescript
const added = await companies.addUserToCompany({
  id: '123', // company ID
  user_id: '456',
  rol_id: '789' // optional
});
console.log(added); // true if successful
```

### removeUserFromCompany(id: string, user_id: string): Promise<Boolean>

Removes a user from a company.

```typescript
const removed = await companies.removeUserFromCompany('123', '456');
console.log(removed); // true if successful
```

## Company Settings

### getCompanySettings(): Promise<CompanySettings>

Retrieves the settings for the current company.

```typescript
const settings = await companies.getCompanySettings();
console.log(settings.settings);
```

Returns a `CompanySettings` object containing company-specific configurations.

## Best Practices

1. Use pagination when fetching large sets of companies or users to optimize performance.
2. Implement proper error handling for all company operations.
3. Validate input data before sending requests to create or update companies.
4. Use meaningful search terms and filters to narrow down company queries.
5. Regularly audit company user lists and remove unnecessary access.
6. Implement role-based access control when adding users to companies.

## Troubleshooting

- **Company Creation Failures**: Ensure all required fields are provided and valid.
- **User Assignment Issues**: Verify that the user and company IDs exist and are correct.
- **Query Performance**: Use appropriate filters and pagination to optimize large queries.
- **Permission Errors**: Ensure the authenticated user has the necessary permissions for company operations.

## Error Handling

Implement try/catch blocks for all company operations:

```typescript
try {
  await companies.updateCompany({ id: '123', input: updatedData });
} catch (error) {
  console.error('Failed to update company:', error.message);
  // Handle error (e.g., show user feedback, log error)
}
```

Common error scenarios:
- Company not found
- Duplicate company name
- Insufficient permissions
- Invalid input data

## Security Considerations

1. Implement strict access controls for company management operations.
2. Regularly audit company membership and remove unnecessary access.
3. Use encrypted connections (HTTPS) for all company-related operations.
4. Implement logging for sensitive company operations for audit trails.
5. Validate and sanitize all input data to prevent injection attacks.

## Integration Tips

1. Combine with the Users module for comprehensive user-company relationship management.
2. Utilize the Roles module to manage role-based access within companies.
3. Integrate with the Filesystem module for handling company logos and documents.
4. Use webhooks to sync company data with external systems.

## Advanced Usage

### Batch Company Operations

For efficient bulk operations:

```typescript
async function batchUpdateCompanies(updates: InputCompanyParams[]) {
  return Promise.all(updates.map(update => companies.updateCompany(update)));
}
```

### Company Data Analysis

Implement company data analysis using aggregated queries:

```typescript
async function analyzeCompanyGrowth(companyId: string, timeRange: { start: Date, end: Date }) {
  const usersOverTime = await companies.getCompanyUsers({
    where: { 
      column: 'COMPANIES_ID', 
      operator: 'EQ', 
      value: companyId,
      AND: [
        { column: 'CREATED_AT', operator: 'GTE', value: timeRange.start.toISOString() },
        { column: 'CREATED_AT', operator: 'LTE', value: timeRange.end.toISOString() }
      ]
    },
    orderBy: [{ column: 'CREATED_AT', order: 'ASC' }]
  });
  
  // Analyze user growth over time
  return usersOverTime.companyUsers.data.reduce((acc, user, index) => {
    acc.push({ date: user.created_at, totalUsers: index + 1 });
    return acc;
  }, []);
}
```

### Custom Company Hierarchies

Implement custom company hierarchy structures:

```typescript
async function createCompanyHierarchy(parentCompanyId: string, subsidiaries: CompanyInput[]) {
  const parentCompany = await companies.getCompanies({ 
    where: { column: 'ID', operator: 'EQ', value: parentCompanyId }
  });
  
  const createdSubsidiaries = await Promise.all(subsidiaries.map(sub => 
    companies.createCompany({ ...sub, parent_company_id: parentCompanyId })
  ));
  
  return { parent: parentCompany, subsidiaries: createdSubsidiaries };
}
```

By effectively utilizing the Companies module, you can build sophisticated company management systems within your Kanvas-powered applications, handling everything from basic CRUD operations to complex hierarchical structures and user management.
