* **Prevent Binary from Being Modified**: An Android binary (such as an APK file or compiled DEX/native code) can be modified, though doing so requires reverse engineering
and re-signing the package. You can prevent your published Android app binary from being modified or tampered with by using GooglePlays builtin Automatic Protection and 
the Play Integrity API. Google Play Automatic Protection focuses on preventing unauthorized redistribution, repackaging, and sideloading. It verifies that the app comes
from the official Google Play Store. Google Play Integrity API assesses whether the app binary is genuine (installed by Google Play) and running on an untampered/locked 
device, this means that it helps you detect when your app is running on a rooted device and emulators, in theory this would help you protect against tools like frida
which actually doesn't modify the binary, instead it modifies the running process in memory of an app injecting Javascript in its memory, however in practice a bad actor
can use Magisk modules to trick Integrity's API to pass integrity checks and then use Frida. It said Google Play Integrity can help you block or restrict a rooted device
from using your app, but it does not guarantee 100% prevention on its own. In order to prevent code/process injection combine the Play Integrity API with local
root-detection libraries 
