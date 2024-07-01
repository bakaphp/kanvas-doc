# System Modules Module

The System Modules module in the Kanvas Core SDK provides functionality for managing and querying system modules within the Kanvas ecosystem. System modules represent different components or features of the system, allowing for dynamic configuration and extensibility.

## Key Features

- Retrieve system modules
- Query modules by slug
- Hierarchical module structure support

## Usage

Access the System Modules module through the `systemModules` property on your KanvasCore instance:

```typescript
const kanvas = new KanvasCore({...});
const systemModules = kanvas.systemModules;
```

## Core Methods

### getSystemModules(first: number, page?: number): Promise<SystemModuleInterface[]>

Retrieves a paginated list of system modules.

```typescript
const modules = await systemModules.getSystemModules(10, 1);
console.log(modules);
```

Parameters:
- `first`: Number of modules to retrieve
- `page`: Page number for pagination (optional)

Returns an array of `SystemModuleInterface` objects.

### getSystemModulesBySlug(slug: string): Promise<SystemModuleInterface[]>

Retrieves system modules by their slug.

```typescript
const module = await systemModules.getSystemModulesBySlug('users');
console.log(module);
```

Parameters:
- `slug`: The unique slug identifier for the module

Returns an array of matching `SystemModuleInterface` objects (usually just one).

## SystemModuleInterface

The `SystemModuleInterface` represents the structure of a system module:

```typescript
interface SystemModuleInterface {
  id: string;
  uuid: string;
  name: string;
  slug: string;
  model_name: string;
  app: AppUserInterface;
  parent: SystemModuleInterface;
  menu_order: number;
  show: number;
}
```

- `id`: Unique identifier
- `uuid`: Universal unique identifier
- `name`: Human-readable name of the module
- `slug`: URL-friendly identifier
- `model_name`: Associated model name (if applicable)
- `app`: Related app information
- `parent`: Parent module (for hierarchical structures)
- `menu_order`: Order in menu listings
- `show`: Visibility flag

## Best Practices

1. Cache frequently accessed modules to reduce API calls.
2. Use slugs for consistent module identification across the application.
3. Implement error handling for cases where modules might not exist.
4. Utilize pagination to efficiently handle large numbers of modules.
5. Consider module hierarchies when designing system architecture.

## Troubleshooting

- **Module Not Found**: Ensure the slug or ID used is correct and the module exists.
- **Pagination Issues**: Verify that the `first` and `page` parameters are valid.
- **Performance Concerns**: For large systems, consider implementing local caching of module data.

## Error Handling

Implement try/catch blocks for all system module operations:

```typescript
try {
  const modules = await systemModules.getSystemModules(10);
} catch (error) {
  console.error('Failed to fetch system modules:', error.message);
  // Handle error (e.g., show user feedback, log error)
}
```

Common error scenarios:
- Network failures
- Invalid pagination parameters
- Module not found (for slug-based queries)

## Security Considerations

1. Ensure that only authorized users can access system module information.
2. Validate input parameters to prevent potential injection attacks.
3. Be cautious about exposing detailed module information in client-side applications.

## Integration Tips

1. Use system modules to dynamically configure UI components or features.
2. Integrate with the Roles module to implement module-based permissions.
3. Utilize system modules for extensible plugin architectures in your application.

## Advanced Usage

### Dynamic Feature Toggling

Use system modules to implement dynamic feature toggling:

```typescript
async function isFeatureEnabled(featureSlug: string): Promise<boolean> {
  const [feature] = await systemModules.getSystemModulesBySlug(featureSlug);
  return feature ? feature.show === 1 : false;
}

// Usage
if (await isFeatureEnabled('advanced-analytics')) {
  // Enable advanced analytics feature
}
```

### Module Hierarchy Navigation

Implement a function to traverse module hierarchies:

```typescript
async function getModuleHierarchy(rootSlug: string): Promise<SystemModuleInterface[]> {
  const [rootModule] = await systemModules.getSystemModulesBySlug(rootSlug);
  if (!rootModule) return [];

  const allModules = await systemModules.getSystemModules(100); // Adjust number as needed
  
  function findChildren(parent: SystemModuleInterface): SystemModuleInterface[] {
    return allModules.filter(m => m.parent && m.parent.id === parent.id);
  }

  function buildHierarchy(module: SystemModuleInterface): SystemModuleInterface {
    const children = findChildren(module);
    return {
      ...module,
      children: children.map(buildHierarchy)
    };
  }

  return [buildHierarchy(rootModule)];
}

// Usage
const userModuleHierarchy = await getModuleHierarchy('users');
console.log(JSON.stringify(userModuleHierarchy, null, 2));
```

### Module-based Permission Check

Integrate with a hypothetical permission system:

```typescript
async function hasModulePermission(userId: string, moduleSlug: string): Promise<boolean> {
  const [module] = await systemModules.getSystemModulesBySlug(moduleSlug);
  if (!module) return false;

  // This is a hypothetical function - implement based on your permission system
  return checkUserPermission(userId, module.id);
}

// Usage
if (await hasModulePermission('user123', 'admin-panel')) {
  // Allow access to admin panel
} else {
  // Deny access
}
```

By effectively utilizing the System Modules module, you can create dynamic, extensible applications within the Kanvas ecosystem. This module is particularly useful for building modular systems, implementing feature flags, and managing complex application structures with hierarchical components.
