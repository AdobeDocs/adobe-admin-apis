# Getting started with Adobe Admin APIs

Adobe Admin APIs provide enterprise organizations with programmatic control over administrative tasks in the Adobe Admin Console, enabling them to integrate Adobe's administrative capabilities into their workflows, scripts, and tools to automate administrative processes.

With the Adobe Admin APIs, you can:

Configure and manage Content Retention Policies for inactive users to define how inactive users' assets (stored in Adobe Cloud Storage) are preserved or permanently deleted when accounts are deactivated.

## Prerequisites

Before you can use the Adobe Admin APIs, you must use the [Adobe Developer Console](https://developer.adobe.com/) to create a development project. The integration registers your application as a client of the Adobe Admin API, and gives you the credentials you need to authorize calls to the API.

For information on setting up an **Adobe Developer Console** project, see [Developer Console](./console.md).

For information about client credential authentication and retrieving Client ID, Client Secret, Scopes, or access tokens, see [Authentication Setup](./authentication.md).

## Make your first API call

Once you have created your access token, you can follow the steps below to make your first API call.

1. Open your terminal and paste the code below.
2. Replace the variables `<YOUR_ACCESS_TOKEN>` with the token you generated on the **Adobe Developer Console**.
3. Once all variables have been replaced, you can run the command.

```bash
curl --request GET \
    --url 'https://cloudstorage.adobe.io/v1/policies/inactive_user_content_purge' \
    --header 'Authorization: Bearer <YOUR_ACCESS_TOKEN>' \
    --header 'Content-Type: application/vnd.adobecloud.directory+json'
```

Congratulations! You have just made your first request to the Adobe Admin API.

## Deepen your understanding

Explore the [Working with Adobe Admin APIs](../quick-start/index.md) tutorial for a working example of the Adobe Admin API's capabilities.

See the [API Reference](https://dummy-link-to-api-reference.com) for details about the Adobe Admin API functions.
