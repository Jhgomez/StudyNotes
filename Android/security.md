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

* [Biometric Authentication](https://developer.android.com/identity/sign-in/biometric-auth):

* **Trusted CA and SSL Pinning:**  Some apps choose to limit the set of certificates they accept by either limiting the set of CAs they trust or by certificate pinning.
You can limit or add CAs in your app as explained [here](https://developer.android.com/privacy-and-security/security-config#CustomTrust). Certificate pinning is done by
providing a set of certificates by hash of the public key (SubjectPublicKeyInfo of the X.509 certificate). A certificate chain is then valid only if the certificate
chain contains at least one of the pinned public keys. In android you can configure them using [this](https://developer.android.com/privacy-and-security/security-config#CertificatePinning)
guide
