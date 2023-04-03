# The Internet
## Have a broad understanding of what the internet is and how it works ([What is the Internet?](https://launchschool.com/lessons/4af196b9/assignments/268243e5)) ([Protocols](https://launchschool.com/lessons/4af196b9/assignments/a53e65ce)) ([A Layered System](https://launchschool.com/lessons/4af196b9/assignments/21ef33af))

The internet is a "network of networks." Any number of devices that are connected to communicate or exchange data is a network and the internet is a large amount of localized networks that use a series of routers to communicate with each other.

The internet itself is the infrastructure that makes up these networks and their interconnections along with the protocols they use to communicate.

The internet works by using a series of conceptual "layers" operating on top of one another. Each layer, from the physical devices all the way up to specific application protocols, facilitates a different part of network communication. Each layer itself having its own unit of data, or protocol data unit. Lower levels encapsulate higher levels data in their own protocol data unit.

## Understand the characteristics of the physical network, such as latency and bandwidth ([The Physical Network](https://launchschool.com/lessons/4af196b9/assignments/097d7577))

At the lowest level, we have the physical means of transmitting the data. This is your network cards, your wires, radio waves, light, etc... How the signal is made up is dependant on the medium of which it travels.

The characteristics of the physical network are latency and bandwidth, which come from the physical limitations of the infrastructure it self.

- Latency is the measure of time for data to get from one point to another. In otherwords it is a measure of delay.
  - Propagation delay - the time it takes for a message to travel from the sender to the recipient.
  - Transmission delay - the time it takes to push a message into its medium. So like transmit into the air with wifi, or the entire electrical signal being made in a wire.
  - Processing delay - the time it takes a router to process the packet header.
  - Queuing delay - The time data waits in a buffer until data can be processed.
  - Last-mile latency - the majority of the above delays happen at the network edges, where data is transmitted from the ISP to the local network as there are more frequent and shorter hops.
  -Round-trip Time(RTT) - The length of the time from the signal being sent to the acknoledgement of receipt being received.
- Bandwidth is the amount of data that can be sent along the physical infrastructure of a network for a particular unit of time.
  - Typically, bandwidth for a connection is the lowest amount along all hops over the entire connection.

## Have a basic understanding of how lower level protocols operate ([A Layered System](https://launchschool.com/lessons/4af196b9/assignments/21ef33af))
### Ethernet ([The Link/ Data Link Layer](https://launchschool.com/lessons/4af196b9/assignments/81df3782))
### IP ([The Internet/ Network Layer](https://launchschool.com/lessons/4af196b9/assignments/b222ecfb))

- Data Link/Link Layer - The datalink layer uses Ethernet as its protocol and is intended for local area network communication
  - Ethernet's Protocol Data Unit is frames.
  - Ethernet uses Multimedia Access Control(MAC) Addresses, which are burnt into the physical network adapter, which are a sequence of six two-digit hex numbers. Each MAC address should be unique.
  - Ethernet uses the MAC address of the sender and the receiver to send data over a local area network.
  - Is impractical for inter-network communication as MAC addressing is physical and does not follow a logical heirarchy, thus cant be broken down into sub-divisions.
  - A Frame encapsulates a Packet
- Network/Internet Layer - The Network layer uses the Internet Protocol(IP) as its protocol and is intended for inter-network communication.
  - IP uses a PDU called an IP Packet.
  - Packets have a header and a data payload.
  - Packets data payload usually encapsulates a TCP fragment or a UDP datagram.
  - Packet headers include some fields like Version, TTL, Protocol, Checksum, the Source Address, and IP address. It also has ID, Flags, and Fragment Offset for fragmenting large packets into multiple smaller ones to be reassembled at the destination.
  - IP uses IP addresses for addressing. IP addresses are unique, logical, and heirarchical.
  - Routers route IPs between networks by referencing routing tables.

## Know what an IP address is and what a port number is ([The Internet/ Network Layer](https://launchschool.com/lessons/4af196b9/assignments/b222ecfb)) ([Communication Between Processes](https://launchschool.com/lessons/2a6c7439/assignments/41113e98))

IP addresses are used by the Internet Protocol in order to address inter-network communication. They come in two flavors:
- IPv4 addresses are 32 bits in length and have four sections with numbers ranging from `0` to `255`. `192.168.1.0` is a network address, `192.168.1.255` is a broadcast address, while everything in between can be a device address.
- IPv6 has 128-bit addresses(eight 16 bit blocks). They are typically written with 8 blocks of four hexadecimal numbers. `2001:db8:3333:4444:5555:6666:7777:8888`

Port numbers are used by Transport layer protocols such TCP or UDP. Port numbers are an implementation of multiplexing, which tells the device which application the data received is for.
- 0-1023 = well-known ports.
- 1024-49151 = registered ports.
- 49152 - 65535 = dynamic or private ports, typically used for allocation on client as ephemeral ports.

If you have both an IP address and a port number, you have a socket. A socket is a communication end-point.

## Have an understanding of how DNS works ([Book: Background](https://launchschool.com/books/http/read/background#howtheinternetworks))

Domain Name System(DNS) is responsible for converting domain names to an IP address using a distributed database. Your client will consult a DNS when it needs to send data to a domain name and the DNS will give the client the IP tied to that domain name.

A device will cache DNS results in its DNS Cache.

## Understand the client-server model of web interactions, and the role of HTTP as a protocol within that model ([Some Background and Diagrams](https://launchschool.com/lessons/cc97deb5/assignments/586769d9))

