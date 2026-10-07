
* **Hybrid Encryption:** Https uses hybrid encryption by default, it is all handled by the http client library you're using, if you're doing it manually like if you're implementing
your own http client you may need to handle the whole process yourself which includes the process for creating hybrid encryption, but before it happens there is one or two more steps
like coordinating between the client and the server what algorithm and cypher suite is going to be used to do asymetric encryption, after that the handshake happens, I actually don't
know the process by heart but what I want to explain is that, 1) https uses hybrid encryption, that means that, both, the client and the server have both an asymetric
key pair(private and public) and one of them, usually the client will generate a symetric key, then the server and client will exchange public keys, and the one that generated the
symetric key will use the other end's asymmetric public key to encrypt the symmetric key that it just generated, it will send that key to the other end, the other end then will be
able to decrypt the other's end symetric key using it's own private key, so the symmetric key has been transmitted securly and both ends can use it to encrypt and decrypt messages,
the purpose of using the symmetric key even if it is less secure is that it is more efficient, encrypting and decrypting using an asymmetric key is more expensive than using a
symmetric key. However we should know that Https only provides TLS, that means is only secure in the transport layer, what does it mean? for the client side it may mean nothing as
the traffic it receives is directly arriving and directly leaving to and from its hardware to the backend, however, the backend can face another challenge, depending on its
infrastructure it will first hit a proxy or a load balancer, and either one of these two will actually decrypt the bytes and then forward the decrypted bytes to your application server
and this can be considered a security breach, there is different ways to solve it, one way is to configure hybrid encryption at the application level.
