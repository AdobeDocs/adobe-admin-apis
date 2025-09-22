# Working with Admin APIs

This guide outlines the essential steps to get started with Adobe Admin APIs. It covers how to set up your Developer Console project, configure access and permissions, retrieve credentials, and test endpoints for policy management and other administrative tasks.

## Prerequisites

To use the Admin APIs, the user must have developer rights within the Adobe organization. This involves:

- Adding the user as a developer in the organization.
- Assigning the necessary products for the developer APIs.

## Step 1: Set up your Developer Console project

1. Log in to the [Adobe Developer Console](https://developer.adobe.com/).
2. Create a project or open an existing one.
3. Add **Adobe Admin APIs** to your project.
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

## Step 4: Testing Admin API endpoints

For quick testing and exploration, you can use the generated access token to authorize requests on the [Swagger UI](../../api/specification.md).

Here, you can interact with Admin API endpoints, including policy-related operations for admin users, to verify your setup and understand how the APIs work.

## Admin APIs: Policy management

To manage Admin policies in your organization, you can retrieve and update policies using the Admin APIs. Policies define rules such as data retention periods or content purging for inactive users.

### Policy object

The following policy objects are available:

- `policyType`: A string representing the type of policy (Example:  `inactive_user_content_purge`).  
- `attributes`: An object containing policy-specific settings, including:  
    o `enabled` (boolean): Whether the policy is active.  
    o `retention` (string, optional): Retention period in ISO 8601 format.

### Get policy details

Use the `GET Policy details` API to retrieve the details of a specific policy for your organization.

#### Request

```bash
curl -X GET \
    'https://dummy-link.com/v1/policies/org/inactive_user_content_purge' \
    -H 'accept: application/json' \
    -H 'x-request-id: 1234567890' \
    -H 'Authorization: Bearer YOUR_ACCESS_TOKEN_HERE'
```

Replace `YOUR_ACCESS_TOKEN_HERE` with a valid OAuth access v3 token.

#### Response

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

- `policyType`: The type of the policy
- `attributes.enabled`: Whether the policy is enabled (true) or disabled (false)
- `attributes.retention`: Retention period using ISO 8601 duration format (P2Y means 2 years)

### Update policy

Use a `PATCH request` to modify attributes of an existing policy.

#### Request

```bash
curl -X PATCH \
    'https://dummy-link.com/v1/policies/org/inactive_user_content_purge' \
    -H 'accept: application/json' \
    -H 'If-Match: "33a64df551425fcc55e4d42a148795d9f25f89d4", W/"0815"' \
    -H 'x-request-id: 1234567890' \
    -H 'Authorization: Bearer YOUR_ACCESS_TOKEN_HERE' \
    -H 'Content-Type: application/json-patch+json' \
    -d '[
        {
            "op": "replace",
            "path": "/attributes/enabled",
            "value": false
        },
        {
            "op": "remove",
            "path": "/attributes/retention"
        },
        {
            "op": "add",
            "path": "/attributes/retention",
            "value": "P2Y"
        }
    ]'
```

Replace `YOUR_ACCESS_TOKEN_HERE` with a valid OAuth access token.  
The If-Match header includes the ETag(s) for optimistic concurrency control.

#### Response

Sample response:

```json
{
    "policyType": "inactive_user_content_purge",
    "attributes": {
        "enabled": true,
        "retention": "PT5M"
    }
}
```