In the client-server model, you have a client which will reach out and make requests of a server. The server is capable of receiving these requests and responding as needed.

- Web Server - serves staic resources
- Application Server - handles more complicated requests that require data processing.
- Data store - Storage construct that can save data for later retrieval and process.

# TCP & UDP
## Have a clear understanding of the TCP and UDP protocols, their similarities and differences ([Transmission Control Protocol (TCP)](https://launchschool.com/lessons/2a6c7439/assignments/d09ddd52)) ([User Datagram Protocol (UDP)](https://launchschool.com/lessons/2a6c7439/assignments/9bb82c9b))

- Transmission Control Protocol (TCP)
  - PDU is a Segment
  - Connection-oriented protocol
  - Establishes connection through the Three-way Handshake
    - Sender sends `SYN` segment
    - Receiver receives `SYN` and sends back `SYN ACK`
    - Sender receives `SYN ACK` and sends `ACK`
  - Provides reliability by In-order Delivery, error detection, and message acknowledgement and retransmission.
    - Each segment has a sequence number and acknowledgement number in its header in order to know what segments weren't received so that it can retransmit them.
    - Also has a checksum in the header for error detection
  - Provides Congestion Avoidance by using data loss as a feedback to avoid congestion and reduce the size of the transmission window.
  - Provides Flow Control by using the window field of the TCP header and defining a buffer size. This allows a sender to not overwhelm the receiver.
  - Latency overhead due to handshake process
  - Head-of-line blocking due to in-order delivery slowing connection when a segment is missing and needs retransmitted. Leads to queuing delay.
- User Datagram Protocol (UDP)
  - PDU is a Datagram
  - Connectionless protocol
  - Very simple header, just includes ports, checksum, and length.
  - Speed and flexibility is its main positives.
  - Does nothing about reliability by itself.
  - Great for applications that don't require reliability to be stable.


## Have a broad understanding of the three-way handshake and its purpose ([Transmission Control Protocol (TCP)](https://launchschool.com/lessons/2a6c7439/assignments/d09ddd52))

- Sender sends `SYN` segment
- Receiver receives `SYN` and sends back `SYN ACK`
- Sender receives `SYN ACK` and sends `ACK`

The handshake ensures both the sender and receiver can reach each other and establishes the connection. The sender can't send any application specific data until it sends its `ACK`, so there is round-trip latency which provides overhead. This gives them baseline in which they can now communicate and ensure each segment are delivered in order.

## Have a broad understanding of flow control and congestion avoidance ([Transmission Control Protocol (TCP)](https://launchschool.com/lessons/2a6c7439/assignments/d09ddd52))

Flow Control is a technique created to prevent a sender from overwhelming the receiver with data. It is implemented by the receiver telling the sender how much data it can handle in a particular time-frame through the use of a buffer.

Congestion Avoidance is a technique that is used to prevent overwheming a network. It is implemented in TCP by detecting how much data has been lost and adjusting the transmission window based on that data. The higher the loss, the lower the window, thus the less data transmitted at one time.

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

- HTTP Request is a text-based message sent from a client to a server in order to request something from a server, typically access to a resource
  - Request line
    - Method - what kind of request (EX: `GET` or `POST`)
    - Path - Path to resource
    - Version - version of HTTP to use
  - Headers
    - host (added in HTTP 1.1) denotes which host the request is being made for
    - `session id`, `keep-alive`, languages, etc...
  - Optional Body
    - Depends on the method
    - With `POST` it is the data being sent to server.
- HTTP Response is a text-based message sent from a server to a client that responds to a clients request.
  - Response line
    - Status Code - three digit number telling status of the request
    - Status Text - Short description of the status of the request
    - Version - HTTP Version of response
  - Optional Headers
    - encoding
    - name of server
    - redirect? using `Location` header with a `302` status
    - `content-type`
    - `content-length`
  - Optional Body contains the raw data from the requested resource

## Be able to describe the HTTP request/response cycle ([Book: Making HTTP Requests](https://launchschool.com/books/http/read/making_requests)) ([Book: Processing Responses](https://launchschool.com/books/http/read/processing_responses)) ([The Request Response Cycle](https://launchschool.com/lessons/cc97deb5/assignments/83ae67aa))

The HTTP Request/Response cycle describes the process in which a client requests something from a server and the server responds to the request made by the client.

1. Client makes a HTTP Request
2. Server processes the request, verifying session, loading any data and running any necessary code, etc...
3. Server sends HTTP Response
4. Client processes response. A browser would display it.

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

The server is able to send a session identifier to the client. This allows the client to send it back to the server during a request to maintain a sense of persistent connection between requests.

By using session identifiers it forces the server to inspect every request to see if a session id was included, if so it must also check if it is valid. The server also needs to retrieve session data based on the id as well as recreate the state from the data to send back as a response. This gives some overhead on processing requests, especially those with `session id`s.

### Cookies

Cookies are pieces of data that are sent from the server and stored on the client side. Cookies are compared with the server side session data to identify the current session. Cookies are how `session id`s are stored client side.

Cookies are set with the `set-cookie` response header.

### Asynchronous JavaScript calls(AJAX)

Asynchronous JavaScript and XML calls allow browsers to update parts of a web page without having to request the whole page each time. With AJAX, responses are processed by some callback. This is all usually done via some client-side JavaScript code.

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
