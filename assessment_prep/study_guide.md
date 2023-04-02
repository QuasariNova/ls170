# The Internet
## Have a broad understanding of what the internet is and how it works ([What is the Internet?](https://launchschool.com/lessons/4af196b9/assignments/268243e5)) ([Protocols](https://launchschool.com/lessons/4af196b9/assignments/a53e65ce)) ([A Layered System](https://launchschool.com/lessons/4af196b9/assignments/21ef33af))

## Understand the characteristics of the physical network, such as latency and bandwidth ([The Physical Network](https://launchschool.com/lessons/4af196b9/assignments/097d7577))

## Have a basic understanding of how lower level protocols operate ([A Layered System](https://launchschool.com/lessons/4af196b9/assignments/21ef33af))
### Ethernet ([The Link/ Data Link Layer](https://launchschool.com/lessons/4af196b9/assignments/81df3782))
### IP ([The Internet/ Network Layer](https://launchschool.com/lessons/4af196b9/assignments/b222ecfb))

## Know what an IP address is and what a port number is ([The Internet/ Network Layer](https://launchschool.com/lessons/4af196b9/assignments/b222ecfb)) ([Communication Between Processes](https://launchschool.com/lessons/2a6c7439/assignments/41113e98))

## Have an understanding of how DNS works ([Book: Background](https://launchschool.com/books/http/read/background#howtheinternetworks))

## Understand the client-server model of web interactions, and the role of HTTP as a protocol within that model ([Some Background and Diagrams](https://launchschool.com/lessons/cc97deb5/assignments/586769d9))

# TCP & UDP
## Have a clear understanding of the TCP and UDP protocols, their similarities and differences ([Transmission Control Protocol (TCP)](https://launchschool.com/lessons/2a6c7439/assignments/d09ddd52)) ([User Datagram Protocol (UDP)](https://launchschool.com/lessons/2a6c7439/assignments/9bb82c9b))

## Have a broad understanding of the three-way handshake and its purpose ([Transmission Control Protocol (TCP)](https://launchschool.com/lessons/2a6c7439/assignments/d09ddd52))

## Have a broad understanding of flow control and congestion avoidance ([Transmission Control Protocol (TCP)](https://launchschool.com/lessons/2a6c7439/assignments/d09ddd52))

# URLs
## Be able to identify the components of a URL, including query strings ([Book: What is a URL?](https://launchschool.com/books/http/read/what_is_a_url)) ([URLs](https://launchschool.com/lessons/cc97deb5/assignments/a28ccb6f))

http://www.example.com:88/home?item=book

The parts of a URL are:
- The scheme (ex http) indicates the protocol used to access the resource.
- The host (ex www.example.com) tells the client where the resource is hosted.
- The port (ex :88), is required if you want to use  aport other than default.
- The path (ex /home) shows what local resource is being requested.
- The query string (ex ?item=book) is used to send data to the server.

  Query Parameters are the key value pairs included in the query string(key=value). & is used to separate different key value pairs. URL Encoding is used for characters that are reserved or not ascii

## Be able to construct a valid URL ([Book: What is a URL?](https://launchschool.com/books/http/read/what_is_a_url)) ([URLs](https://launchschool.com/lessons/cc97deb5/assignments/a28ccb6f))

URL must include scheme and host. Path is needed for resources outside of default and query string is needed for sending data. Finally, the port is only needed if you aren't using the default port for the scheme(html is 80, htmls is 443).

## Have an understanding of what URL encoding is and when it might be used ([Book: What is a URL?](https://launchschool.com/books/http/read/what_is_a_url#urlencoding))

URLs only accept certain characters from the 128-character ASCII character set. Reserved or unsafe ASCII characters, as well as characters not in the set, have to be encoded. You do so by replacing the non-conforming characters with a `%` followed by two hexadecimal digits that represent a UTF-8 character.

UTF-8 uses 1-4 bytes to represent every character, so you might need to have up to four `%FF` sequences.

Characters must be encoded if:
1. They have no corresponding character in the standard ASCII set.
2. The use of the character is unsafe. `%` is used on other characters, quotation marks, `#`, brackets, and `~` all are unsafe too.
3. If the character is reserved for special use within the URL. `/`, `?`, `:`, `@`, and `&` are reserved.

# HTTP and the Request/Response Cycle
## Be able to explain what HTTP requests and responses are, and identify the components of each ([Book: Making HTTP Requests](https://launchschool.com/books/http/read/making_requests)) ([Book: Processing Responses](https://launchschool.com/books/http/read/processing_responses))

## Be able to describe the HTTP request/response cycle ([Book: Making HTTP Requests](https://launchschool.com/books/http/read/making_requests)) ([Book: Processing Responses](https://launchschool.com/books/http/read/processing_responses)) ([The Request Response Cycle](https://launchschool.com/lessons/cc97deb5/assignments/83ae67aa))

## Be able to explain what status codes are, and provide examples of different status code types ([Book: Processing Responses](https://launchschool.com/books/http/read/processing_responses#statuscode))

The `status code` is a three-digit number that the server sends with its response to a request, signifying the status of the request. `status text` is added to the `status code` to provide a description of the code.

| Status Code | Status Text | Meaning |
|:---:|:---:|:---:|
| 200 | OK | The request was handled successfully. |
| 302 | Found | The requested resource has changed temporarily. Usually results in a redirect to another URL. |
| 404 | Not Found | The requested resource cannot be found. |
| 500 | Internal Server Error | The server has encountered a generic error. |

