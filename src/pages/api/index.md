# API reference

The Adobe Admin APIs provide enterprise customers complimentary, programmatic access to a standardized set of administrative capabilities,  regardless of their product mix. Using the Adobe Admin APIs, you can automate the Adobe Admin Console by integrating these APIs into your workflows, scripts, and tools.

## Connecting to the Adobe Admin APIs

Before using the Adobe Admin APIs, you must create a development project in the **Adobe Developer Console**. This integration registers your application as a client of the Adobe Admin APIs, and provides the necessary credentials to authorize API calls.

- For setup instructions, refer to [Developer Console](https://developer.adobe.com/).  
- For details on client credential authentication, including how to retrieve your Client ID, Client Secret, Scopes, and access tokens, refer to  [Authentication Setup](https://developer-stage.adobe.com/cloud-storage/guides/getting-started/authentication).

## Adobe Admin API Calls

Adobe Admin APIs provide enterprise organizations with programmatic control over administrative tasks in the Adobe Admin Console. These APIs allow you to integrate Adobe’s administrative features into your internal systems, streamlining and automating processes such as configuring a Content Retention Policy for inactive user assets and more.

For a complete overview of available features, see [Administrative Capabilities](../guides/overview/capabilities.md).

All API requests should be directed to the Adobe Admin API server:

```json
https://cloudstorage.adobe.io/v1
```

## Policies

Represents a set of rules that govern how assets and operations are managed and accessed within the system.

| Operation                       | Method | Endpoint                     | Description                                                                                      |
|----------------------------------|--------|------------------------------|--------------------------------------------------------------------------------------------------|
| Get a policy by policyType       | GET    | `/policies/org/{policyType}`     | Retrieves a specific policy identified by its policyType, provided the user has the necessary permissions. |
| Update a policy by policyType    | PATCH  | `/policies/org/{policyType}`     | Updates a specific policy identified by its policyType, provided the user has the necessary permissions.    |
