PASSWORD MANAGER

Secure Password Manager with AES Encryption, Master Authentication, and Persistent Storage

> Problem Statement:

With the rapid increase in the number of digital platforms, users are required to manage numerous accounts, each with unique and complex passwords. Remembering these passwords often leads individuals to adopt insecure practices, such as reusing passwords or storing them in plain text, which increases vulnerability to cyberattacks and data breaches.

Existing password storage methods either lack encryption or rely on insecure local storage, leaving sensitive information exposed. Hence, there is a critical need for a secure, user-friendly, and persistent password management system that ensures passwords remain confidential, accessible, and protected even across multiple sessions.

> Objective:

To design and develop an enhanced Password Manager application in Java that allows users to securely store, manage, and retrieve passwords. The system will incorporate AES encryption for password security, SHA-256 hashing for master password authentication, and persistent local storage (using files or database) to retain data safely.

> Features:

AES Encryption & Decryption:
All passwords will be encrypted using the Advanced Encryption Standard (AES) before storage and decrypted only upon retrieval.

Master Password Authentication:
Access to the password vault will be protected by a user-defined master password, verified through SHA-256 hashing.

Persistent Encrypted Storage:
Encrypted passwords will be stored securely in a local file or lightweight database (e.g., SQLite) to retain data even after program termination.

Password Generator:
The system will include a secure random password generator to help users create strong, unpredictable passwords.

User-Friendly GUI Interface (JavaFX):
A clean, intuitive graphical interface will replace the console-based system, making the application more practical and accessible.

CRUD Operations:
Users can add, view, update, or delete stored passwords, ensuring complete management of credentials.

Activity Logging (Optional):
The system will maintain a log file of key actions (e.g., password additions or deletions) for better tracking and debugging.

> Outcome:

A robust and secure Java-based password management application that:

Protects sensitive user data using industry-standard encryption.

Provides persistent storage for passwords across sessions.

Incorporates authentication and password generation features.

Offers an interactive GUI for ease of use.

This project demonstrates practical application of cryptography, authentication, secure storage, and GUI development — key concepts in cybersecurity and software engineering.
