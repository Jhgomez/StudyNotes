* `checkCallingPermission` or `checkCallingOrSelfPermission`: First you should know that often times you need to perform some IPC, in Android you can do that
using Services, Broadcast Receivers, IBinder, Messenger, Intent, as declared [here](https://developer.android.com/privacy-and-security/security-tips#interprocess-communication).
If your IPC is accessible to other applications, you can apply a security policy by using the `<permission>` element you can restrict the use of the component, that means
filtering out/in intents(which is API you use to inform the system you want to launch a service/broadcasr receiver) that can execute your service(any exposed IPC)
for this you usually create a custom permission, and here is where we use the functions we are talking about, they helps us check if the permissions match
before executing any code on behalf the callee process. However it is said that this approach is not bullet proof and it can be Hijacked, so if the IPC is between apps
you own and are signed with the same key, use a `signature-level` permission in the `android:protectionLevel`. The functions in question are used to check if
processes calling a service are authorized to perform the work. Again, custom permissions are not bulletproof, for example if you use `android:protectionLevel="normal"`
or omit the attribute, any malicious app can request and receive the custom permission automatically, completely bypassing your IPC security or an app can install
before yours declaring a permission with an identical name, the security boundary can be spoofed or subverted.
