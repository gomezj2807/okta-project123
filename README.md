# Cruise0 React JS test app integrated with Auth0

## Documentation
Quickstart : https://auth0.com/docs/quickstart/spa/react

## Installation

Using npm

### `npm install @auth0/auth0-react'

## Configure Auth0
Create a Single Page Application in the Auth0 Dashboard : https://manage.auth0.com

If you're using an existing application, verify that you have configured the following settings in your Single Page Application:

* Click on the "Settings" tab of your application's page.
* Scroll down and click on the "Show Advanced Settings" link.
* Under "Advanced Settings", click on the "OAuth" tab.
* Ensure that "JsonWebToken Signature Algorithm" is set to RS256 and that "OIDC Conformant" is enabled.

Next, configure the following URLs for your application under the "Application URIs" section of the "Settings" page:

* Allowed Callback URLs: http://localhost:3000
* Allowed Logout URLs: http://localhost:3000
* Allowed Web Origins: http://localhost:3000
These URLs should reflect the origins that your application is running on. Allowed Callback URLs may also include a path, depending on where you're handling the callback.

Take note of the Client ID and Domain values under the "Basic Information" section. You'll need these values in the next step.

## Configure the SDK

Configure the SDK
Configure the SDK by wrapping your application in Auth0Provider:
```ruby
// src/index.js
import React from 'react';
import { createRoot } from 'react-dom/client';
import { Auth0Provider } from '@auth0/auth0-react';
import App from './App';

const root = createRoot(document.getElementById('app'));

root.render(
  <Auth0Provider
    domain="YOUR_AUTH0_DOMAIN"
    clientId="YOUR_AUTH0_CLIENT_ID"
    authorizationParams={{
      redirect_uri: window.location.origin,
    }}
  >
    <App />
  </Auth0Provider>
);
```
For more code samples on how to integrate auth0-react SDK in your React application, have a look at our examples here: https://github.com/auth0/auth0-react/blob/main/EXAMPLES.md


