# Working with Adobe Admin APIs for Storage Management

This guide outlines the essential steps to get started with Adobe Admin APIs for Storage Management. It covers how to set up your Developer Console project, configure access and permissions, retrieve credentials, and test endpoints to manage content stored in Adobe storage for business.

## Prerequisites

To use the Adobe Admin APIs for Storage Management, the user must have developer rights within the Adobe organization. This involves:

- Adding the user as a developer in the organization.
- Assigning the necessary products for the developer APIs.

## Step 1: Set up your Developer Console project

1. Log in to the [Adobe Developer Console](https://developer.adobe.com/).
2. Create a project or open an existing one.
3. Add **Adobe Admin APIs -  Storage Management** to your project.
4. Configure the API to use server-to-server authentication. This setup allows your server to securely store client secrets and generate access tokens without user interaction.

## Step 2: Configure access and permissions

- Add the relevant product profiles to your integration’s service account. This grants access to granular Admin API features.
- After saving the API configuration, assign the technical user a role such as system admin, storage admin, or both within the organization. This step ensures the user has the necessary permissions to perform administrative operations.

## Step 3: Obtain credentials and access tokens

1. Return to your [Developer Console project](https://developer.adobe.com/) to retrieve credentials:

   - Client ID
   - Client secret
   - Scopes  

2. You can generate an access token directly from the Developer Console UI or programmatically by using these credentials to request a v3 access token.

## Step 4: Testing API endpoints

For quick testing and exploration, you can use the generated access token to authorize requests on the [Swagger UI](../../api/specification.md).

Here, you can interact with Adobe Admin APIs for Storage Management’s endpoints, including policy-related operations for admin users, to verify your setup and understand how the APIs work.

## Step 5: Managing content with Adobe Admin APIs for Storage Management

You can manage the following types of policies: 

- [Content Retention policy](#content-retention-policy)
- [Move Restrictions policy](#move-restrictions-policy)

### Content retention policy

The _Content Retention Policy for Inactive User_ defines rules such as retention periods and content deletion criteria for inactive users, automatically triggering the permanent deletion of user assets once the defined retention period expires.

To use this policy for your organization, you can configure, retrieve, and update it using the APIs described below.

#### Policy object

The following policy objects are available:

| Parameter | Description |
|---|---|
| `policyType` | A string representing the type of policy (Example:  `inactive_user_content_purge`).  |
| `attributes` | An object containing policy-specific settings, including:  <br> - `enabled` (boolean): Whether the policy is active.  <br> - `retention` (string, optional): Retention period in ISO 8601 format. |

#### Enabling policy

Use a `PATCH` request to enable the policy. The default retention period is 2 years, which can be customised to any duration between 30 days and 10 years (specified in months or years) using the ISO 8601 duration format.

##### Request

```bash
curl -X PATCH \
  'https://cloudstorage-stage.adobe.io/v1/policies/org/inactive_user_content_purge' \
  -H 'accept: application/json' \
  -H 'If-Match: "your-current-etag-value"' \
  -H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
    {
      "op": "replace",
      "path": "/attributes/enabled",
      "value": "true"
    }
  ]'
```

Replace `YOUR_ACCESS_TOKEN` with a valid OAuth access token.  
The `If-Match` header includes the ETag(s) for optimistic concurrency control.

##### Response

Sample response:

```json
{
  "policyType": "inactive_user_content_purge",
  "attributes": {
    "enabled": true,
    "retention": "P2Y"
  }
}
```

**Response parameters**

| Parameter | Description |
|---|---|
| `policyType` | The type of the policy |
| `attributes.enabled` | Whether the policy is enabled (`true`) or disabled (`false`) |
| `attributes.retention` | Retention period using ISO 8601 duration format (`P2Y` means 2 years) |

#### Get policy details

Use the `GET Policy details` API to retrieve the details of a specific policy for your organization.

##### Request

```bash
curl -X GET \ 
    'https://cloudstorage-stage.adobe.io/v1/policies/org/inactive_user_content_purge' \ 
    -H 'accept: application/json' \ 
    -H 'x-request-id: 1234567890' \ 
    -H 'Authorization: Bearer YOUR_ACCESS_TOKEN_HERE' 
```

Replace `YOUR_ACCESS_TOKEN_HERE` with a valid OAuth access v3 token.

##### Response

Sample response:

```json
{
    "policyType": "inactive_user_content_purge",
    "attributes": {
        "enabled": true,
        "retention": "P2Y"
    }
}
```

Response parameters:

| Parameter | Description |
|---|---|
| `policyType` | The type of the policy |
| `attributes.enabled` | Whether the policy is enabled (true) or disabled (false) |
| `attributes.retention` | Retention period using ISO 8601 duration format (P2Y means 2 years) |

#### Disabling policy

Use a PATCH request to disable the policy.

##### Request

```bash
curl -X PATCH \
  'https://cloudstorage-stage.adobe.io/v1/policies/org/inactive_user_content_purge' \
  -H 'accept: application/json' \
  -H 'If-Match: "your-current-etag-value"' \
  -H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
    {
      "op": "replace",
      "path": "/attributes/enabled",
      "value": "false"
    }
  ]'
```

Replace `YOUR_ACCESS_TOKEN` with a valid OAuth access token.  
The `If-Match` header includes the ETag(s) for optimistic concurrency control.

##### Response

Sample response:

```json
{
  "policyType": "inactive_user_content_purge",
  "attributes": {
    "enabled": false,
    "retention": "P2Y"
  }
}
```

#### Updating retention period

Use a PATCH request to modify retention of an existing policy.

##### Request

```bash
curl -X PATCH \
  'https://cloudstorage-stage.adobe.io/v1/policies/org/inactive_user_content_purge' \
  -H 'accept: application/json' \
  -H 'If-Match: "your-current-etag-value"' \
  -H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  -H 'Content-Type: application/json-patch+json' \
  -H 'x-request-id: 123e4567-e89b-12d3-a456-426614174000' \
  -d '[
    {
      "op": "replace",
      "path": "/attributes/retention",
      "value": "P5Y"
    }
  ]'
```

Replace `YOUR_ACCESS_TOKEN` with a valid OAuth access token.  
The `If-Match` header includes the ETag(s) for optimistic concurrency control.

##### Response

Sample response:

```json
{
  "policyType": "inactive_user_content_purge",
  "attributes": {
    "enabled": true,
    "retention": "P5Y"
  }
}
```

### Move Restrictions policy

The Move Restrictions Policy determines whether users in your organization can move assets into shared projects or folders outside your organization’s storage.

To use this policy for your organization, you can retrieve, enable and disable it using the APIs described below.

#### Policy object

The following policy objects are available:

| Parameter | Description |
|---|---|
| `policyType` | A string representing the type of policy (Example: asset_ownership_transfer) |
| `attributes` | An object containing policy-specific settings, including:  <br> - `enabled` (boolean): Whether the policy is active. |

#### Get policy details

Use the `GET Policy details` API to retrieve the current configuration for your organization. 

##### Request

```bash
curl --location 'https://cloudstorage-stage.adobe.io/v1/policies/org/asset_ownership_transfer' \
--header 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
--header 'x-request-id: 1234567890' \
```

##### Response

```json
{
  "policyType": "asset_ownership_transfer",
  "attributes": {
    "enabled": true
  }
}
```

#### Disable policy

Use a PATCH request to disable the policy.

##### Request

```bash
curl --location --request PATCH 'https://cloudstorage-stage.adobe.io/v1/policies/org/asset_ownership_transfer' \
--header 'Content-Type: application/json-patch+json' \
--header 'If-Match: "your-current-etag-value"' \
--header 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
--header 'x-request-id: 1234567890' \
--data '[
  {
    "op": "replace",
    "path": "/attributes/enabled",
    "value": false
  }
]'
```

##### Response

```json
{
  "policyType": "asset_ownership_transfer",
  "attributes": {
    "enabled": false
  }
}
```

#### Enable policy

Use a PATCH request to enable the policy.

##### Request

```bash
curl --location --request PATCH 'https://cloudstorage-stage.adobe.io/v1/policies/org/asset_ownership_transfer' \
--header 'Content-Type: application/json-patch+json' \
--header 'If-Match: "your-current-etag-value"' \
--header 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
--header 'x-request-id: 1234567890' \
--data '[
  {
    "op": "replace",
    "path": "/attributes/enabled",
    "value": true
  }
]'
```

##### Response

```json
{
  "policyType": "asset_ownership_transfer",
  "attributes": {
    "enabled": true
  }
}
```

#### Response parameters

| Parameter          | Description                                     |
|--------------------|------------------------------------------------|
| `policyType`         | The type of the policy                          |
| `attributes.enabled` | Whether the policy is enabled (true) or disabled (false) |
