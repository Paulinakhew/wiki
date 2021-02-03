# OAuth

These notes have been taken from [this](https://www.oauth.com/oauth2-servers/getting-ready/) free book.

## Background

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

## 1. Getting Ready

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

