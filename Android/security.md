* [Permissions](https://developer.android.com/privacy-and-security/security-tips#permission-definitions): Android's documentation advice to not use permissins
in for interacting with `BroadcastReceiver`s, `Service`s, `ContentProvider`s, basically when doing any IPC, because it can be confusing to users. But if you
still need to use a custom permission then, declare it in the app manifest using the `<permission>` element(in the app providing exposing the IPC). Apps
calling to the IPC can reference the new permission by adding a `<uses-permission>` element in their manifest files. You can also add permissions dynamically
by using the `addPermission()` method.

* `checkCallingPermission` or `checkCallingOrSelfPermission`: First you should know that often times you need to perform some IPC, in Android you can do that
using `Service`s, `BroadcastReceiver`s, `IBinder`, `Messenger`, `Intent`, as declared [here](https://developer.android.com/privacy-and-security/security-tips#interprocess-communication).
If your IPC is accessible to other applications, you can apply a security policy by using the `<permission>` element you can restrict the use of the component, that means
filtering out/in intents(which is API you use to inform the system you want to launch a service/broadcasr receiver) that can execute your service(any exposed IPC)
for this you usually create a custom permission, and here is where we use the functions we are talking about, they helps us check if the permissions match
before executing any code on behalf the callee process. However it is said that this approach is not bullet proof and it can be Hijacked, so if the IPC is between apps
you own and are signed with the same key, use a `signature-level` permission in the `android:protectionLevel`. The functions in question are used to check if
processes calling a service are authorized to perform the work. Again, custom permissions are not bulletproof, for example if you use `android:protectionLevel="normal"`
or omit the attribute, any malicious app can request and receive the custom permission automatically, hence, completely bypassing your IPC security or an app can be installed
before yours and if it declares a permission with an identical name, the security boundary can be spoofed or subverted.

* [Content Providers](https://developer.android.com/privacy-and-security/security-tips#content-providers): Content providers can provide more granular access by declaring
the `android:grantUriPermissions` attribute and using the `FLAG_GRANT_READ_URI_PERMISSION` and `FLAG_GRANT_WRITE_URI_PERMISSION` flags in the `Intent` object that activates
the component. The scope of these permissions can be further limited by the `<grant-uri-permission>` element. 

* [WebView Security](https://developer.android.com/privacy-and-security/security-best-practices#webview): If possible use `myWebView.createWebMessageChannel` to
create `WebMessagePort`, these allow both native and JS send messages to ports and listen to onmessage events, however, they can only pass string data (no direct
binary payload support), however a more modern solution is use `WebViewCompat.addWebMessageListener`. Check "How Do You Use WebMessagePort As An Alternative
to addJavascriptInterface()?" in StackOverflow for an explanation on how to use `WebMessagePort` and/or check this [implementation sample](https://github.com/commonsguy/cw-omnibus/tree/master/WebKit/SensorPort).
Another way to interface between the app and the WebView is `WebView.addJavascriptInterface`, it injects a Java or Kotlin object directly into the WebView's
JavaScript context. JavaScript can call methods on this object synchronously or asynchronously as if it were a local JS object. For JS to
be able to call a method must be annotated with `@JavascriptInterface`. Since the app cannot easily verify which frame or origin inside the WebView triggered
the method this solution is considered somewhat risky if used in not tursted content, so use it only if necessary and in trusted and in sites you control, but
in this case and almost always apps shouldn't let users navigate to sites that are outside of your control. Whenever possible, use an allowlist to restrict the
content loaded by your app's WebView objects. In addition, never enable JavaScript interface support unless you completely control and trust the content in your 
app's WebView objects

* **SSL Pinning:**  You can do SSL pinning using different methods, OkHttp let's you set SSL pinning by client but you can do it app-wide by addin network security
configurations as stated [here](https://developer.android.com/privacy-and-security/security-best-practices#network-security-config)

* [Share Dara Securely Across Apps](https://developer.android.com/privacy-and-security/security-best-practices#permissions-share-data): If you need to share data
such as having a PDF app open a PDF your app owns, grant one time access to the opening app only, also, use `content://` URIs, not `file://` URI

* **AI Risk Assessment:** A great way to mitigate AI risks in practice is using industry tools like the [SAIF Risk Self-Assessment](https://saif.google/risk-self-assessment)
to better understand and mitigate risks. Also check ["Mitigate AI rIsk in your app"](https://developer.android.com/privacy-and-security/risks/ai-risks/risks-mitigations)

* [Mitigate security risks in your app](https://developer.android.com/privacy-and-security/risks): Documentation offers us a list of common security risks separated
by categories which include: Storage, Cryptography, Network Communication, Platform Interaction, Code Quality

* [Encrypt Plaint Text With KeyStore](https://developer.android.com/privacy-and-security/risks/hardcoded-cryptographic-secrets): You can use keystor to ecnrypt plain
text, you could use this in combination with Datastore to store auth tokens safely, or to do End-to-End or Hybrid encryption in network communications. This is a concept
based on Java Encryption, so learn more about Java Keystore in [this](https://youtu.be/NH49dTEYPg0?si=sS4dlTBXeikHq6aL) series. A very interesting concept is that java
has different keystore file formats to create the a keystore file, the most secure file format, as far as I know, PKCS12. However there is something even more secure
called PKCS11, this is an API interface used to talk to physical or remote hardware security unit, this is backed by hardware security module(HSM), basically this is a
hardware bridge and is possible by specifying a configuration file, it can connect directly to a HSM module or through a native .so (Linux) or .dll (Windows) library.
As long as that driver file exposes a standard C interface, Java does not care whether the backend is hardware or software. This is what Android keystore does using
trusted execution environment(TEE) or SE(Secure Element)

* **Cryptography**: We have symmetric and asymmetric keys, asymmetric encryption solves the key-distribution problem (is more secure against key-interception risks
because the private key is never shared), whereas symmetric encryption (such as AES-256) actually offers higher mathematical strength per bit than standard asymmetric
algorithms (such as RSA-2048), they basically have different roles and in practice can not substitute each other, rather, they work together, neither is ideal on its
own because they’re just impractical or limited in each other’s roles. TLS/SSL secure communications using HTTPS uses both, it does hybrid encryption. You can also do
hybrid encryption at the application-layer or message-level for encrypting payloads on top of TLS/SSL, this approach is used in apps that require even more secure
communications because it protects against man in the middle attacks, which could succeed if an attacker gets to bypass TLS with a proxy using a certificate that the
user's device trusts, in this context hybrid encryption guarantees that the body of the message is encrypted all the way down to the server application, this matters
because because load balancers, CDNs, API gateways and reverse proxies decrypt TLS (they are known as TLS terminators), and the content would be vulnerable when
traveling between those and the actual server application consuming the data. Asymmetric keys can sometimes be called private keys/key pairs, private keys and key pairs
concepts are very related because, a key-pair consists of a private and a public key, the public key is generated from the private key, if the public key is lost for
any reason it can be just extracted from the private key again, a pure key-pair is used in things like SSH connections, they authenticate the client and the server. You
could use them to encrypt a text but symmetric keys are preferred for doing this because they're faster and less resource consuming when encrypting texts. The most
common use case for asymmetric keys is in HTTPS communications, we can generate a TLS/SSL certificate using a private key, that private key is used to create a
certificate signing request(CSR), the CSR is signed with your private key and contains the public key and your identity, this CSR is then signed by issuer(CA) which
generates the actual certificate, but they can be self signed, or as I already mentioned, we can request a certificate authority to sign our certificate. Both self
signed and signed by a CA certificates can act on behalf of a certificate authority, a CA can not exist without a certificate which is always a self signed certificate,
this certificate is the root certificate, intermediate certificates can issue leaf certificates by signing CSRs on behalf of the CA, this is only possible if the self
signed certificate or intermediate certificate was issued with the `basicConstraints: CA:TRUE` extension. If you don't create a self signed certificate with that extension
then you would use it for getting HTTPS communications in development environments or in internal server communications. A chain of certificates is a concept that exists
due to this parent-child relationship between root and intermediate certificates, intermediate with other intermediate certificates, and an intermediate or root and leaf
certificate.

* Java Criptography Architecture Engine Classes And Algorithms: In [this](https://docs.oracle.com/en/java/javase/27/security/java-cryptography-architecture-jca-reference-guide.html#GUID-A7EEDE25-C4C0-4C28-94EA-262858AE9212)
guide we learn that engine classes provide the interface to a specific type of cryptographic service, independent of a particular cryptographic algorithm or provider.
They can either provide cryptographic operations (for example, encryption, digital signatures, and message digests), or provid generators or converters of cryptographic
material (keys and algorithm parameters), or provide objects (keystores or certificates) that encapsulate the cryptographic data and can be used at higher layers of
abstraction. Lets define some of them that are of particular interest to me in the context of Android development:

  * SecureRandom: Used to generate random or pseudo-random numbers.
  * Cipher: Initialized with keys, these used for encrypting/decrypting data. There are various types of algorithms: symmetric bulk encryption (for example, AES), asymmetric encryption (for example, RSA), and password-based encryption (for example, PBE). There exists two types of ciphers, block and stream ciphers. Block ciphers process entire blocks at a time, usually many bytes in length. If there is not enough data to make a complete input block, the data must be padded: that is, before encryption, dummy bytes must be added to make a multiple of the cipher's block size. These bytes are then stripped off during the decryption phase. The padding can either be done by the application, or by initializing a cipher to use a padding type such as "PKCS5PADDING". In contrast, stream ciphers process incoming data one small unit (typically a byte or even a bit) at a time. This allows for ciphers to process an arbitrary amount of data without padding. When encrypting using a simple block cipher, two identical blocks of plaintext will always produce an identical block of cipher text, if an attacker notices breaking repeated ciphertext is easier, this is why you'd want to use cipher modes which alterates the output block, to do this you pass an initial value to the first block, this is known as an Initialization Vector(IV). THe IV simply altera the data before encryption. IV should be random and doesn't need to be protected or kept secret. Available modes are CBC, CFB, OFB, and more. You get an instance of a cipher using the factory method `Cipher.getInstance`, you pass it a transformation which is a string indicating its characteristics, it can be `"algorithm/mode/padding"` or `"algorithm"`. The objects returned by factory methods are uninitialized, and must be initialized before they become usable. In case of Cipher, it needs to be initialized for one of four modes, `ENCRYPT_MODE`, `DECRYPT_MODE`, `WRAP_MODE`, `UNWRAP_MODE`. The same parameters that were used for encryption must be used for decryption. Data can be encrypted or decrypted in one step (single-part operation `doFinal`) or in multiple steps (multiple-part operation `update` which must be terminated by one of the these `doFinal` or `doFinal(byte[], int)` ). A multiple-part operation is useful if you do not know in advance how long the data is going to be, or if the data is too long to be stored in memory all at once. `Cipher.getOutputSize` method can be used to determine how big the output buffer should be.
  * KeyPairGenerator: Used to generate a new pair of public and private keys suitable for use with a specified algorithm. 
  * KeyGenerator: Used to generate new secret keys for use with a specified algorithm. There are two ways to generate a key: in an algorithm-independent manner, and in an algorithm-specific manner. The only difference between the two is the initialization of the object
  * KeyStore: Used to create and manage a keystore. A keystore is a database of keys. Private keys in a keystore have a certificate chain associated with them, which authenticates the corresponding public key. A keystore also contains certificates from trusted entities.

  You can find the algorithms that each engine class supports [here](https://docs.oracle.com/en/java/javase/27/docs/specs/security/standard-names.html). 

* [Biometric Authentication](https://developer.android.com/identity/sign-in/biometric-auth):

* **Trusted CA and SSL Pinning:**  Some apps choose to limit the set of certificates they accept by either limiting the set of CAs they trust or by certificate pinning.
You can limit or add CAs in your app as explained [here](https://developer.android.com/privacy-and-security/security-config#CustomTrust). Certificate pinning is done by
providing a set of certificates by hash of the public key (SubjectPublicKeyInfo of the X.509 certificate). A certificate chain is then valid only if the certificate
chain contains at least one of the pinned public keys. In android you can configure them using [this](https://developer.android.com/privacy-and-security/security-config#CertificatePinning)
guide
