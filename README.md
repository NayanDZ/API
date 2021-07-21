# 4-API/Web Services

## API

- Application Programming Interface (API) is a software intermediary that allows your applications to communicate with one another. 
It provides routines, protocols, and tools for developers building software applications, while enabling the extraction and sharing of data in an accessible manner.

- Content formats of API is JSON, XML, plain text, JPEG, PDF etc.

## Web Services     

- A web service is software composed of standardized XML messaging system.
- The benefit of web services are since all of its communication is in XML, they are not restricted to any operating system or programming languages
- Web services are built on top of open standards such as XML, Java, HTTP, TCP/IP.
 
## API vs Web Services 

Majorly two types of services used in the development environment REST and SOAP.

1. SOAP (Simple Object Access Protocol) is an XML-based messaging protocol for exchanging information among computers. 
SOAP’s built-in WS-Security standard uses XML Encryption, XML Signature, and SAML tokens to deal with transactional messaging security considerations.
- Web services depends on:
  - XML: to tag the data (as markup and syntax)
  - SOAP(Simple Object Access Protocol): to transfer a message
  - WSDL(Web Services Description Language): to describe the availability of service
  - UDDI (Universal Description, Discovery and Integration): Registry service is a Web service that manages information about service providers, service   implementations, and service metadata
- Test cases to find in web services:
  - Fuzzing
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

2. REST (Representational State Transfer) uses HTTP to obtain data and perform operations on remote computer systems. It supports SSL authentication and HTTPS to achieve secure communication.

   REST uses the JSON standard


## Tools for performing VAPT
   - SoapUI
   - Postman
   - Burp Suite

## API security best practices

1. Authentication
2. Data Encoding
3. Access
4. API Request (Input)
5. Cryptography
6. Processing
7. API Response (Output)
   - Set " X-Frame-Options: DENY " header
   - Set " X-Content-Type-Options: nosniff " header
   - Set " Content-Security-Policy: default-src 'none' " header
   - Remove Fingerprinting headers:
     - X-Powered-By , X-AspNet-Version, Server, etc.
   - Force content-type for response. If you return application/json content then your content-type response is application/json.
   - Don't return sensitive: Credentials, Passwords, Server IP, Internal Path, security tokens and Users PAN or BANK details.
   - Return the proper status code according to the API output.
     - HTTP defines the status code in every response in REST application do not use only 200 for success and 404 for error, there is a list of codes defined for HTTP using of these in REST API is enforced.  

