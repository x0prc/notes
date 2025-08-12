---
dg-publish: true
permalink:
---






- aka **==Secure Socket Layer (SSL)==** is the workhorse of internet security.
    - TLS protects connections between servers and clients.

## ==Target Applications and Requirements==

- The primary driver for creating TLS was to **==enable secure browsing in applications.==**
- Also helps to protect internet-based communication in general by establishing a secure channel between a client and a server that ensures the ==**data transferred is confidential, authenticated, and unmodified.**==
- TLS defeats man-in-the-middle attacks by authenticating servers (and optionally clients) **==using certificates and trusted certificate authorities.==**

## ==TLS Protocol Suite==

- TLS usually sits between the transport protocol TCP and an ==**application layer protocol such as HTTP or SMTP, in order to secure data transmitted over a TCP connection.**==
- Can also work over the ==**User Datagram Protocol (UDP) transport protocol**==, which is used for “connectionless” transmissions such as voice or video traffic.

## ==TLS in a Nutshell==

- The ==**record protocol**== defines a packet format to encapsulate data from higher-level protocols and sends this data to another party.
- The **==handshake protocol==**—or just handshake—is TLS’s key agreement protocol.
    - The handshake is started by a client to initiate a secure connection with a server.
    - Once both the client and the server have processed each other’s messages, they’re ready to exchange encrypted data using session keys established through the handshake

### ==Certificates and Certificate Authorities==

- The certificate validation step, wherein a server uses a certificate to authenticate itself to a client
- For example :
    - certificate 0 is the one received by [google.com](http://google.com/) ,
    - certificate 1 belongs to the entity that signed certificate 0,
    - and certificate 2 belongs to the entity that signed certificate 1.
    - The organization that issued certificate 2 (GeoTrust) granted permission to Google Internet Authority to issue a certificate (certificate 1) for the domain name [www.google.com](http://www.google.com/), thereby transferring trust to Google Internet Authority.

## ==The Record Protocol==

- Communications is transmitted as sequences of ==**TLS records**==, the data packets used by TLS.
- Is essentially a transport protocol, agnostic of the transported data’s meaning; **==this is what makes TLS suitable for any application.==**

### ==Structure of TLS Record==

- TLS record is a chunk of data of at most 16 kilobytes, structured as follows :
    - The first byte represents the type of data transmitted and is set to the **==value 22 for handshake data, 23 for encrypted data, and 21 for alerts.==**
        - In the TLS 1.3 specifications, this value is called ==**_ContentType._**==
    - The second and third byte are set to 3 and 1, respectively. These bytes are fixed for historical reasons and are not unique to TLS version 1.3.
        - In the specifications, this 2-byte value is called _**==ProtocolVersion.==**_
    - The fourth and fifth bytes encode the length of the data to transmit as a **==16-bit integer, which can be no larger than 2^14 bytes (16KB).==**
    - The rest of the bytes are the data to transmit **==_(also called the payload)_==**, of a length equal to the value encoded by the record’s fourth and fifth bytes.

### ==Nonces==

- The nonces ==**used to encrypt and decrypt TLS records**== are derived from 64-bit sequence numbers, maintained locally by each party, and incremented for each new record.
- TLS records don’t specify the nonce to be used by the authenticated cipher.

### ==Zero Padding==

- Zero Padding mitigates traffic analysis attacks.
    - Traffic analysis is a method that attackers use to extract information from traffic patterns using timing, volume of data transferred, and so on.
- Zero padding adds zeros to the plaintext in order to inflate the cipher-text’s size, ==**and thus to fool observers into thinking that an encrypted message is longer than it really is.**==

  

![Screenshot_2023-08-16_at_5.10.34_PM.png](/img/user/img/Screenshot_2023-08-16_at_5.10.34_PM.png)

## ==Cryptographic Algorithms==

- TLS 1.3 uses authenticated encryption algorithms,
    - a key derivation function (a hash function that derives secret keys from a shared secret),
    - as well as a Diffie–Hellman operation.
- TLS 1.3 supports only three algorithms:
    
    1. AES-GCM,
    2. AES-CCM (a slightly less efficient mode than GCM),
    3. and the ChaCha20 stream cipher combined with the Poly1305 MAC.
    
    - The secret key can be either 128 bits (AES-GCM or AES-CCM) or 256 bits (AES-GCM or ChaCha20-Poly1305).