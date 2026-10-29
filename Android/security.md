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


* [Biometric Authentication](https://developer.android.com/identity/sign-in/biometric-auth):

* **Trusted CA and SSL Pinning:**  Some apps choose to limit the set of certificates they accept by either limiting the set of CAs they trust or by certificate pinning.
You can limit or add CAs in your app as explained [here](https://developer.android.com/privacy-and-security/security-config#CustomTrust). Certificate pinning is done by
providing a set of certificates by hash of the public key (SubjectPublicKeyInfo of the X.509 certificate). A certificate chain is then valid only if the certificate
chain contains at least one of the pinned public keys. In android you can configure them using [this](https://developer.android.com/privacy-and-security/security-config#CertificatePinning)
guide
