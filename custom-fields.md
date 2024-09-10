### Custom Fields

One of the most powerful features of Kanvas is the ability to add custom fields to your app. Custom fields are used to store additional information about any entity in your app. Think of them as a dynamic storage system, much like a hashtable, where you can store any data tied directly to a specific entity.

Kanvas provides **two primary interfaces** for managing custom fields:
- **App, Users, & Company Settings** (special handling)
- **Entity Custom Fields** (standard handling for other entities)

These interfaces allow for flexible customization, enabling you to adapt the data model for different entities based on your application's needs.

#### Supported Data Types for Custom Fields
You can store the following types of data in custom fields:
- **Strings**
- **Arrays**
- **Numbers**
- **Boolean**

### Key Features

Kanvas offers several methods to interact with custom fields:

- **Set:** Add or update custom field data for any entity.
- **Get:** Retrieve a specific custom field value.
- **GetAll:** Retrieve all custom fields associated with an entity.
- **Delete:** Remove a custom field from an entity.

### Custom Field Categories

Kanvas distinguishes between different types of custom fields:
1. **App Settings:** Global settings applied across the entire application.
2. **User Settings:** Settings specific to individual users.
3. **Company Settings:** Configuration settings for specific companies or organizations.
4. **Entity Custom Fields:** Custom fields that can be attached to any other entities, such as products or messages.

App, company, and user settings are treated with special importance and are managed with dedicated methods for retrieval and modification. All other entities use a more generalized interface for handling custom fields. 

This separation ensures that critical settings like app configuration and user preferences are handled efficiently, while still offering extensive flexibility for other entities.


## App Settings

App settings represent global configuration options that apply to the entire application. These are managed separately from other custom fields, with specific methods dedicated to their retrieval and modification.

What would be the usage of app settings?
- feature flags
- configuration for internal app settings (smtp, third party integrations, etc)
- branding
- etc

#### 1. Get All App Settings

To retrieve all the settings associated with the current app, you can use the `appSettings()` method. This method returns a list of all settings, making it easy to manage global configurations.

```typescript
const settings = await kanvasSDK.settings.appSettings();
console.log(settings.adminAppSettings);  // Logs all app settings
```

#### 2. Get a Specific App Setting

To retrieve a specific app setting, use the `appSetting()` method. You pass the key of the setting you want to retrieve.

```typescript
const themeColor = await kanvasSDK.settings.appSetting('theme_color');
console.log(themeColor);  // Returns the theme color setting for the app
```

#### 3. Set an App Setting

To add or modify an app setting, use the `setAppSettings()` method. This method allows you to configure values that will apply across the entire application.

```typescript
await kanvasSDK.settings.setAppSettings({
    key: 'theme_color',
    value: '#000000',
    public: true
});
```

These examples demonstrate how to manage global settings within your application using dedicated methods, ensuring that core configuration remains easily accessible and maintainable.

## Company Settings

Company settings are used to store configuration options that are specific to a company or organization. These settings are used to configure the behavior of the app for a specific company.

Examples:
- Total number of users
- Company feature flag
- Configuration for third party integrations for that specific company (smtp, twillio, shopify keys, etc)
- Custom fields for a company
- etc

#### 1. Get All Company Settings

To retrieve all the settings associated with the current company, you can use the `companySettings()` method. This method returns a list of all settings, making it easy to manage global configurations.

```typescript
const settings = await kanvasSDK.settings.getCompanySettings(companyUuid);
console.log(settings.adminCompanySettings);  // Logs all app settings
```

#### 2. Get a Specific Company Setting

To retrieve a specific company setting, use the `companySetting()` method. You pass the key of the setting you want to retrieve.

```typescript
const themeColor = await kanvasSDK.settings.companySetting(companyUuid, key);
console.log(themeColor);  // Returns the theme color setting for the app
```

#### 3. Set an Company Setting

To add or modify an company setting, use the `setCompanySettings()` method. This method allows you to configure values that will apply across the entire application.

```typescript
await kanvasSDK.settings.setCompanySettings({
    entity_uuid: companyUuid,
    key: 'stripe_key',
    value: 'sk_test_1234567890',
    public: false
});
```

These examples demonstrate how to manage global settings within your application using dedicated methods, ensuring that core configuration remains easily accessible and maintainable.

## User Settings

User settings are used to store configuration options that are specific to a user. These settings are used to configure the behavior of the app for a specific user.

