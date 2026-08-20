# 🔐 Android Security — Interview Preparation

«A practical Android interview guide covering the most commonly asked security concepts, explained in simple words + real-life examples.»

---

1. Secure Data Storage

❓ How do you securely store sensitive data in Android?

Sensitive information such as authentication tokens, encryption keys and personal information should not be stored as plain text.

Depending on the requirement, Android provides mechanisms such as:

- Android Keystore
- Encrypted storage
- Encrypted databases/files
- Secure token storage

The important rule is:

«Never store sensitive information in plain text if an attacker could access the device/app data.»

💡 Real-life example

A banking app should never store your login password like:

password = "MyPassword123"

Instead, sensitive credentials should be protected using appropriate Android security mechanisms.

🎯 Interview answer

«"For sensitive data, I avoid plain-text storage and use Android Keystore-backed encryption or encrypted storage depending on the use case."»

---

2. Android Keystore

❓ What is Android Keystore?

Android Keystore is a system that allows an application to generate and use cryptographic keys securely.

The important point is that the app doesn't need to directly handle the raw key material.

Keys can also be stored using hardware-backed security on supported devices.

💡 Real-life example

Think of Keystore like a bank locker.

You can ask the bank to use something inside the locker, but you don't necessarily walk around carrying the valuable item yourself.

Similarly, your app can ask Android to perform cryptographic operations using a protected key.

🎯 Interview answer

«"Android Keystore provides a secure way to generate and use cryptographic keys, with hardware-backed protection available on supported devices."»

---

3. Secure Token Storage

❓ How do you securely store access and refresh tokens?

Authentication tokens are sensitive because someone possessing a valid token may be able to access the user's account.

Avoid storing them in:

- Plain SharedPreferences
- Logs
- Hardcoded constants
- Unencrypted files

Use secure/encrypted storage, often backed by Android Keystore.

💡 Real-life example

A food delivery app stores a user's authentication token so they don't need to log in every time.

If that token is stolen, someone may be able to impersonate the user.

🎯 Interview answer

«"I store authentication tokens using encrypted storage and protect the encryption keys using Android Keystore."»

---

4. Hardcoded Secrets

❓ Why shouldn't you hardcode API keys or secrets in an Android app?

An APK can be reverse engineered.

Even if a secret is hidden inside:

const val API_KEY = "secret123"

an attacker may extract it from the APK.

💡 Real-life example

You publish your app with a database password inside the APK.

An attacker downloads the APK, decompiles it and discovers the password.

🎯 Interview answer

«"Anything shipped inside the APK should be considered potentially accessible to an attacker. Sensitive secrets should therefore live on a secure backend rather than inside the app."»

---

5. Biometric Authentication

❓ What is Biometric Authentication?

Biometric authentication allows users to authenticate using something such as:

- Fingerprint
- Face
- Other supported biometric methods

Android provides APIs for securely integrating biometric authentication.

💡 Real-life example

A banking app asks:

«"Authenticate with fingerprint to view your account."»

The user doesn't have to enter their password every time.

🎯 Interview answer

«"Biometric authentication allows users to authenticate using device-supported biometrics such as fingerprint or face."»

---

6. BiometricPrompt

❓ How does BiometricPrompt work?

"BiometricPrompt" is Android's API for displaying a standardized biometric authentication prompt.

Typical flow:

App
 ↓
BiometricPrompt
 ↓
User provides fingerprint/face
 ↓
Android verifies biometric
 ↓
Authentication result
 ↓
App continues

The application should not receive or store the user's actual biometric data.

💡 Real-life example

Your banking app doesn't receive your fingerprint image.

Android handles the biometric verification and simply tells the application whether authentication succeeded.

🎯 Interview answer

«""BiometricPrompt" provides a standard Android API for biometric authentication while keeping the actual biometric data protected by the system."»

---

7. Authentication vs Authorization

❓ What's the difference?

