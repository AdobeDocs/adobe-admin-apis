# Authentication setup

Learn how to authenticate requests to the Adobe Admin APIs.

## Overview

Every request made to Adobe Admin APIs must include an encrypted access token. Your secure, server-side application retrieves an access token by making a request to the [Adobe Identity Management System (IMS)](https://www.adobe.com/content/dam/cc/en/trust-center/ungated/whitepapers/corporate/adobe-identity-management-services-security-overview.pdf), using your **Client ID** and **Client Secret**.

## Prerequisites

This document assumes you have worked with your organization's **Administrator** and have the following:

- A user account with a **Developer** role authorized for an Adobe product that uses **Enterprise Storage**. This grants access to the [Adobe Developer Console](https://developer.adobe.com/).
- An [Adobe Developer Console project](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) configured with either **OAuth server-to-server** or **OAuth user authentication** credentials for the Adobe Cloud Storage and Collaboration APIs.
- Access to your **Client ID** and **Client Secret** from the **Adobe Developer Console** project. Securely store these credentials and never expose them in client-side or public code.

For more information about setting up an Adobe Developer Console project, see [Adobe Developer Console](https://developer.adobe.com/).

## Authentication Types

The Adobe Admin APIs support Server-to-Server authentication using OAuth Server-to-Server credentials. This authentication method is designed for different use cases, depending on whether your application acts independently or on behalf of a user.

For a detailed comparison and implementation guidance, refer to [Adobe Developer Authentication Guide](https://developer.adobe.com/developer-console/docs/guides/authentication/).

### Server-to-Server Authentication

Use **Server-to-Server authentication** if your application needs to execute actions on Adobe cloud storage content without involving a user.

#### Retrieve a Server-to-Server access token

Perform the following steps:

1. Open a secure terminal and export your **Client ID** and **Client Secret** as environment variables:

    ```sh
    export ADOBE_ADMIN_CLIENT_ID=yourClientIdAsdf123
    export ADOBE_ADMIN_CLIENT_SECRET=yourClientSecretAsdf123
    ```

2. Run the following command to generate an access token:

    ```sh
    curl --location 'https://ims-na1.adobelogin.com/ims/token/v3' \
      --header 'Content-Type: application/x-www-form-urlencoded' \
      --data-urlencode 'grant_type=client_credentials' \
      --data-urlencode "client_id=$ADOBE_ADMIN_CLIENT_ID" \
      --data-urlencode "client_secret=$ADOBE_ADMIN_CLIENT_SECRET" \
      --data-urlencode 'scope=openid, AdobeID, creative_sdk, adobe_admin_api'
    ```

   A sample response is as follows:

   ```json
   {
    "access_token": "yourAccessTokenAsdf123",
    "token_type": "bearer",
    "expires_in": 86399
   }
   ```

   The `expires_in` field indicates the token’s validity in seconds, typically, 24 hours. Your application should securely store the token and refresh it before expiration.

3. Export your access token as an environment variable:

    ```sh
    export ADOBE_ADMIN_ACCESS_TOKEN=yourAccessTokenAsdf123
    ```

## Technical Account Permissions

When using **OAuth Server-to-Server authentication**, all API requests are executed through a **Technical Account**. This account is automatically created when you configure **Server-to-Server authentication** in your **Adobe Developer Console** project.

However, to enable access to Adobe cloud storage content, you must explicitly grant permissions to the **Technical Account**.

Granting permissions to the **Technical Account** is done through the **Adobe Admin Console**.

> **Note:** You must be an **Administrator** for your organization to grant permissions to the **Technical Account**.

For step-by-step instructions, refer to the [Technical Account setup guide](#).