## Understand what is meant by 'state' in the context of the web, and be able to explain some techniques that are used to simulate state ([Book: Stateful Web Applicaitons](https://launchschool.com/books/http/read/statefulness))

HTTP is a stateless protocol. State refers to a website being able to change and remember a users actions.

We can do this by using Sessions, Cookies, and/or Asynchronous JavaScript calls.

### Sessions

### Cookies

### Asynchronous JavaScript calls(AJAX)

## Explain the difference between GET and POST, and know when to choose each
### GET Requests ([Book: Making Requests](https://launchschool.com/books/http/read/making_requests#get))

`GET` requests are used to request resources. Typically, clicking a link on a webpage or typing an address in the address bar of your browser produce `GET` requests.

`GET /tiger.html HTTP/1.1`

### POST Requests ([Book: Making Requests](https://launchschool.com/books/http/read/making_requests#post))

`POST` requests are used to send data to the server or initiate some action on the server.

`POST /new_player HTTP/1.1` Would have info in body of request.

# Security
## Have an understanding of various security risks that can affect HTTP, and be able to outline measures that can be used to mitigate against these risks ([Book: Security](https://launchschool.com/books/http/read/security))

### Session Hijacking

Session Hijacking is where an attacker gets ahold of your session id and uses it to impersonate you to the server.

Countermeasures for it include:
- Resetting Sessions. Every successful login renders an old session invalid and creates a new one. By forcing authentication when entering any potentially sensitive area, you cut off the jacked session id.
- Setting an expiration time for sessions. This does not allow an attacker infinite time to pose as the real user.
- HTTPS

#### HTTPS
HTTP is inherently unsafe due to it being a text based protocol. All of its data is sent with plaintext and if someone were to use packet sniffing techniques, they can read all the data sent between you and the server.

This is dangerous because if someone got ahold of your session id, they could impersonate you to the server.

Secure HTTP(HTTPS) helps solve session hijacking by using TLS to encrypt every HTTP request/response preventing others from easily reading the data contained.

#### Same-origin policy
The same-origin policy permits any interaction between resources that come from the same origin, but restricts certain interactions between resources originating from different origins.

An origin is the combination of scheme, host, and port.

This helps prevent websites from attacking each other. This keeps your server from sending importent session information to an origin other than itself.

### Cross-Site Scripting (XSS)

Cross Site scripting is where a server allows users to input HTML or JavaScript that ends up being displayed by the site directly. If the input isn't sanitized, users will be able to inject code into the page contents and the browser will execute it.

Some ways of preventing this are:
- Sanitize user input by elimanating problematic input, or by disallowing HTML and JavaScript input altogether.
- Escape all user input data when displaying it. By escaping special characters that would be interpretted as HTML, you prevent the browser from executing it and instead display it as plain text.

## Be aware of the different services that TLS can provide, and have a broad understanding of each of those services ([The Transport Layer Security (TLS) Protocol](https://launchschool.com/lessons/74f1325b/assignments/83bf156b))

Transport Layer Security is a Session layer protocol used to provide Encryption, Authentication, and Integrity to a TCP connection.

### Encryption ([TLS Encryption](https://launchschool.com/lessons/74f1325b/assignments/54f6defc))

TLS sets up an encrypted connection by performing a TLS handshake.

1. `ClentHello` message will be sent after TCP `ACK`. This message contains the maximum version of TLS the client can support along with a list of Cipher Suites that the client can use.
2. The server responds with a `ServerHello` message, which chooses a TLS version and which Cipher Suite to use along with its certificate. It also sends a `ServerHelloDone` marker to indicate that this step is done.
3. The client will then intiate the key exchange process. It does this by generating a 'pre-master secret', which it then encrypts using the server's public key and sends it to the server. The server decrypts this using its private key.
4. Both the client and server will use the 'pre-master' secret to generate the same symmetric key using the chosen Cypher Suite.
5. The client having already sent the `ClientCipherSpec` flag with its `ClientKeyExchange` message, will now receive a message from the server with the `ChangeCipherSpec` and `Finished` flags, which indicate that the TLS Handshake is done.
6. The client and server now communicate using the symmetric key for encryption.

In short, the TLS handshake agrees which version of TLS to establish a secure connection, agree with which algorithm to use to generate the key, and using the public key of the server communicate the necessary information to generate the symmetric key which will be used to communicate with going forward.

### Authentication ([TLS Authentication](https://launchschool.com/lessons/74f1325b/assignments/95e698ab))

As part of the TLS handshake, the server will send its certificate. This certificate can be used to authenticate that the client is actually talking to the server it thinks it is.

- The server sends its certificate
- The server creates a 'signature' which is just some data that is encrypted with the server's private key.
- The signature is transmitted in a message along with the unencrypted data that was encrypted.
- The client, decrypts using the public key from the certificate and checks that the data is the same.

Certificates are verified by a signature from a Certificate Authority, which is verified by a Root Certificate Authority. This all works due to Chain of Trust, that only these CAs can sign these certifactes and that they verified the identity of the certificate holder before they issued the certificate.

### Integrity ([TLS Integrity](https://launchschool.com/lessons/74f1325b/assignments/a88271cf))

TLS provides integrity by providing a Message Authentication Code inside its Protocol Data Unit. The Message Authentication Code is a digest that was created from the data payload prior to encryption. When the client receives the data, after they have decrypted the data they then generate the same digest and check that they are the same.

By doing this it confirms that the message sent was not tampered with as any tampering would generate a different digest.
