![cas-vs-saml-vs-oauth2](https://user-images.githubusercontent.com/96379191/158010491-c1629915-988a-4a4d-845d-9b091bf2d080.png)


## SAML

### The SAML Authentication workflow

1. An end user clicks on the “Login” button on a file sharing service at example.com. The file sharing service at example.com is the Service Provider, and the end user is the Client.
2. To authenticate the user, example.com constructs a SAML Authentication Request, signs and optionally encrypts it, and sends it directly to the IdP. The IdP verifies the received SAML Authentication Request and, if valid, presents a login form for the end user to enter their username and password.
3. The Service Provider redirects the Client’s browser to the IdP for authentication. Once the Client has successfully logged in, the IdP generates a SAML Assertion (also known as a SAML Token), which includes the user identity (such as the username entered before), and sends it directly to the Service Provider.
4. The IdP redirects the Client back to the Service Provider.
5. The Service Provider verifies the SAML Assertion, extracts the user identity from it, assigns correct permissions for the Client and then logs them into the service.

![Screenshot 2022-03-12 at 4 33 27 PM](https://user-images.githubusercontent.com/96379191/158010586-a5615658-82c6-4e4d-81e2-23fb78438855.png)

### The OAuth workflow

Critically, OAuth doesn’t assume that the Client is a web browser.

The example workflow proceeds now as follows:

1. An end user clicks on the “Login” button on a file sharing service at example.com. The file sharing service at example.com is the Resource Server, and the end user is the Client.
2. The Resource Server presents the Client with an Authorisation Grant, and redirects the Client to the Authorisation Server
3. The Client requests an Access Token from the Authorisation Server using the Authorisation Grant Code
4. The Client logs in to the Authorisation Server, and if the code is valid, the Client gets an Access Token that can be used request a protected resource from the Resource Server
5. After receiving a request for a protected resource with an accompanying Access Token, the Resource Server verifies the validity of the token directly with the Authorisation Server
6. If the token was valid, the Authorisation Server sends information about the Client to the Resource Server

![Screenshot 2022-03-12 at 4 34 17 PM](https://user-images.githubusercontent.com/96379191/158010613-83578bb0-c5d2-43c9-b422-1ebef89d4e35.png)

