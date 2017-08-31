## OAuth 2
- OAuth 2 is an authorization framework that enables applications to obtain limited access to user accounts on an HTTP service, such as Facebook, Google, Github etc.
- OAuth 2 works over HTTP and authorizes Devices, APIs, Servers and Applications with access tokens rather than credentials. 
- Although there are two versions of OAuth (OAuth 1.0a and OAuth2). OAuth2 is more popular and most widely used.

### The Authorization Code Grant
1. The authorization code OAuth grant type is meant to be used on web servers, where the code is not public.
2. The developer will register himself with the API server(Authentication server eg:Facebook) and will receive **client-id** and **client-secret**.
3. When a user visits your website and wants to login using third-party identinty, they will be redireced to *Identity Providers* website.  
`https://login.identity_provider.com/oauth?response_type=code&client_id=xxx&redirect_uri=xxx&state=xxxx`
4. They will then use their credentials to login to *Identity Providers* website, and will be prompted to accept certain permissions.
5. Once they accept those permissions, they will be redired back to your website along with an authorization code.  
`https://yoursite.com/state=xxx&code=xxx`
6. You will then use this **authorization code**, your **client-id** and **client-secret** to request the ****access token from the identity provider’s API.  
`POST https://api.identity_provider.com/oauth/token?grant_type=authorization_code&code=xxx&redirect_uri=xxx&client_id=xxx&client_secret=xxx`
7. This **access token** can be used to request user information(for which the user granted permissions) from the Identity Provider.

### The Implicit Grant Type
1. As Implicit grants doesn’t require you to store any secret key information, thus it is ideal for client-side web applications and mobile apps.
2. It is similar to *Autherization Grant Type* but in this case the Authorization server 
will directly send the **access-token** in the response to first request.  
`https://login.identity_provider.com/oauth?response_type=token&client_id=xxx&redirect_uri=xxx&state=xxxx`
3. This **access token** can be used to request user information(for which the user granted permissions) from the Identity Provider.

### The Password Credentials Grant Type
1. The password credentials grant type is meant to be used for first class web applications OR mobile applications.
2. You will accept username and password form user and POST them to your identity service to receive the access token.  
`POST https://login.identity_provider.com/oauth/token?grant_type=password&username=xxx&password=xxx&client_id=xxx`
3. This **access token** can be used to request user information(for which the user granted permissions) from the Identity Provider.

### The Client Credentials Grant Type
1. The client credentials grant type is meant to be used for application code(eg: how many users have logged into your service).
2. Your application makes a request to the identity provider’s API service using it’s application credentials.  
`POST https://login.identity_provider.com/oauth/token?grant_type=client_credentials&client_id=xxx&client_secret=xxx`
3. You’ll then receive an access token in the response which you can use to make real API calls to retrieve information from the identity provider’s API service.
