# API reference

The Adobe Admin APIs for Storage Management provide all Enterprise customers with free, programmatic access to a standard set of storage management capabilities to manage content stored in Adobe storage for business. This enables them to integrate Adobe's storage management capabilities into their workflows, scripts, and tools to automate storage management.

## Connecting to the Adobe Admin APIs

Before using the Adobe Admin APIs for Storage Management, you must create a development project in the **Adobe Developer Console**. This integration registers your application as a client of the Adobe Admin APIs for Storage Management, and provides the necessary credentials to authorize API calls.

- For setup instructions, refer to [Developer Console](https://developer.adobe.com/).  
- For details on client credential authentication, including how to retrieve your Client ID, Client Secret, Scopes, and access tokens, refer to  [Authentication Setup](https://developer-stage.adobe.com/cloud-storage/guides/getting-started/authentication).

## API calls

Read more complete overview of [available storage management capabilities](../guides/overview/capabilities.md).

With these APIs, you can configure and manage a Content Retention Policy for your organization's inactive users' assets and more.

All API requests should be directed to the Adobe Admin API for Storage Management server:

```json
https://cloudstorage.adobe.io/v1
```

## Policies

Represents a set of rules that govern how assets and operations are managed and accessed within the system.

| Operation                             | Method | Endpoint                                               | Description                                                                                                                                                                                                                                                                                        |
|---------------------------------------|--------|--------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Get a policy by policyType            | GET    | `/policies/org/{policyType}`                           | Retrieves a specific policy identified by its policyType, provided the user has the necessary permissions.                                                                                                                                                                                         |
| Update a policy by policyType         | PATCH  | `/policies/org/{policyType}`                           | Updates a specific policy identified by its policyType, provided the user has the necessary permissions.                                                                                                                                                                                           |
| List policies                         | GET    | `/policies/asset/{policyType}`                         | Lists all policies of a given policyType.                                                                                                                                                                                                                                                          |
| Get policy by policyId                | GET    | `/policies/asset/{policyType}/{policyId}`              | Retrieves a specific policy by policyId.                                                                                                                                                                                                                                                           |
| Create policy                         | POST   | `/policies/asset/{policyType}`                         | Creates a new policy.                                                                                                                                                                                                                                                                              |
| Update policy                         | PATCH  | `/policies/asset/{policyType}/{policyId}`              | Updates a specific policy.                                                                                                                                                                                                                                                                         |
| Delete policy                         | DELETE | `/policies/asset/{policyType}/{policyId}`              | Deletes a specific policy.                                                                                                                                                                                                                                                                         |
| Attach single asset to a policy       | POST   | `/policies/asset/{policyType}/{policyId}/add-asset`    | Associates an asset to a policy.                                                                                                                                                                                                                                                                   |
| Remove single asset from policy       | POST   | `/policies/asset/{policyType}/{policyId}/remove-asset` | Removes an asset from a policy.                                                                                                                                                                                                                                                                    |
| Get assets attached to policy         | GET    | `/policies/asset/{policyType}/{policyId}/assets`       | Gets assets associated with a specific policy.                                                                                                                                                                                                                                                     |
| Get cleanup policies applied on asset | GET    | `/projects/{assetId}/policies`                         | Gets policies applied on a specific asset.          \<br /\> The API currently only returns direct policies applied on asset.|
