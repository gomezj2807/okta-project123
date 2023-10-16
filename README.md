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

## Add Login to Your Application
The Auth0 React SDK gives you tools to quickly implement user authentication in your React application, such as creating a login button using the loginWithRedirect() method from the useAuth0() hook. Executing loginWithRedirect() redirects your users to the Auth0 Universal Login Page, where Auth0 can authenticate them. Upon successful authentication, Auth0 will redirect your users back to your application.
```ruby
import React from "react";
import { useAuth0 } from "@auth0/auth0-react";

const LoginButton = () => {
  const { loginWithRedirect } = useAuth0();

  return <button onClick={() => loginWithRedirect()}>Log In</button>;
};

export default LoginButton;
```

## Add Logout to Your Application
Now that you can log in to your React application, you need a way to log out. You can create a logout button using the logout() method from the useAuth0() hook. Executing logout() redirects your users to your Auth0 logout endpoint (https://YOUR_DOMAIN/v2/logout) and then immediately redirects them to your application.
```ruby
import React from "react";
import { useAuth0 } from "@auth0/auth0-react";

const LogoutButton = () => {
  const { logout } = useAuth0();

  return (
    <button onClick={() => logout({ logoutParams: { returnTo: window.location.origin } })}>
      Log Out
    </button>
  );
};

export default LogoutButton;
```

##Show User Profile Information
The Auth0 React SDK helps you retrieve the profile information associated with logged-in users quickly in whatever component you need, such as their name or profile picture, to personalize the user interface. The profile information is available through the user property exposed by the useAuth0() hook. Take this Profile component as an example of how to use it:
```ruby
import React from "react";
import { useAuth0 } from "@auth0/auth0-react";

const Profile = () => {
  const { user, isAuthenticated, isLoading } = useAuth0();

  if (isLoading) {
    return <div>Loading ...</div>;
  }

  return (
    isAuthenticated && (
      <div>
        <img src={user.picture} alt={user.name} />
        <h2>{user.name}</h2>
        <p>{user.email}</p>
      </div>
    )
  );
};

export default Profile;
```

For more code samples on how to integrate auth0-react SDK in your React application, have a look at our examples here: https://github.com/auth0/auth0-react/blob/main/EXAMPLES.md


