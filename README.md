🔐 Password Manager (Java)

A secure, Java-based Password Manager that uses AES encryption, SHA-256 master authentication, and persistent encrypted storage to safely manage user credentials across sessions.

📌 Problem Statement

With the growing number of digital services, users are required to maintain multiple accounts with strong and unique passwords. This often leads to insecure practices such as password reuse or storing credentials in plain text, increasing the risk of data breaches and cyberattacks.

Existing password storage solutions either lack proper encryption or rely on insecure local storage mechanisms. There is a clear need for a secure, user-friendly, and persistent password management system that protects sensitive credentials without compromising usability.

🎯 Objective

To design and develop a secure Password Manager in Java that enables users to store, retrieve, and manage passwords safely using:

AES encryption for protecting stored passwords

SHA-256 hashing for master password authentication

Persistent local storage to retain encrypted data across sessions

✨ Key Features

🔐 AES Encryption & Decryption
All stored passwords are encrypted using the Advanced Encryption Standard (AES) and decrypted only when required.

🔑 Master Password Authentication
Vault access is protected using a master password verified via SHA-256 hashing.

💾 Persistent Encrypted Storage
Encrypted credentials are stored securely in a local file or lightweight database (e.g., SQLite).

🔄 CRUD Operations
Users can Add, View, Update, and Delete stored credentials.

🎲 Secure Password Generator
Generates strong, random, and unpredictable passwords.

🖥 JavaFX GUI Interface
A clean and intuitive graphical user interface for improved usability.

📝 Activity Logging (Optional)
Logs important actions such as password creation or deletion for tracking and debugging.

🛠️ Technologies Used

Java

JavaFX (GUI)

AES (Advanced Encryption Standard)

SHA-256 Hashing

File System / SQLite (Persistent Storage)

🧩 System Workflow

User authenticates using a master password

Master password is verified using SHA-256 hashing

Passwords are encrypted using AES before storage

Encrypted data is stored persistently

Decryption occurs only during authorized retrieval

📊 Outcome

The project delivers a robust and secure password management solution that:

Protects sensitive credentials using industry-standard cryptography

Ensures secure and persistent local storage

Provides full credential management through CRUD operations

Enhances usability through a modern GUI

This project demonstrates practical knowledge of cryptography, authentication, secure storage, and GUI-based application development, aligning strongly with cybersecurity and software engineering principles.

🚀 Future Enhancements

Cloud-based encrypted synchronization

Auto-lock and inactivity timeout

Two-factor authentication (2FA)

Export / import encrypted vaults

⚠️ Security Note

Sensitive files, SDKs, and binaries are intentionally excluded from the repository using .gitignore. Users must install required dependencies separately.

⭐ If you like this project, feel free to star the repository!