Authentication = Who are you?

Authorization = What are you allowed to do?

💡 Real-life example

You log into an admin dashboard.

Authentication:
"Are you Rehan?"

Authorization:
"Is Rehan allowed to delete users?"

🎯 Easy memory trick

«Authentication → Identity»

«Authorization → Permission»

---

8. HTTP vs HTTPS

❓ What's the difference between HTTP and HTTPS?

HTTP sends data without encryption.

HTTPS uses TLS encryption to protect communication.

HTTP
Client ────────────────> Server
        Plain communication

HTTPS
Client ════════════════> Server
        Encrypted communication

💡 Real-life example

If you're entering your banking credentials, you don't want someone monitoring the network to read them.

HTTPS encrypts the communication.

🎯 Interview answer

«"HTTPS is HTTP secured using TLS, providing encryption, authentication and integrity for network communication."»

---

9. How HTTPS Works

❓ How does HTTPS actually work?

At a high level:

1. Client connects to server
        ↓
2. Server provides certificate
        ↓
3. Client validates certificate
        ↓
4. TLS establishes secure keys
        ↓
5. Encrypted communication begins

After the secure connection is established, application data is encrypted.

💡 Real-life example

When your Android app calls:

https://api.example.com/user

the request travels through the network in encrypted form.

---

10. SSL/TLS

❓ What is SSL/TLS?

TLS stands for:

«Transport Layer Security»

It protects data transmitted over a network.

SSL is the older predecessor of TLS.

Today, modern systems primarily use TLS.

💡 Real-life example

When your Android app communicates with a server over HTTPS, TLS protects that communication from being easily read or modified by attackers.

🎯 Interview answer

«"TLS is the cryptographic protocol used by HTTPS to secure communication between the client and server."»

---

11. SSL/TLS Handshake

❓ What happens during an SSL/TLS handshake?

Simplified flow:

Client
  │
  │ ClientHello
  ↓
Server
  │
  │ ServerHello + Certificate
  ↓
Client
  │
  │ Certificate validation
  ↓
Secure key establishment
  │
  ↓
Encrypted communication

The exact handshake differs between TLS versions, but the basic goal is:

«Authenticate the server and establish secure cryptographic keys.»

💡 Real-life example

Before your banking app starts sending sensitive account information, the app and server establish a secure communication channel.

---

12. MITM Attack

❓ What is a Man-in-the-Middle attack?

A MITM attacker attempts to position themselves between the client and server.

Android App
     ↓
   Attacker
     ↓
   Server

The attacker attempts to intercept or manipulate communication.

💡 Real-life example

Imagine connecting to a malicious public Wi-Fi network at an airport.

An attacker controlling the network attempts to intercept communication between your phone and the server.

🎯 Interview answer

«"A MITM attack occurs when an attacker intercepts communication between two parties and potentially reads or modifies the data."»

---

13. Preventing MITM Attacks

❓ How do you prevent MITM attacks in Android?

Common protections include:

- Use HTTPS/TLS
- Validate server certificates
- Avoid accepting invalid certificates
- Use modern TLS versions
- Certificate pinning when appropriate
- Never blindly trust all certificates

🚫 Bad practice

// Trusting every certificate
// Extremely insecure

💡 Real-life example

A banking app should never accept an arbitrary certificate just because the connection is technically HTTPS.

🎯 Interview answer

«"I use HTTPS with proper certificate validation and, where appropriate, certificate pinning to reduce MITM risks."»

---

14. Certificate Pinning

❓ What is Certificate Pinning?

Certificate pinning means the app has an expected certificate or public-key identity for its backend.

During the connection, the app verifies that the server matches the expected identity.

💡 Real-life example

Imagine your app saying:

«"I only trust this specific identity for my banking server."»

Even if an attacker presents another certificate that is otherwise trusted by the device, the app can reject it if it doesn't match the pin.

🎯 Interview answer

