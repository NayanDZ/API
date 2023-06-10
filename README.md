# API/Web Services Security Testing
### [API Security Top 10 2023](https://owasp.org/www-project-api-security/) 
 https://apisecurity.io/encyclopedia/content/owasp/owasp-api-security-top-10.htm

## API (Application Programming Interface)

- API is a software intermediary that allows your applications to communicate with one another. 
- API: we have URI(Uniform Resource Identifier) by using we send request which is GET or POST.
- It provides routines, protocols, and tools for developers to building software applications, while enabling the extraction and sharing of data in an accessible manner.

- Content formats of API: JSON, XML, plain text, JPEG, PDF etc.

## Web Services     

- A web service is software composed of standardized XML messaging system.
- SOAP: We have to send WSDL which is in XML format.
- The benefit of web services are since all of its communication is in XML.
- Not restricted to any operating system or programming languages.

- Web services are built on top of open standards such as XML, Java, HTTP, TCP/IP.
 
## REST vs SOAP 

Majorly two types of services used in the development environment **REST** and **SOAP**.

***1. SOAP (Simple Object Access Protocol)*** is an XML-based messaging protocol for exchanging information among computers. 
SOAP’s built-in WS-Security standard uses XML Encryption, XML Signature, and SAML tokens to deal with transactional messaging security considerations.
- Web services depends on:
  - XML: to tag the data (as markup and syntax)
  - SOAP(Simple Object Access Protocol): to transfer a message
  - WSDL(Web Services Description Language): to describe the availability of service
  - UDDI (Universal Description, Discovery and Integration): Registry service is a Web service that manages information about service providers, service   implementations, and service metadata
- Test cases to find in web services (Threats):
  - XSS /SQLi/ Malformed XML
  - File Upload
  - Xpath Injection
  - XML Bomb (DoS)
  - Authentication based attacks
  - Replay attacks
  - Session fixation
  - XML Signature wrapping
  - Session timeout
  - Host Cipher Support/ Valid Certificate/ Protocol Support
  - Hashing Algorithm Support
  - Fuzzing

***2. REST (Representational State Transfer)*** uses HTTP to obtain data and perform operations on remote computer systems. It supports SSL authentication and HTTPS to achieve secure communication.

   REST uses the JSON standard


## ⚙️ Tools for performing VAPT
   - SoapUI
   - Postman
   - Burp Suite

## API security best practices

***1. Authentication***
   - Don't use Basic Auth. Use standard authentication instead (e.g. JWT, OAuth).
     - **Auth Strategies**
       - [Basic Authentication](https://roadmap.sh/guides/basic-authentication.png): String is encoded with Base64
       - [Session Based Authentication](https://roadmap.sh/guides/session-authentication.png)
       - [Token Based Authentication](https://roadmap.sh/guides/token-authentication.png)
         - [JWT-JSON Web Token](https://roadmap.sh/guides/jwt-authentication.png)
           -Use a random complicated key (JWT Secret) to make brute forcing the token very hard.
           -Don't extract the algorithm from the header. Force the algorithm in the backend (HS256 or RS256).
           -Make token expiration (TTL, RTTL) as short as possible.
           
         - [OAuth- Open Authentication](https://roadmap.sh/guides/oauth.png)
           -Always validate redirect_uri server-side to allow only whitelisted URLs.
           -Always try to exchange for code and not tokens (don't allow response_type=token).
           -Use state parameter with a random hash to prevent CSRF on the OAuth authentication process.
           
         - [SSO -- Single Sign-On](https://roadmap.sh/guides/sso.png)
         
   - Don't reinvent the wheel in Authentication, token generation, password storage. Use the standards.
   - Use Max Retry and jail features in Login.
   - Use encryption on all sensitive data.    

***2. Data Encoding***
   - JSON encoding preferred for the user-supplied data to prevent the arbitrary remote code execution and other attack types this can be done by using the JSON serializer.
   - XML encoding is another type of mechanism used to check the XML content sent to the browser is parse-able and does not contain XML injection. 


***3. Cryptography & Data Security***
   - Use HTTPS on server side to avoid MITM (Man in the Middle Attack).
   - Use HSTS header with SSL to avoid SSL Strip attack.
   - The TLS is properly implemented to avoid the network level attacks.
   - Web application must be secured with encryption methodologies in storing and accessing the data.
   - Limit requests (Throttling) to avoid DDoS / brute-force attacks.

***4. API Request (Input)***
   - Use the proper HTTP method according to the operation: GET (read), POST (create), PUT/PATCH (replace/update), and DELETE (to delete a record), and respond with 405 Method Not Allowed if the requested method isn't appropriate for the requested resource.
   - Validate content-type on request Accept header (Content Negotiation) to allow only your supported format (e.g. application/xml, application/json, etc.) and respond with 406 Not Acceptable response if not matched.
   - Validate content-type of posted data as you accept (e.g. application/x-www-form-urlencoded, multipart/form-data, application/json, etc.).
   - Validate user input to avoid common vulnerabilities (e.g. XSS, SQL-Injection, Remote Code Execution, etc.).
   - Don't use any sensitive data (credentials, Passwords, security tokens, or API keys) in the URL, but use standard Authorization header.
   - Use an API Gateway service to enable caching, Rate Limit policies (e.g. Quota, Spike Arrest, or Concurrent Rate Limit) and deploy APIs resources dynamically.
   - Using of Secure parsing methodologies for the XML based inputs in the application to avoid the attacks like XML External Entity injection.
   - While using HTTP Methods POST and PUT validate the content type of the request on the server side.

***5. Processing***
   - Protect all the endpoints behind authentication to avoid broken authentication process.
   - User own resource ID should be avoided. Use /me/orders instead of /user/654321/orders.
   - Don't auto-increment ID’s. Use UUID instead.
   - If you are parsing XML files, make sure entity parsing is not enabled to avoid XXE attack.
   - If you are parsing XML files, make sure entity expansion is not enabled to avoid Billion Laughs/XML bomb via exponential entity expansion attack.
   - Use a CDN for file uploads.
   - Dealing with huge amount of data, use Workers and Queues to process as much as possible in background and return response fast to avoid HTTP Blocking.
   - Do not forget to turn the DEBUG mode OFF.

***6. API Response (Output)***
   - Set " X-Frame-Options: DENY " header
   - Set " X-Content-Type-Options: nosniff " header
   - Set " Content-Security-Policy: default-src 'none' " header
   - Remove Fingerprinting headers:
     - X-Powered-By , X-AspNet-Version, Server, etc.
   - Force content-type for response. If you return application/json content then your content-type response is application/json.
   - Don't return sensitive: Credentials, Passwords, Server IP, Internal Path, security tokens and Users PAN or BANK details.
   - Return the proper status code according to the API output.
     - HTTP defines the status code in every response in REST application do not use only 200 for success and 404 for error, there is a list of codes defined for HTTP using of these in REST API is enforced.
       - 201 Created – Resource created.
       - 202 Accepted – Accepted for processing.
       - 400 Bad Request – Malformed request having a message body format error.
       - 401 Unauthorized – Wrong or no Authentication.
       - 403 Forbidden – Authentication succeeded but the user doesn’t have permission to access the resource
       - 405 Method Not Allowed – Unexpected HTTP method. 

### 🔗 Other Useful Links
[31 Tips — API Security & Pentesting](https://github.com/inonshk/31-days-of-API-Security-Tips)

