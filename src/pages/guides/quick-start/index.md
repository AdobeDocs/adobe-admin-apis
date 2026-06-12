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

- [Content Retention policy for inactive user](#content-retention-policy-for-inactive-user)
- [Content Retention Policy for Work-in-Progress (WIP) content](#content-retention-policy-for-work-in-progress-wip-content)
- [Move Assets policy](#move-assets-policy)

### Content retention policy for inactive user

The _Content Retention Policy for Inactive User_ defines rules such as retention periods and content deletion criteria for inactive users. It automatically triggers permanent deletion of user assets after the defined retention period expires.

To use this policy for your organization, you can configure, retrieve, and update the policy using the APIs described below.

#### Policy object

The following policy objects are available:

| Parameter | Description |
|---|---|
| `policyType` | A string representing the type of policy (Example:  `inactive_user_content_purge`).  |
| `attributes.enabled` | Indicates whether the policy is active.  |
|`attributes.retention` | Retention period in ISO 8601 format. |

#### Enabling policy

Use the `PATCH /policies/org/{policyType}` request to enable the policy. The default retention period is two years, which can be customized to any duration between 30 days and 10 years, specified in months or years using the ISO 8601 duration format.

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

**Notes:**

- Replace `YOUR_ACCESS_TOKEN` with a valid OAuth access token.
- The `If-Match` header includes the ETag(s) for optimistic concurrency control.

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
| `attributes.retention` | Retention period in ISO 8601 duration format (for example, `P2Y` represents 2 years) |

#### Get policy details

Use the `GET policies/org/{policyType}` API to retrieve the details of a specific policy for your organization.

##### Request

```bash
curl -X GET \ 
    'https://cloudstorage-stage.adobe.io/v1/policies/org/inactive_user_content_purge' \ 
    -H 'accept: application/json' \ 
    -H 'x-request-id: 1234567890' \ 
    -H 'Authorization: Bearer YOUR_ACCESS_TOKEN_HERE' 
```

**Note:** Replace `YOUR_ACCESS_TOKEN_HERE` with a valid OAuth access v3 token.

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

**Notes:**

- Replace `YOUR_ACCESS_TOKEN` with a valid OAuth access token.  
- The `If-Match` header includes the ETag(s) for optimistic concurrency control.

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

Use the `PATCH /policies/org/{policyType}` request to modify retention of an existing policy.

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

**Notes:**

- Replace `YOUR_ACCESS_TOKEN` with a valid OAuth access token.  
- The `If-Match` header includes the ETag(s) for optimistic concurrency control.

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

### Content Retention Policy for Work-in-Progress (WIP) content

The Content Retention Policy for Work-in-Progress (WIP) Content defines how long Creative Cloud Projects are retained from the date the policy is associated before they are permanently deleted. Administrators can create one or more policies per organization and associate them individually with specific Creative Cloud Projects.

A Creative Cloud Project can be directly associated with only one scheduled content deletion policy at a time.

The retention period begins when the policy is first associated with the project. If a different policy is later associated with the same project, the retention timer restarts from the new association date.

Projects associated with a scheduled content deletion policy remain fully accessible for standard CRUD operations. CRUD operations do not reset or impact retention enforcement.

If multiple cleanup policies apply to a project, the earliest scheduled deletion date takes precedence.

#### Retention Lifecycle

| Step | Event                                                    |
|------|----------------------------------------------------------|
| 1    | Policy associated with project (`policyAppliedDate` set) |
| 2    | Retention period runs                                    |
| 3    | Retention period ends                                    |
| 4    | Project soft-deleted → moves to Deleted view             |
| 5    | 30 days after soft delete                                |
| 6    | Project permanently and irrecoverably deleted            |

#### Policy Object

- `policyType` - Type of policy. Value: `scheduled_content_deletion`
- `policyId` - Unique identifier for the policy instance (UUID)
- `name` - Admin-supplied display name for the policy
- `attributes.retention` - Retention duration in ISO 8601 format. Minimum: `P1M`, Maximum: `P10Y`
- `createdDate` - ISO 8601 timestamp when the policy was created
- `modifiedDate` - ISO 8601 timestamp when the policy was last modified
- `policyEtag` - ETag used for optimistic concurrency control

#### Create a Policy

Use the `POST /policies/asset/{policyType}` request to create a new WIP retention policy.

**Request**

```bash
curl -X POST \
  'https://cloudstorage-stage.adobe.io/v1/policies/asset/scheduled_content_deletion' \
  -H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-request-id: 1234567890' \
  -d '{
    "name": "WIP Cleanup - 6 months",
    "attributes": {
      "retention": "P6M"
    }
  }'
```

**Notes:**

- Replace `YOUR_ACCESS_TOKEN` with a valid OAuth v3 access token.
- The authenticated user must have `org_admin` or `storage_admin` role.

**Response**

```json
{
  "policyId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "policyType": "scheduled_content_deletion",
  "name": "WIP Cleanup - 6 months",
  "attributes": {
    "retention": "P6M"
  },
  "createdDate": "2025-01-05T14:00:00Z",
  "modifiedDate": "2025-01-05T14:00:00Z",
  "policyEtag": "1735304400000"
}
```

#### Get a Policy

Use the `GET /policies/asset/{policyType}/{policyId}` request to retrieve a specific policy.

**Request**

```bash
curl -X GET \
  'https://cloudstorage-stage.adobe.io/v1/policies/asset/scheduled_content_deletion/{policyId}' \
  -H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  -H 'x-request-id: 1234567890'
```

**Response**

```json
{
  "policyId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "policyType": "scheduled_content_deletion",
  "name": "WIP Cleanup - 6 months",
  "attributes": {
    "retention": "P6M"
  },
  "createdDate": "2025-01-05T14:00:00Z",
  "modifiedDate": "2025-01-05T14:00:00Z",
  "policyEtag": "1735304400000"
}
```

#### List All Policies

Use a `GET /policies/{policyType}` request to list all WIP retention policies for your organization.

**Request**

```bash
curl -X GET \
  'https://cloudstorage-stage.adobe.io/v1/policies/asset/scheduled_content_deletion?limit=50' \
  -H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  -H 'x-request-id: 1234567890'
```

**Response**

```json
{
  "paging": {
    "nextUrl": "https://cloudstorage-stage.adobe.io/v1/policies/asset/scheduled_content_deletion?cursor=eyJvZmZzZXQiOjJ9",
    "limit": 50
  },
  "items": [
    {
      "policyId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
      "policyType": "scheduled_content_deletion",
      "name": "WIP Cleanup - 6 months",
      "attributes": {
        "retention": "P6M"
      },
      "createdDate": "2025-01-05T14:00:00Z",
      "modifiedDate": "2025-01-05T14:00:00Z",
      "policyEtag": "1735304400000"
    }
  ]
}
```

#### Update a Policy

Use a `PATCH /policies/asset//{policyType}/{policyId}` request to modify an existing policy.

**Request**
```bash
curl -X PATCH \
  'https://cloudstorage-stage.adobe.io/v1/policies/asset/scheduled_content_deletion/{policyId}' \
  -H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  -H 'If-Match: "YOUR_CURRENT_ETAG"' \
  -H 'Content-Type: application/json-patch+json' \
  -H 'x-request-id: 1234567890' \
  -d '[
    {
      "op": "replace",
      "path": "/attributes/retention",
      "value": "P1Y"
    }
  ]'
```

**Response**

```json
{
  "policyId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "policyType": "scheduled_content_deletion",
  "name": "WIP Cleanup - 6 months",
  "attributes": {
    "retention": "P1Y"
  },
  "createdDate": "2025-01-05T14:00:00Z",
  "modifiedDate": "2025-06-01T09:00:00Z",
  "policyEtag": "1748768400000"
}
```

#### Delete a Policy

Use a `DELETE /policies/asset/{policyType}/{policyId}` request to permanently remove a policy.

Deleting a policy immediately stops enforcement for all associated projects. Projects are not deleted because of policy deletion.

**Request**

```bash
curl -X DELETE \
  'https://cloudstorage-stage.adobe.io/v1/policies/asset/scheduled_content_deletion/{policyId}' \
  -H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  -H 'If-Match: "YOUR_CURRENT_ETAG"' \
  -H 'x-request-id: 1234567890'
```

**Response**

`204 No Content`

#### Associate a CC Project with a Policy

Use a `POST /policies/asset/{policyType}/{policyId}/add-asset` request to associate a Creative Cloud Project with a retention policy.

Once associated, the retention period begins from the association date.

**Request**

```bash
curl -X POST \
  'https://cloudstorage-stage.adobe.io/v1/policies/asset/scheduled_content_deletion/{policyId}/add-asset' \
  -H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-request-id: 1234567890' \
  -d '{
    "assetId": "urn:aaid:sc:US:your-project-id"
  }'
```

**Response**

```json
{
  "assetId": "urn:aaid:sc:US:your-project-id",
  "assetType": "project",
  "name": "My Creative Project",
  "path": "/My Creative Project",
  "policyAppliedDate": "2025-06-01T10:30:00Z",
  "policyAppliedBy": "admin-guid@techacct.adobe.com"
}
```

#### Remove a CC Project from a Policy

Use a `POST /policies/asset/{policyType}/{policyId}/remove-asset` request to disassociate a project from a retention policy.

**Request**

```bash
curl -X POST \
  'https://cloudstorage-stage.adobe.io/v1/policies/asset/scheduled_content_deletion/{policyId}/remove-asset' \
  -H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-request-id: 1234567890' \
  -d '{
    "assetId": "urn:aaid:sc:US:your-project-id"
  }'
```

**Response**

`200 OK`

#### List Projects Associated with a Policy

Use a `GET /policies/asset/{policyType}n/{policyId}/assets` request to retrieve all Creative Cloud Projects currently associated with a specific policy.

**Request**

```bash
curl -X GET \
  'https://cloudstorage-stage.adobe.io/v1/policies/asset/scheduled_content_deletion/{policyId}/assets' \
  -H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  -H 'x-request-id: 1234567890'
```

**Response**

```json
{
  "paging": {
    "nextUrl": "https://cloudstorage-stage.adobe.io/v1/policies/asset/scheduled_content_deletion/{policyId}/assets?cursor=eyJvZmZzZXQiOjIwfQ",
    "limit": 20
  },
  "items": [
    {
      "assetId": "urn:aaid:sc:US:your-project-id",
      "assetType": "project",
      "name": "My Creative Project",
      "path": "/My Creative Project",
      "policyAppliedDate": "2025-06-01T10:30:00Z",
      "policyAppliedBy": "admin-guid@techacct.adobe.com"
    }
  ]
}
```

#### Get Policy Applied to a Project

> **Note:** This API requires the `cloud_storage_collab_api` scope in addition to the admin API scopes.

Use a `GET /projects/{projectId}/policies` request to retrieve the current retention policy currently associated with a specific Creative Cloud Project.

**Request**
```bash
curl -X GET \
  'https://cloudstorage-stage.adobe.io/v1/projects/{projectId}/policies' \
  -H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  -H 'x-request-id: 1234567890'
```

**Response**
```json
{
  "items": [
    {
      "policyId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
      "policyType": "scheduled_content_deletion",
      "name": "WIP Cleanup - 6 months",
      "policyAppliedDate": "2025-06-01T10:30:00Z",
      "attributes": {
        "retention": "P6M"
      },
      "policyEtag": "1735304400000"
    }
  ]
}
```

#### Response Codes

| Code | Description                                                        |
|------|--------------------------------------------------------------------|
| 200  | OK — request succeeded                                             |
| 201  | Created — policy created successfully                              |
| 204  | No Content — policy deleted successfully                           |
| 400  | Bad Request — unsupported asset type or malformed request body     |
| 403  | Forbidden — caller does not have org_admin or storage_admin role   |
| 404  | Not Found — policy or project does not exist                       |
| 409  | Conflict — project already associated with another policy          |
| 412  | Precondition Failed — ETag mismatch                                |
| 422  | Unprocessable Entity — validation error or invalid retention value |

### Move Assets policy

The Move Assets Policy determines whether users in your organization can move assets into shared projects or folders outside your organization’s storage.

To use this policy for your organization, you can retrieve, enable and disable it using the APIs described below.

#### Policy object

The following policy objects are available:

| Parameter | Description |
|---|---|
| `policyType` | A string representing the type of policy (Example: asset_ownership_transfer) |
| `attributes` | An object containing policy-specific settings, for example, the value `enabled` (boolean) indicates whether the policy is active. |

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