«"Certificate pinning adds an additional trust check by restricting which server certificate or public key the app accepts."»

---

15. Network Security Configuration

❓ What is Network Security Configuration?

Android provides "network_security_config.xml" to configure network security policies.

For example, you can control:

- Cleartext traffic
- Trusted certificates
- Domain-specific network rules

💡 Real-life example

You might want production traffic to always use HTTPS while allowing HTTP only for a local development environment.

🎯 Interview answer

«"Network Security Configuration allows us to declaratively configure Android's network security policies."»

---

16. Cleartext Traffic

❓ What is cleartext traffic?

Cleartext traffic means communication without encryption, such as HTTP.

HTTP → Cleartext
HTTPS → Encrypted

Android allows developers to control whether cleartext traffic is permitted.

💡 Real-life example

If your production app communicates with:

http://api.example.com

an attacker monitoring the network may potentially see the transmitted data.

🎯 Interview answer

«"For production APIs, I disable cleartext traffic and use HTTPS."»

---

17. Reverse Engineering

❓ How can an Android application be reverse engineered?

An APK can be downloaded and analyzed.

Attackers can:

APK
 ↓
Extract
 ↓
Decompile / Disassemble
 ↓
Inspect code/resources
 ↓
Understand application logic

Obfuscation makes this harder, but doesn't make reverse engineering impossible.

💡 Real-life example

An attacker downloads your APK and analyzes it to discover how your authentication logic works.

🎯 Interview answer

«"Android applications can be reverse engineered, so we use techniques such as R8 obfuscation, secure backend validation and APK signing to increase protection."»

---

18. ProGuard

❓ What is ProGuard?

ProGuard is a tool historically used for:

- Code shrinking
- Optimization
- Obfuscation

It can remove unused code and make the remaining code harder to understand.

💡 Real-life example

Instead of readable names like:

PaymentManager
processPayment()

obfuscated output may use short, meaningless names.

🎯 Interview answer

«"ProGuard is a tool traditionally used for shrinking, optimization and obfuscation of Android applications."»

---

19. R8

❓ What is R8?

R8 is Android's modern code shrinker and optimizer.

It performs tasks such as:

- Shrinking
- Optimization
- Obfuscation

It is integrated into the Android build process.

💡 Real-life example

Your app contains thousands of classes, but only a portion is actually required in the final application.

R8 can remove unused code and optimize the resulting APK.

🎯 Interview answer

«"R8 is Android's modern shrinker, optimizer and obfuscator used to reduce application size and make reverse engineering harder."»

---

20. ProGuard vs R8

❓ What's the difference?

ProGuard| R8
Older tool| Modern Android tool
Shrinking| Shrinking
Obfuscation| Obfuscation
Optimization| Optimization
Historically used| Commonly used today

🎯 Easy answer

«ProGuard is the older solution; R8 is the modern Android shrinker/optimizer/obfuscator.»

---

21. Code Obfuscation

❓ What is code obfuscation?

Obfuscation changes code into a form that's harder for humans to understand.

For example:

Before:
PaymentManager.processPayment()

After:
a.b()

It doesn't make the application impossible to reverse engineer.

💡 Real-life example

A thief may still be able to enter a house, but confusing the layout makes it harder for them to understand where everything is.

🎯 Interview answer

«"Obfuscation makes reverse engineering more difficult by transforming readable code into less understandable code."»

---

22. API Keys & Secrets

❓ Can R8 protect API keys or secrets?

No.

R8 can obfuscate code, but it cannot make a secret embedded inside an APK truly secret.

If the application needs the value at runtime, a determined attacker may potentially extract it.

💡 Real-life example

You put:

const val SECRET_KEY = "ABC123"

inside the app.

Even if R8 changes the variable name, the actual secret may still be recoverable.

🎯 Interview answer

«"R8 protects code structure, not secrets. Sensitive secrets should be kept on a secure backend whenever possible."»

