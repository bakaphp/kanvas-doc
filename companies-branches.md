# Companies Branches Module

The Companies Branches module in the Kanvas Core SDK provides comprehensive functionality for managing company branches, including creation, updates, deletion, and user association within the Kanvas ecosystem.

## Key Features

- Branch CRUD operations
- User management within branches
- Pagination and filtering support for branch queries
- Branch-specific user queries

## Usage

Access the Companies Branches module through the `companiesBranches` property on your KanvasCore instance:

```typescript
const kanvas = new KanvasCore({...});
const branches = kanvas.companiesBranches;
```

## Core Methods

### getCompanyBranches(options?: BranchQueryOptions): Promise<CompanyBranchInterface>

Retrieves a list of company branches with optional filtering, pagination, and sorting.

```typescript
const branchesData = await branches.getCompanyBranches({
  first: 10,
  page: 1,
  where: { column: 'NAME', operator: 'LIKE', value: '%Main%' },
  orderBy: [{ column: 'CREATED_AT', order: 'DESC' }],
  search: 'Headquarters'
});
console.log(branchesData.data);
```

Returns a `CompanyBranchInterface` object containing an array of branch data and pagination info.

### createCompanyBranch(input: CompanyBranchInput): Promise<CompanyBranchInterface>

Creates a new company branch.

```typescript
const newBranch = await branches.createCompanyBranch({
  name: 'Downtown Office',
  companies_id: '123',
  address: '123 Main St, City',
  is_default: false
});
console.log(newBranch.id);
```

Returns a `CompanyBranchInterface` object with the created branch's details.

### updateCompanyBranch(id: string, input: CompanyBranchInput): Promise<CompanyBranchInterface>

Updates an existing company branch's information.

```typescript
const updatedBranch = await branches.updateCompanyBranch('456', {
  name: 'Updated Downtown Office',
  phone: '+1234567890'
});
console.log(updatedBranch.name);
```

Returns the updated `CompanyBranchInterface` object.

### deleteCompanyBranch(id: string): Promise<Boolean>

Deletes a company branch by its ID.

```typescript
const isDeleted = await branches.deleteCompanyBranch('456');
console.log(isDeleted); // true if successful
```

## User Management Methods

### getCompanyBranchUsers(options?: BranchUserQueryOptions): Promise<UserInterface>

Retrieves users associated with a company branch.

```typescript
const branchUsers = await branches.getCompanyBranchUsers({
  first: 20,
  page: 1,
  where: { column: 'BRANCHES_ID', operator: 'EQ', value: '456' }
});
console.log(branchUsers.data);
```

Returns a `UserInterface` object with user data and pagination info.

### addUserToBranch(id: string, user_id: string): Promise<Boolean>

Adds a user to a company branch.

```typescript
const added = await branches.addUserToBranch('456', '789');
console.log(added); // true if successful
```

### removeUserFromBranch(id: string, user_id: string): Promise<Boolean>

Removes a user from a company branch.

```typescript
const removed = await branches.removeUserFromBranch('456', '789');
console.log(removed); // true if successful
```

## Best Practices

1. Use pagination when fetching large sets of branches or users to optimize performance.
2. Implement proper error handling for all branch operations.
3. Validate input data before sending requests to create or update branches.
4. Use meaningful search terms and filters to narrow down branch queries.
5. Regularly audit branch user lists and remove unnecessary access.
6. Ensure that at least one branch is set as default for each company.

## Troubleshooting

- **Branch Creation Failures**: Ensure all required fields are provided and valid, especially the `companies_id`.
- **User Assignment Issues**: Verify that the user and branch IDs exist and are correct.
- **Query Performance**: Use appropriate filters and pagination to optimize large queries.
- **Permission Errors**: Ensure the authenticated user has the necessary permissions for branch operations.

## Error Handling

Implement try/catch blocks for all branch operations:

```typescript
try {
  await branches.updateCompanyBranch('456', updatedData);
} catch (error) {
  console.error('Failed to update branch:', error.message);
  // Handle error (e.g., show user feedback, log error)
}
```

Common error scenarios:
- Branch not found
- Duplicate branch name within a company
- Insufficient permissions
- Invalid input data
- Attempting to delete the last or default branch

## Security Considerations

1. Implement strict access controls for branch management operations.
2. Regularly audit branch membership and remove unnecessary access.
3. Use encrypted connections (HTTPS) for all branch-related operations.
4. Implement logging for sensitive branch operations for audit trails.
5. Validate and sanitize all input data to prevent injection attacks.

## Integration Tips

1. Combine with the Companies module for comprehensive company structure management.
2. Utilize the Users module to manage user-branch relationships effectively.
3. Integrate with the Filesystem module for handling branch-specific documents or images.
4. Use webhooks to sync branch data with external systems (e.g., HR software, CRM).

## Advanced Usage

### Batch Branch Operations

For efficient bulk operations:

```typescript
async function batchUpdateBranches(updates: Array<{id: string, input: CompanyBranchInput}>) {
  return Promise.all(updates.map(update => branches.updateCompanyBranch(update.id, update.input)));
}
```

### Branch Hierarchy Management

Implement branch hierarchy structures:

```typescript
async function createBranchHierarchy(companyId: string, mainBranch: CompanyBranchInput, subBranches: CompanyBranchInput[]) {
  const main = await branches.createCompanyBranch({...mainBranch, companies_id: companyId, is_default: true});
  
  const createdSubBranches = await Promise.all(subBranches.map(sub => 
    branches.createCompanyBranch({...sub, companies_id: companyId, parent_id: main.id})
  ));
  
  return { mainBranch: main, subBranches: createdSubBranches };
}
```

### Branch Analytics

Implement branch performance analytics:

```typescript
async function analyzeBranchPerformance(branchId: string, timeRange: { start: Date, end: Date }) {
  const branchUsers = await branches.getCompanyBranchUsers({
    where: { 
      column: 'BRANCHES_ID', 
      operator: 'EQ', 
      value: branchId,
      AND: [
        { column: 'CREATED_AT', operator: 'GTE', value: timeRange.start.toISOString() },
        { column: 'CREATED_AT', operator: 'LTE', value: timeRange.end.toISOString() }
      ]
    },
    orderBy: [{ column: 'CREATED_AT', order: 'ASC' }]
  });
  
  // Analyze user growth, activity, or other metrics
  // This is a simplified example - you'd typically integrate with other modules or external data
  return {
    userGrowth: branchUsers.data.length,
    activeUsers: branchUsers.data.filter(user => user.is_active).length,
    // Add more metrics as needed
  };
}
```

By effectively utilizing the Companies Branches module, you can build sophisticated branch management systems within your Kanvas-powered applications. This module allows for detailed control over company structure, user assignments, and branch-specific operations, enabling you to create tailored solutions for multi-location businesses or complex organizational structures.
