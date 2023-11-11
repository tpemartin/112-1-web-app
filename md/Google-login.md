# Concept

> You may need to update your `react` package through

To use Google Login in your web app, you would first need to set it up using Google's OAuth2.0. The general flow is:

1. The user logs in using their Google account through your app.
2. Google returns an access token to the app.
3. The app sends this token to the backend server.
4. The server verifies this token with Google's servers.
5. If the token is verified, the server checks if the user's email is in the specified group of emails.
6. If the email is in the group, the server returns a positive response to the app.

Here is a simplified example of how you might implement this in Node.js using the Google APIs client library.

```javascript
const { OAuth2Client } = require('google-auth-library');
const client = new OAuth2Client(CLIENT_ID);

async function verify(token) {
  const ticket = await client.verifyIdToken({
      idToken: token,
      audience: CLIENT_ID,
  });
  const payload = ticket.getPayload();
  const userid = payload['sub'];
  return payload;
}

app.post('/api/verify', (req, res) => {
  const token = req.body.token;
  verify(token).then(payload => {
    const userEmail = payload['email'];
    const allowedEmails = ['allowedemail1@gmail.com', 'allowedemail2@gmail.com']; // Your list of allowed emails
    if (allowedEmails.includes(userEmail)) {
      res.status(200).send('Email is in the specified group.');
    } else {
      res.status(403).send('Email is not in the specified group.');
    }
  }).catch(error => {
    res.status(401).send('Unauthorized');
  });
});
```

In the code above, replace `CLIENT_ID` with your Google API client ID. This code assumes you're using Express.js for your server and that the client sends the Google access token in a POST request to `/api/verify`.

Please note that this is a simplified example. In a production environment, you should add proper error handling, secure your routes, and avoid hard-coding sensitive data. Consider using environment variables for storing sensitive data such as the `CLIENT_ID` and the list of allowed emails.

# React implementation

<https://blog.logrocket.com/guide-adding-google-login-react-app/>

# Server-side flow

<https://developers.google.com/identity/sign-in/web/server-side-flow>

# React implementation (deprecated)

To implement Google Login in a React app, you can use "react-google-login", a third-party package that simplifies the process. Here are the steps:

1. First, install the package using npm:

```bash
npm install react-google-login
```

2. Then, use the package in your React component like so:

```jsx
import React from 'react';
import { GoogleLogin } from 'react-google-login';

const responseGoogle = (response) => {
  console.log(response);
  // you can see the Google's response in the console, it includes a lot of information, but the most important is the tokenId
}

const App = () => {
  return (
    <div>
      <GoogleLogin
        clientId="YOUR_CLIENT_ID.apps.googleusercontent.com" // replace with your client id
        buttonText="Login with Google"
        onSuccess={responseGoogle}
        onFailure={responseGoogle}
        cookiePolicy={'single_host_origin'}
      />
    </div>
  );
}

export default App;
```

In this example, replace `YOUR_CLIENT_ID` with your actual client ID from Google. The `responseGoogle` function will receive the Google user's information once they've successfully logged in.

Remember, the `response` object contains the user's `tokenId`. You can send this `tokenId` to your server for further verification as described in the previous response.