# WEEK 3: CRACKED PASSWORD

## 📌 Project Overview
This repository contains the documentation and results for the Week 3 cybersecurity assignment. The objective of this task was to demonstrate password cracking techniques by extracting and cracking a password hash.

## 🛠️ Tools Used
*   **[e.g., Kali Linux]** - Operating system used for the environment.
*   **[e.g., Hashcat or John the Ripper]** - Tool used to crack the password hash.
*   **[e.g., rockyou.txt]** - Wordlist used for the dictionary attack.

## 🚀 Methodology (Steps Taken)
1.  **Hash Extraction:** [Explain how you got the hash. e.g., "Extracted the NTLM hash from the provided SAM file."]
2.  **Identifying Hash Type:** [e.g., "Identified the hash as an MD5 hash."]
3.  **Executing the Attack:** [Explain the command you used. e.g., "Ran the following command using John the Ripper: `john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt`"]
4.  **Cracking the Password:** [e.g., "Successfully recovered the plaintext password within 5 minutes."]

## 📸 Screenshots
Below are the screenshots demonstrating the process and the final result:

### 1. The Target Hash
![Initial Hash](screenshots/IMG-20260921-WA0002.jpg)
*(Describe what this image shows)*

### 2. Running the Cracking Tool
![Cracking Process](screenshots/IMG-20260921-WA0003.jpg)
*(Describe what this image shows)*

### 3. Password Successfully Cracked
![Final Result](screenshots/IMG-20260921-WA0004.jpg)
*(Describe what this image shows)*

## 🧠 Conclusion & Lessons Learned
This assignment demonstrated the importance of using strong, complex passwords. Weak passwords that exist in common wordlists (like rockyou.txt) can be cracked in seconds. To mitigate this, organizations should enforce multi-factor authentication (MFA) and complex password policies.
