🔐 Android Security — Interview Preparation

«A practical Android security interview guide with simple explanations, real-life examples, and interview-ready answers.»

---

📚 Table of Contents

1. "Secure Data Storage" (#1-secure-data-storage)
2. "Android Keystore" (#2-android-keystore)
3. "Secure Token Storage" (#3-secure-token-storage)
4. "Hardcoded Secrets" (#4-hardcoded-secrets)
5. "Biometric Authentication" (#5-biometric-authentication)
6. "BiometricPrompt" (#6-biometricprompt)
7. "Authentication vs Authorization" (#7-authentication-vs-authorization)
8. "HTTP vs HTTPS" (#8-http-vs-https)
9. "How HTTPS Works" (#9-how-https-works)
10. "SSL/TLS" (#10-ssltls)
11. "SSL/TLS Handshake" (#11-ssltls-handshake)
12. "MITM Attack" (#12-mitm-attack)
13. "Preventing MITM Attacks" (#13-preventing-mitm-attacks)
14. "Certificate Pinning" (#14-certificate-pinning)
15. "Network Security Configuration" (#15-network-security-configuration)
16. "Cleartext Traffic" (#16-cleartext-traffic)
17. "Reverse Engineering" (#17-reverse-engineering)
18. "ProGuard" (#18-proguard)
19. "R8" (#19-r8)
20. "ProGuard vs R8" (#20-proguard-vs-r8)
21. "Code Obfuscation" (#21-code-obfuscation)
22. "API Keys & Secrets" (#22-api-keys--secrets)
23. "APK Signing" (#23-apk-signing)
24. ""android:exported"" (#24-androidexported)
25. "Securing Android Components" (#25-securing-android-components)
26. "WebView Security" (#26-webview-security)
27. ""addJavascriptInterface()"" (#27-addjavascriptinterface)
28. "Reverse Engineering Tools" (#28-reverse-engineering-tools)
29. "Root Detection" (#29-root-detection)

---

1. Secure Data Storage

❓ How do you securely store sensitive data in Android?

Sensitive data such as authentication tokens, encryption keys, passwords, and personal information should not be stored as plain text.

For sensitive data, we can use:

- Android Keystore
- Encrypted storage
- Encrypted files/database
- Secure token storage

The important rule is:

«Never store sensitive information as plain text.»

💡 Real-life example

A banking app should not simply save a user's password inside a normal text file or SharedPreferences.

Instead, sensitive information should be protected using appropriate Android security mechanisms.

🎯 Interview answer

«"I avoid storing sensitive data in plain text and use encrypted storage with Android Keystore where appropriate."»

---

2. Android Keystore

❓ What is Android Keystore?

Android Keystore is a secure place provided by Android to create and protect encryption keys.

Your app can use these keys to encrypt or decrypt data, but the key itself is protected by Android.

On some devices, the key can also be protected by special hardware, making it even harder to extract.

💡 Real-life example

Think of Android Keystore like a bank locker.

You can ask the bank to use something inside the locker, but you don't carry the valuable item around yourself.

Similarly, your app asks Android to use the encryption key when needed.

🎯 Interview answer

«"Android Keystore securely creates and protects cryptographic keys so apps can use them without directly exposing the keys."»

---

3. Secure Token Storage

❓ How do you securely store access and refresh tokens?

Access and refresh tokens are sensitive because someone with a valid token may be able to access the user's account.

Avoid storing tokens in:

- Plain SharedPreferences
- Logs
- Hardcoded constants
- Unencrypted files

Use secure/encrypted storage and protect encryption keys using Android Keystore where appropriate.

💡 Real-life example

A food delivery app stores an authentication token so the user doesn't have to log in every time.

If someone steals that token, they may be able to impersonate the user.

🎯 Interview answer

«"I store authentication tokens using encrypted storage and protect the encryption keys using Android Keystore."»

---

4. Hardcoded Secrets

❓ Why shouldn't you hardcode API keys or secrets in an Android app?

An Android APK can be reverse engineered.

For example:

const val API_KEY = "secret123"

Even if the variable name is obfuscated, a determined attacker may still extract the secret from the APK.

💡 Real-life example

Imagine putting your house key inside a box and giving that box to everyone.

Even if you write "nothing important here" on the box, someone can still open it.

🎯 Interview answer

«"Anything shipped inside the APK should be considered potentially accessible. Sensitive secrets should be kept on a secure backend whenever possible."»

---

5. Biometric Authentication

❓ What is Biometric Authentication?

Biometric authentication allows users to authenticate using device-supported biometrics such as:

- Fingerprint
- Face
- Other supported biometric methods

💡 Real-life example

A banking app asks:

«"Authenticate with fingerprint to view your account."»

The user doesn't need to enter their password every time.

🎯 Interview answer

«"Biometric authentication allows users to authenticate using supported device biometrics such as fingerprint or face."»

---

6. BiometricPrompt

❓ How does "BiometricPrompt" work?

"BiometricPrompt" is Android's API for displaying a standard biometric authentication prompt.

The basic flow is:

App
 ↓
BiometricPrompt
 ↓
User provides fingerprint/face
 ↓
Android verifies the biometric
 ↓
Authentication result
 ↓
App continues

The app does not receive or store the user's actual biometric data.

💡 Real-life example

Your banking app doesn't receive your fingerprint image.

Android handles the biometric verification and tells the application whether authentication succeeded.

🎯 Interview answer

«""BiometricPrompt" provides a standard Android API for biometric authentication while the actual biometric data remains protected by the system."»

---

7. Authentication vs Authorization

❓ What's the difference between Authentication and Authorization?

Authentication = Who are you?

Authorization = What are you allowed to do?

💡 Real-life example

You log into an admin dashboard.

Authentication:
"Are you Rehan?"

Authorization:
"Is Rehan allowed to delete users?"

🧠 Easy memory trick

«Authentication → Identity»

«Authorization → Permission»

🎯 Interview answer

«"Authentication verifies who the user is, while authorization determines what that user is allowed to do."»

---

8. HTTP vs HTTPS

❓ What's the difference between HTTP and HTTPS?

HTTP sends data without encryption.

HTTPS uses TLS encryption to protect communication.

HTTP
Client ────────────────> Server
       Unencrypted

HTTPS
Client ════════════════> Server
       Encrypted

💡 Real-life example

If you're entering banking credentials, you don't want someone monitoring the network to read them.

HTTPS encrypts the communication.

🎯 Interview answer

«"HTTPS is HTTP secured using TLS, providing encryption, authentication, and integrity for network communication."»

---

9. How HTTPS Works

❓ How does HTTPS actually work?

At a high level:

Client
  ↓
Connects to server
  ↓
Server provides certificate
  ↓
Client validates certificate
  ↓
Secure keys are established
  ↓
Encrypted communication begins

💡 Real-life example

When your Android app calls:

https://api.example.com/user

the request and response are protected using the secure TLS connection.

🎯 Interview answer

«"HTTPS uses TLS to authenticate the server, establish secure cryptographic keys, and then encrypt communication between the client and server."»

---

10. SSL/TLS

❓ What is SSL/TLS?

TLS stands for:

«Transport Layer Security»

TLS is the security protocol used to protect data sent over a network.

SSL is the older predecessor of TLS.

Modern systems use TLS rather than old SSL versions.

💡 Real-life example

When your Android app communicates with a server over HTTPS, TLS protects that communication from being easily read or modified by attackers.

🎯 Interview answer

«"TLS is the cryptographic protocol used by HTTPS to secure communication between the client and server."»

---

11. SSL/TLS Handshake

❓ What happens during an SSL/TLS handshake?

The exact process depends on the TLS version, but conceptually:

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
  ↓
Encrypted communication

The main goals are:

1. Agree on security parameters
2. Authenticate the server
3. Establish secure session keys
4. Start encrypted communication

💡 Real-life example

Before your banking app sends sensitive account information, the app and server establish a secure communication channel.

🎯 Interview answer

«"The TLS handshake establishes the secure connection, validates the server's identity, and establishes keys used to encrypt communication."»

---

12. MITM Attack

❓ What is a Man-in-the-Middle attack?

A MITM attack occurs when an attacker tries to position themselves between the client and server.

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
- Never accept invalid certificates
- Use modern TLS versions
- Certificate pinning when appropriate
- Never blindly trust all certificates

🚫 Bad practice

Never configure the app to trust every certificate just to make an API call work.

💡 Real-life example

A banking app should never accept an arbitrary certificate just because the connection is technically HTTPS.

🎯 Interview answer

«"I use HTTPS with proper certificate validation and, where appropriate, certificate pinning to reduce MITM risks."»

---

14. Certificate Pinning

❓ What is Certificate Pinning?

Certificate pinning means the app has an expected certificate or public-key identity for its backend.

The app checks that the server matches the expected identity during the TLS connection.

💡 Real-life example

Imagine your app saying:

«"I only trust this specific identity for my banking server."»

Even if an attacker presents another certificate that is otherwise trusted by the device, the app can reject it if it doesn't match the configured pin.

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

You might want production traffic to always use HTTPS while allowing HTTP only in a controlled development environment.

🎯 Interview answer

«"Network Security Configuration allows us to configure Android's network security policies declaratively."»

---

16. Cleartext Traffic

❓ What is cleartext traffic and how do you prevent it?

Cleartext traffic means communication without encryption, such as HTTP.

HTTP  → Cleartext
HTTPS → Encrypted

For production applications, cleartext traffic should generally be disabled unless there is a specific reason to allow it.

💡 Real-life example

If your production app communicates with:

http://api.example.com

the communication is not protected by TLS.

🎯 Interview answer

«"I disable cleartext traffic for production and use HTTPS for API communication."»

---

17. Reverse Engineering

❓ How can an Android application be reverse engineered?

An APK can be downloaded and analyzed.

Conceptually:

APK
 ↓
Extract
 ↓
Decompile / Disassemble
 ↓
Inspect code/resources
 ↓
Understand application logic

Obfuscation makes this harder, but does not make reverse engineering impossible.

💡 Real-life example

An attacker downloads your APK and analyzes it to understand how your authentication or payment logic works.

🎯 Interview answer

«"Android applications can be reverse engineered, so we use techniques such as R8 obfuscation, secure backend validation, and APK signing to increase protection."»

---

18. ProGuard

❓ What is ProGuard?

ProGuard is an older tool used for:

- Code shrinking
- Optimization
- Obfuscation

It can remove unused code and make the remaining code harder to understand.

💡 Real-life example

Instead of readable names like:

PaymentManager
processPayment()

obfuscated code may contain short, meaningless names.

🎯 Interview answer

«"ProGuard is a tool traditionally used for shrinking, optimization, and obfuscation of Android applications."»

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

Your application contains thousands of classes, but only some are required in the final APK.

R8 can remove unused code and optimize the final application.

🎯 Interview answer

«"R8 is Android's modern shrinker, optimizer, and obfuscator used to reduce app size and make reverse engineering harder."»

---

20. ProGuard vs R8

❓ What's the difference between ProGuard and R8?

ProGuard| R8
Older tool| Modern Android tool
Shrinking| Shrinking
Obfuscation| Obfuscation
Optimization| Optimization
Historically common| Commonly used today

🎯 Easy answer

«"ProGuard is the older solution, while R8 is the modern Android shrinker, optimizer, and obfuscator."»

---

21. Code Obfuscation

❓ What is code obfuscation?

Obfuscation changes code into a form that is harder for humans to understand.

For example:

Before:
PaymentManager.processPayment()

After:
a.b()

It makes reverse engineering harder, but does not make it impossible.

💡 Real-life example

Imagine giving someone a map where all the street names have been replaced with random letters.

They still have the map, but understanding it becomes much harder.

🎯 Interview answer

«"Code obfuscation makes reverse engineering harder by transforming readable code into less understandable code."»

---

22. API Keys & Secrets

❓ Can R8 protect API keys or secrets?

No.

R8 protects and obfuscates code, but it cannot make a secret embedded inside an APK truly secret.

If the app needs the value at runtime, a determined attacker may potentially extract it.

💡 Real-life example

You put:

const val SECRET_KEY = "ABC123"

inside your application.

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

«"APK signing provides application identity and helps Android verify that an APK has not been improperly modified."»

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

If the room is private, random visitors cannot enter it.

🎯 Interview answer

«""android:exported" controls whether a component can be accessed by other applications."»

---

25. Securing Android Components

❓ How do you secure Activities, Services, and BroadcastReceivers?

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

«"I minimize exported components, protect exposed components with permissions, and validate incoming intents and data."»

---

26. WebView Security

❓ What are common WebView security issues?

WebView can become risky when loading untrusted content.

Common concerns include:

- Untrusted URLs
- JavaScript
- JavaScript interfaces
- Unsafe URL handling
- Unsafe SSL error handling

💡 Real-life example

If your app loads an attacker-controlled website inside a WebView and exposes sensitive native functionality, the website may potentially abuse that bridge.

🎯 Interview answer

«"I restrict WebView navigation to trusted domains, avoid unnecessary JavaScript, and carefully control JavaScript-to-native communication."»

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

«""addJavascriptInterface()" creates a JavaScript-to-native bridge, so it should expose only minimal functionality to trusted content."»

---

28. Common Reverse Engineering Tools

❓ What tools are commonly used for Android reverse engineering and security testing?

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
Observe runtime behavior

🎯 Interview answer

«"Common Android security testing tools include JADX, apktool, Frida, Burp Suite, MobSF, and ADB."»

---

29. Root Detection

❓ What is root detection and why might an app care about rooted devices?

Rooting can give a user or attacker elevated control over the device.

This can make it easier to:

- Inspect app data
- Modify runtime behavior
- Hook application code
- Bypass some security controls

Apps handling highly sensitive data may detect potentially compromised devices.

💡 Real-life example

A banking application may detect that the device is compromised and restrict certain sensitive operations.

⚠️ Important

Root detection is not perfect security.

A sophisticated attacker may bypass it.

🎯 Interview answer

«"Root detection can identify potentially compromised environments, but it should be treated as one layer of defense rather than complete security."»

---

🧠 Final Memory Map

When an interviewer says:

«"Let's talk about Android Security."»

Think:

                 🔐 ANDROID SECURITY
                        │
        ┌───────────────┼───────────────┐
        ↓               ↓               ↓
       DATA          NETWORK           APP
        │               │               │
    Keystore         HTTPS              R8
    Tokens           TLS               Obfuscation
    Secrets          MITM              APK Signing
                    Pinning
                     