---

23. APK Signing

❓ What is APK signing?

APK signing allows Android to verify the identity associated with an application package and helps detect unauthorized modifications.

The developer signs the application using a signing key.

💡 Real-life example

Think of it like a digital signature on a document.

If someone modifies the document after you sign it, the signature no longer matches.

Similarly, modifying an APK can invalidate its expected signature.

🎯 Interview answer

«"APK signing provides application identity and helps Android verify that an APK hasn't been improperly modified."»

---

24. "android:exported"

❓ What does "android:exported" mean?

It controls whether an Android component can be launched by other applications.

Example:

<activity
    android:name=".PaymentActivity"
    android:exported="false" />

Other applications cannot directly launch this activity.

💡 Real-life example

Imagine a bank has an internal employee-only room.

If the room is marked private, random visitors can't enter it.

🎯 Interview answer

«""android:exported" controls whether a component can be accessed by other applications."»

---

25. Securing Android Components

❓ How do you secure Activities, Services and BroadcastReceivers?

Avoid unnecessarily exposing components.

Consider:

- "android:exported"
- Permissions
- Intent validation
- Input validation
- Authentication/authorization

💡 Real-life example

Suppose your app has:

DeleteAccountActivity

You don't want another application to invoke it without authorization.

So you restrict access and validate the request.

🎯 Interview answer

«"I minimize exported components, protect exposed components with permissions and validate incoming intents/data."»

---

26. WebView Security

❓ What are common WebView security issues?

WebView can become risky when loading untrusted content.

Potential concerns include:

- Untrusted URLs
- JavaScript
- JavaScript interfaces
- Unsafe URL handling
- SSL error handling

💡 Real-life example

If your app loads an attacker-controlled website inside WebView and exposes sensitive native functionality, the website may potentially abuse that bridge.

🎯 Interview answer

«"I restrict WebView navigation to trusted domains, avoid unnecessary JavaScript and carefully control JavaScript-to-native communication."»

---

27. "addJavascriptInterface()"

❓ Why can "addJavascriptInterface()" be dangerous?

It allows JavaScript running inside a WebView to communicate with Android code.

JavaScript
     ↓
addJavascriptInterface()
     ↓
Android code

If untrusted web content can access a powerful native interface, it can create security risks.

💡 Real-life example

Imagine giving a website a remote control that can access sensitive Android functionality.

If you load an untrusted website, that remote control becomes dangerous.

🎯 Interview answer

«""addJavascriptInterface()" creates a JavaScript-to-native bridge, so it should only expose minimal functionality to trusted content."»

---

28. Common Reverse Engineering Tools

❓ What tools are commonly used to reverse engineer Android apps?

Tool| Purpose
JADX| Decompile/analyze APK/Dex
apktool| Decode APK resources and Smali
Frida| Runtime instrumentation/hooking
Burp Suite| Inspect/intercept network traffic
MobSF| Mobile security analysis
ADB| Communicate with Android devices

💡 Real-life example

A security tester might use:

JADX
  ↓
Understand application code

Burp Suite
  ↓
Analyze network requests

Frida
  ↓
Observe/modify runtime behavior

🎯 Interview answer

«"For Android security testing, tools like JADX, apktool, Frida, Burp Suite and MobSF are commonly used."»

---

29. Root Detection

❓ What is root detection and why might an app care about rooted devices?

Rooting can give a user or attacker elevated control over the device.

This can make it easier to:

- Inspect app data
- Modify runtime behavior
- Hook application code
- Bypass some security controls

Apps handling highly sensitive data may detect compromised environments.

💡 Real-life example

A banking application may detect that the device has been compromised and restrict certain sensitive operations.

⚠️ Important

Root detection is not perfect security.

A sophisticated attacker may bypass root detection.

🎯 Interview answer

«"Root detection can identify potentially compromised environments, but it should be treated as one layer of defense rather than a complete security solution."»

---
