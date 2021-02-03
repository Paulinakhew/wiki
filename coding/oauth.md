# OAuth

These notes have been taken from [this](https://www.oauth.com/oauth2-servers/getting-ready/) free book.

Tools:

* [Github's API](https://docs.github.com/en/rest)

## [Background](https://www.oauth.com/oauth2-servers/background/)

* before OAuth, you would give a third-party application your password and allow it to act as you
* problems that would arise:
  * applications would store users' passwords in plain text, making them a target for harvesting passwords
  * applications can change the user's password through their account
  * you can only revoke access by changing your password, something that users are typically reluctant to do
* services began to implement things similar to OAuth 1.0
  * e.g. FlickrAuth by Flickr, AuthSub by Google, BBAuth by Yahoo, etc.
  * wide variety of solutions that were incompatible and failed to address certain security considerations
* Blaine Cook, chief architect at Twitter wanted a better authentication method for the Twitter API
* > We want something like Flickr Auth / Google AuthSub / Yahoo! BBAuth, but published as an open standard, with common server and client libraries, etc.  
  > - Blaine Cook, April 5, 2007
* the solution was OAuth 1
* OAuth 2.0 was created to be simpler and less confusing than OAuth 1
  * many use cases, such as mobile applications, could not use OAuth 1
* due to disagreements on fundamental issues between the web and enterprise contributors, the standard was pulled into separate documents
* if someone wants to implement OAuth 2.0 for their web service, they need to synthesize information from a number of different sources
* implementers need to:
  * read RFCs
  * read drafts
  * decide which token types and grant types to support
  * decide token string size
  * read security guidance and cautions in the document
  * understand the implications of the decisions they have to make
* most web services that use OAuth come to the same decisions, resulting in very similar OAuth 2.0 APIs
* this book is a guide to building OAuth 2.0 APIs, with recommendations based on a majority of the live implementations

## [1. Getting Ready](https://www.oauth.com/oauth2-servers/getting-ready/)

* every OAuth service requires you register a new application by signing up as a developer with the service

### Creating an Application

* registration process involves creating an account on the service's website and entering basic information about the application \(name, website, logo, etc.\)
* after registering the application, you receive a `client_id` and sometimes a `client_secret` to use when the app interacts with the service
* you have to register one or more redirect URLs the application will use
  * these are where the OAuth service will return the user to after they have authorized the application
  * these have to be registered otherwise you can create malicious applications that steal user data

### Redirect URLs and State

* OAuth APIs will only redirect users to a registered URL to prevent redirection attacks
  * redirection attacks are where an authorization code/access token is intercepted by an attacker
* redirect URL must be an https endpoint
  * if it is not https, an attacker may be able to intercept the authorization code and use it to hijack a session
* redirect URL validation must be an exact match
  * `https://example.com/auth` would not match `https://example.com/auth?destination=account`
* avoid query string parameters in your redirect URL



* the "state" parameter can be used to encode application state
  * must include random data if you're not including [PKCE](https://www.oauth.com/oauth2-servers/pkce/) parameters in the request
* a string value that is passed into OAuth and is returned after the user authorizes the application
* e.g. you could encode a redirect URL in a JWT and parse it after the user is redirected to the appropriate location in your application

## [2. Accessing Data in an OAuth Server](https://www.oauth.com/oauth2-servers/accessing-data/)

* how to access your data at an existing OAuth 2.0 server
* this chapter covers how to use the GitHub API to build an application that lists all repositories the logged-in user has created

### [2.1 Create an Application](https://www.oauth.com/oauth2-servers/accessing-data/create-an-application/)

* create an application on GitHub to get the client ID and client secret
* fill out the required information, including the callback URL
* after completing the form you'll see your client ID and secret
  * client ID is public information used to build authorized URLs
    * can be included in the JavaScript source code of a web page
  * client secret **must** be kept confidential

### [2.2 Setting up the Environment](https://www.oauth.com/oauth2-servers/accessing-data/setting-up-the-environment/)

> Note: as the linked website has all of the code, I will simply paraphrase what needs to be done and paste the final code snippet at the end of Chapter 2.

* create a method that is a simple wrapper around cURL
  * includes `Accept` and `User-Agent` headers that are required by GitHub's API
  * decodes the JSON response
  * if we have an access token, it will send the proper OAuth header with the access token
* set up variables needed for OAuth, such as the `client_id`, `client_secret`, `authorized_url`, `base_url`, `token_url`, etc. 
  * this varies by application
* set up `logged_in` and `logged_out` views to show whether the user is logged in or logged out
  * `logged_out` view should contain a link to the login URL to start the OAuth process

### [2.3 Authorization Request](https://www.oauth.com/oauth2-servers/accessing-data/authorization-request/)

* add `?action=login` in the query string to start the OAuth process
* create a list of parameters that contain `state` to protect the client
  * state is a random string that the client generates and stores in the session
  * when GitHub sends the user back with the state, we can verify that we initiated the request
* other parameters can include:
  * `response_type` 
  * `client_id`
  * `redirect_uri`
  * `scope`
* send the user to the authorization URL
* user will see GitHub's OAuth authorization prompt
* after the user approves the request, they will be redirected back to our page with `code` and `state` parameters
* next step: exchange authorization code for an access token

### [2.4 Obtaining an Access Token](https://www.oauth.com/oauth2-servers/accessing-data/obtaining-an-access-token/)

* `state` parameter is the same one we set in the initial authorization request
  *  app should check that it matches to prevent attacks
* send a request to GitHub's token endpoint to exchange the authorization code for an access token
* request contains:
  * public `client_id`
  * private `client_secret`
* if the request is successful, GitHub will return an access token
  * we store the access token in the session and redirect to the home page, where the user is logged in
* response from GitHub will look like 

```text
{
  "access_token": "e2f8c8e136c73b1e909bb1021b3b4c29",
  "token_type": "Bearer",
  "scope": "public_repo,user"
}
```

* code will extract the access code and save it in the session
* next time the user visits the page, they will still be logged in

### [2.5 Making API Requests](https://www.oauth.com/oauth2-servers/accessing-data/making-api-requests/)

* the app can use the access token to make API requests
* in this case, the code will use the access token to list the user's repositories and link to each one
* that's it!

### PHP Code

```text
<?php
// Fill these out with the values you got from Github
$githubClientID = '';
$githubClientSecret = '';

// This is the URL we'll send the user to first to get their authorization
$authorizeURL = 'https://github.com/login/oauth/authorize';

// This is the endpoint our server will request an access token from
$tokenURL = 'https://github.com/login/oauth/access_token';

// This is the Github base URL we can use to make authenticated API requests
$apiURLBase = 'https://api.github.com/';

// The URL for this script, used as the redirect URL
$baseURL = 'https://' . $_SERVER['SERVER_NAME'] . $_SERVER['PHP_SELF'];

// Start a session so we have a place to store things between redirects
session_start();


// Start the login process by sending the user
// to Github's authorization page
if(isset($_GET['action']) && $_GET['action'] == 'login') {
  unset($_SESSION['access_token']);

  // Generate a random hash and store in the session
  $_SESSION['state'] = bin2hex(random_bytes(16));

  $params = array(
    'response_type' => 'code',
    'client_id' => $githubClientID,
    'redirect_uri' => $baseURL,
    'scope' => 'user public_repo',
    'state' => $_SESSION['state']
  );

  // Redirect the user to Github's authorization page
  header('Location: '.$authorizeURL.'?'.http_build_query($params));
  die();
}


if(isset($_GET['action']) && $_GET['action'] == 'logout') {
  unset($_SESSION['access_token']);
  header('Location: '.$baseURL);
  die();
}

// When Github redirects the user back here,
// there will be a "code" and "state" parameter in the query string
if(isset($_GET['code'])) {
  // Verify the state matches our stored state
  if(!isset($_GET['state'])
    || $_SESSION['state'] != $_GET['state']) {

    header('Location: ' . $baseURL . '?error=invalid_state');
    die();
  }

  // Exchange the auth code for an access token
  $token = apiRequest($tokenURL, array(
    'grant_type' => 'authorization_code',
    'client_id' => $githubClientID,
    'client_secret' => $githubClientSecret,
    'redirect_uri' => $baseURL,
    'code' => $_GET['code']
  ));
  $_SESSION['access_token'] = $token['access_token'];

  header('Location: ' . $baseURL);
  die();
}


if(isset($_GET['action']) && $_GET['action'] == 'repos') {
  // Find all repos created by the authenticated user
  $repos = apiRequest($apiURLBase.'user/repos?'.http_build_query([
    'sort' => 'created',
    'direction' => 'desc'
  ]));

  echo '<ul>';
  foreach($repos as $repo) {
    echo '<li><a href="' . $repo['html_url'] . '">'
      . $repo['name'] . '</a></li>';
  }
  echo '</ul>';
}

// If there is an access token in the session
// the user is already logged in
if(!isset($_GET['action'])) {
  if(!empty($_SESSION['access_token'])) {
    echo '<h3>Logged In</h3>';
    echo '<p><a href="?action=repos">View Repos</a></p>';
    echo '<p><a href="?action=logout">Log Out</a></p>';
  } else {
    echo '<h3>Not logged in</h3>';
    echo '<p><a href="?action=login">Log In</a></p>';
  }
  die();
}


// This helper function will make API requests to GitHub, setting
// the appropriate headers GitHub expects, and decoding the JSON response
function apiRequest($url, $post=FALSE, $headers=array()) {
  $ch = curl_init($url);
  curl_setopt($ch, CURLOPT_RETURNTRANSFER, TRUE);

  if($post)
    curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($post));

  $headers = [
    'Accept: application/vnd.github.v3+json, application/json',
    'User-Agent: https://example-app.com/'
  ];

  if(isset($_SESSION['access_token']))
    $headers[] = 'Authorization: Bearer ' . $_SESSION['access_token'];

  curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);

  $response = curl_exec($ch);
  return json_decode($response, true);
}
```

### Additional Resources

I coded [this](https://github.com/Paulinakhew/playlist_generator) project that uses OAuth to create a new Spotify playlist, which you can access from [here](https://create-spotify-playlist.herokuapp.com/).

### 3. Signing in with Google



