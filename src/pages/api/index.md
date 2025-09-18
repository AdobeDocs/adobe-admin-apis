# API reference

The Adobe Admin APIs provide all Enterprise customers with free, programmatic access to a standard set of administrative capabilities—regardless of their product mix. Using the Adobe Admin APIs, you can automate the Adobe Admin Console by integrating Adobe Admin APIs into your workflows, scripts, and tools.

## Connecting to the Adobe Admin API

Before using the Adobe Admin APIs, you must create a development project in the **Adobe Developer Console**. This integration registers your application as a client of the Adobe Admin APIs, and provides the credentials required to authorize API calls.

- For setup instructions, refer to [Developer Console](https://developer.adobe.com/).  
- For information about client credential authentication and retrieving **Client ID**, **Client Secret**, **Scopes**, or access tokens, refer to  [Authentication Setup](https://dummy-link.com/authentication-setup).

## Adobe Admin API Calls

Adobe Admin APIs provide enterprise organizations with programmatic control over administrative tasks in the **Adobe Admin Console**, enabling them to integrate Adobe's administrative capabilities into their workflows, scripts, and tools to automate administrative processes. With these APIs, you can configure and manage a **Content Retention Policy** for your organisation's inactive users' assets and more.

For more information on administrative capabilities available, see [Administrative Capabilities](https://dummy-link.com/capabilities).

All API requests should be directed to the Adobe Admin API server:

```json
https://cloudstorage.adobe.io/v1
```

## Policies

Represents a set of rules that govern how assets and operations are managed and accessed within the system.

| Operation                       | Method | Endpoint                     | Description                                                                                      |
|----------------------------------|--------|------------------------------|--------------------------------------------------------------------------------------------------|
| Get a policy by policyType       | GET    | `/policies/{policyType}`     | This endpoint retrieves a specific policy identified by its policyType, provided the user has the necessary permissions. |
| Update a policy by policyType    | PATCH  | `/policies/{policyType}`     | This endpoint updates a specific policy identified by its policyType, provided the user has the necessary permissions.    |
