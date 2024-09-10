### Custom Fields

One of the most powerful features of Kanvas is the ability to add custom fields to your app. Custom fields are used to store additional information about any entity in your app. Imagine custom fields as a dynamic storage system, much like a hashtable, where you can store any data you want, tied directly to a specific entity within your app.

We provide **two interfaces** to work with custom fields:
- **App , Users & Company Settings** (special handling)
- **Entity Custom Fields** (standard handling for other entities)

These interfaces allow you to extend the flexibility of your application by customizing the data associated with different entities, enabling a more tailored experience for each user or system.

#### What Data Types Can You Use for Custom Fields?
You can store the following types of data:
- **Strings**
- **Arrays**
- **Numbers**
- **Boolean**

### Key Features

Kanvas provides a set of methods to interact with custom fields:

- **Set:** Add or update custom field data for any entity.
- **Get:** Retrieve a specific custom field value.
- **GetAll:** Retrieve all custom fields for a particular entity.
- **Delete:** Remove a custom field from an entity.


### Custom Field Categories

Kanvas distinguishes between custom fields for:
1. **App Settings:** Global settings that apply across the application.
2. **User Settings:** User-level settings that configure specific users within the app.
3. **Company Settings:** Company-level settings that configure specific organizations within the app.
4. **Entity Custom Fields:** Custom fields that can be added to any other entities such as products or messages.

App, company, and user settings are treated differently than other custom fields. These settings are core to the ecosystem and have their own dedicated methods for retrieving and modifying data.


## App Settings

App settings represent global configuration options that apply to the entire application. These are managed separately from other custom fields, with specific methods dedicated to their retrieval and modification.

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