
* **Hybrid Encryption:** Https uses hybrid encryption by default, it is all handled by the http client library you're using(In my case as an android developer I know Okhttp will
handle this process for me, all I need to tell it is to use the `https` scheme), if you're doing it manually like if you're implementing your own http client you may need to handle
the whole process yourself which includes the process for creating hybrid encryption, but before it happens there is one or two more steps like coordinating between the client and
the server what algorithm and cypher suite is going to be used to do asymetric encryption, after that the handshake happens, I actually don't know the process by heart but what I
want to explain is that, 1) https uses hybrid encryption, that means that, both, the client and the server have both an asymetric key pair(private and public) and one of them,
usually the client will generate a symetric key, then the server and client will exchange public keys, and the one that generated the symetric key will use the other end's asymmetric
public key to encrypt the symmetric key that it just generated, it will send that key to the other end, the other end then will be able to decrypt the other's end symetric key using
it's own private key, so the symmetric key has been transmitted securly and both ends can use it to encrypt and decrypt messages, the purpose of using the symmetric key even if it is
less secure is that it is more efficient, encrypting and decrypting using an asymmetric key is more expensive than using a symmetric key. However we should know that Https only
provides TLS, that means is only secure in the transport layer, what does it mean? for the client side it may mean nothing as the traffic it receives is directly arriving and directly
leaving to and from its hardware to the backend, however, the backend can face another challenge, depending on its infrastructure it will first hit a proxy or a load balancer, and
either one of these two will actually decrypt the bytes and then forward the decrypted bytes to your application server and this can be considered a security breach as they will be
transmmited as plain text, there is different ways to solve it, one way is to configure hybrid encryption at the application level. However at this point even if we had this
configurations all set up in an Android application we would still be vulnerable to MITM attacks, but why?, thing is that a bad actor could install a tool like Charles Proxy to
catch your communications, the only thing it needs to do is to add Charles Proxy Root Certificate to the device and then its certificate will be trusted and it will be able to
read all the messages between our cellphones and the backend, in theory you could intercept all communications meaning that in the initial messages the proxy would return a fake
public key, then the client uses that public key to encrypt it's symmetric key and then sent it but now charles proxy can decrypt that message using its private key, and therefore
decrypt subsequent messages. How can we solve this? We can do dynamic or static SSL pinning, you can do static SSL pining in different ways, but you will be required to embed
some content in your app (actually dynamic pinning will also requiere this), you could embed the raw public certificate that the server will respond with in its handshake, in
android using Okhttp you would use the function `sslSocketFactory`, but a more modern approach to static SSL pinning is using the public certificate hascode(SHA-256), thing is
To get a TLS certificate signed by a CA, you first generate a key pair (public and private key). You then create a certificate signing request (CSR), which contains your public
key and your identity information, signed with your private key to prove ownership. You send the CSR to the CA, which verifies your identity (or control of the domain), then issues
a certificate: your public key and identity, signed by the CA's private key. The server then uses the certificate together with its private key, which never left the server, to
establish TLS connections. BTW a key pair can be reused, I.e when the certificate has expired we can reuse the key pair to create a new CSR, rotating the key pair is considered a
best practice however there are use cases where rotating keys can introduce availability issues, I'll explain why in a moment. But this is only if you're doing it manually. If
you're hosting your server in behind cloudflare, then Cloudflare can give you a certificate. if you have a VPS in a cloud provider then you can install Certbot ACME and it will
generate the certificates for you. At this point we have encrypted communications in the transport and application layers, yet we are vulnerable to MITM attacks. So how can we
avoid these attacks?, again, there is different ways to do this. One way is, if we have control over the public key that is linked to the certificate a server is using then we s
hould know that a the public key is associated with a hash (SHA-256), we can embed that hash in our app and continue reusing the public key when creating a new certificate, this
way the http client can know that a certificate is valid, avoiding MITM attacks, this is known as static SSL pinning, but there is another way of doing static pinnig, and it is
instead of embedding the hash we embed the certificate or the public key, either one s fine, however  since the public key can be reused to generate a certificate (its hash
can be implicitly reused also) we could benefit from this flexibility instead of embedding the certificate which would force us to update our app's binary whenever the certificate
is changed. It also exist dynamic SSL pinning, in which ceritificates are set at runtime as they are downloaded form the network, however any pin delivered over the network needs
its own trust anchor, or a proxy could swap it. Real dynamic pinning bottoms out in something static: the pin list is signed, and the app has a hardcoded verification key to
check the signature, or the pin list is fetched over a connection protected by a static pin. There is another way to protect our app against these attacks and that is specify
a trusted certificate autorithy, by default apps will trust any cetificate generated by a list of certificate authorities, that list lives in the operating system itself and
is what a proxy uses to intercept our traffict and look legal, however if our binary specifies its own list of CAs then we are efficiently excluding any other CAs a bad acto
might have installed in the device, in Android we can declare a CA using Okhttp which exludes other CAs only from the instance of a client, but other traffic in the app using
the system's tursted CAs would be valid, however we can declare that at the app level using a seurity config and pass it to the manifest and in this case we wouldn't need to
do SSL pinning.
