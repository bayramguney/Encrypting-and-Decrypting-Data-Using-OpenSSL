# Encrypting-and-Decrypting-Data-Using-OpenSSL

# 🔐 Lab - Encrypting and Decrypting Data Using OpenSSL

## 📌 Overview

This lab demonstrates how to use **OpenSSL** to encrypt and decrypt text files using the **AES-256-CBC** encryption algorithm. It also explains how **Base64 encoding** improves the readability and portability of encrypted data.

> **Note:** This lab is intended for educational purposes only. The encryption method shown does not provide modern security guarantees such as authenticated encryption and uses an older password-based key derivation method.

---

## 🎯 Objectives

- Encrypt a text file using OpenSSL
- Encrypt data using AES-256-CBC
- Encode encrypted data with Base64
- Decrypt encrypted files
- Understand the purpose of Base64 encoding
- Learn the limitations of password-based encryption

---

## 🛠️ Technologies Used

- OpenSSL
- Linux Terminal
- AES-256-CBC Encryption
- Base64 Encoding

---

## 📂 Lab Environment

- Security Workstation Virtual Machine
- OpenSSL command-line utility

---

# Part 1 – Encrypting Messages

## Step 1: Navigate to the Lab Directory

```bash
cd ./lab.support.files/
```

---

## Step 2: View the Original File

```bash
cat letter_to_grandma.txt
```

The file contains a readable plaintext message.

---

## Step 3: Encrypt the File

```bash
openssl aes-256-cbc -in letter_to_grandma.txt -out message.enc
```

OpenSSL prompts for an encryption password.

---

## Question 1

### Document the password.

**Answer:**

For security reasons, the password should **not** be documented publicly. Use a strong password and store it securely (for example, in a password manager).

---

## Step 4: View the Encrypted File

```bash
cat message.enc
```

---

## Question 2

### Did the contents of `message.enc` display correctly? What does it look like? Explain.

**Answer:**

No. The file does not display as readable text because it contains **binary encrypted data**. When viewed with `cat`, it appears as random symbols, unreadable characters, or garbled output because the terminal is attempting to display binary data as text.

---

## Step 5: Encrypt Again Using Base64 Encoding

```bash
openssl aes-256-cbc -a -in letter_to_grandma.txt -out message.enc
```

The `-a` option tells OpenSSL to Base64-encode the encrypted output.

---

## Step 6: Display the Encoded File

```bash
cat message.enc
```

The output now consists of readable ASCII characters similar to:

```
U2FsdGVkX19ApWyrn8RD5zNp0RPCuMGZ...
```

---

## Question 3

### Is `message.enc` displayed correctly now? Explain.

**Answer:**

Yes. The encrypted data is now Base64-encoded, converting binary data into readable ASCII text. Although the content is still encrypted and unreadable to humans, it can now be safely displayed in the terminal or stored in text-based systems.

---

## Question 4

### Can you think of a benefit of having `message.enc` Base64-encoded?

**Answer:**

Yes. Base64 encoding allows encrypted data to be safely transmitted through email, text files, web applications, and other systems that only support text. It also prevents corruption that can occur when binary files are transferred through text-only channels.

---

# Part 2 – Decrypting Messages

## Step 1: Decrypt the File

```bash
openssl aes-256-cbc -a -d -in message.enc -out decrypted_letter.txt
```

Enter the same password that was used during encryption.

---

## Step 2: View the Decrypted File

```bash
cat decrypted_letter.txt
```

The original message is displayed.

---

## Question 5

### Was the letter decrypted correctly?

**Answer:**

Yes. After entering the correct password, OpenSSL successfully decrypted the file and restored the original plaintext message without any changes.

---

## Question 6

### The command used to decrypt also contains the `-a` option. Can you explain?

**Answer:**

The `-a` option tells OpenSSL that the encrypted file is Base64-encoded. Before decrypting the data, OpenSSL first decodes the Base64 text back into its original binary encrypted format and then performs the AES-256-CBC decryption.

---

# 🔒 Security Concepts Learned

- Symmetric encryption
- AES-256-CBC algorithm
- Password-based encryption
- Base64 encoding
- Encryption and decryption workflow
- Binary vs. text file formats
- Secure handling of encryption passwords

---

# ⚠️ Security Notes

This lab demonstrates the basic use of OpenSSL but should **not** be used to protect sensitive information because:

- It relies on an older password-based key derivation method.
- It does not provide authentication or integrity protection.
- Modern applications should use stronger key derivation functions (PBKDF2, scrypt, Argon2) and authenticated encryption modes such as AES-GCM.

---

# ✅ Skills Demonstrated

- File encryption with OpenSSL
- File decryption using AES-256-CBC
- Linux command-line operations
- Base64 encoding and decoding
- Understanding symmetric cryptography
- Basic cryptographic security practices
