WEEK-3-CRACKED-PASSWORD

README: Cracking a Password-Protected PDF with John the Ripper

Objective

Recover the password of a password-protected PDF file ("My-Locked-PDF1.pdf") using John the Ripper and a wordlist, then create an unlocked copy of the PDF.

Tools Used

- John the Ripper – Password-cracking tool
- pdf2john.pl – Extracts the password hash from a PDF
- rockyou.txt – Common password wordlist
- qpdf – Removes the password from the PDF once the password is known
- Kali Linux – Operating system

---

Step-by-Step Process

1. Navigate to the Correct Directory

First, I navigated to the Desktop directory and checked that the password-protected PDF was present.

cd ~/Desktop
ls

The file "My-Locked-PDF1.pdf" was confirmed to be present.

"Screenshot: Navigating to Desktop and checking the PDF" (Screenshot%202026-09-17%20121639.png)

---

2. Extract the PDF Password Hash

I used "pdf2john.pl" to extract the encryption hash from the PDF.

/usr/share/john/pdf2john.pl My-Locked-PDF1.pdf > pdf_hash.txt

The full path was used because "pdf2john.pl" was not available directly in the "$PATH".

The extracted hash was saved in:

pdf_hash.txt

Example hash format:

My-Locked-PDF1.pdf:$pdf$4*4*128*-1060*1*16*55d1a5c1...

"Screenshot: Extracting the PDF hash" (Screenshot%202026-09-17%20124310.png)

---

3. Verify the Hash File

I checked the contents of the generated hash file:

cat pdf_hash.txt

The command displayed the PDF hash that John the Ripper would use for password recovery.

---

4. Locate the Wordlist

I searched the system for the RockYou wordlist:

find / -name "rockyou*" 2>/dev/null

The compressed wordlist was found at:

/usr/share/wordlists/rockyou.txt.gz

---

5. Decompress the Wordlist

Because the wordlist was compressed, I decompressed it using:

sudo gunzip /usr/share/wordlists/rockyou.txt.gz

The wordlist was then available as:

/usr/share/wordlists/rockyou.txt

---

6. Run John the Ripper

I navigated back to the Desktop and ran John the Ripper using the RockYou wordlist:

cd ~/Desktop
john --wordlist=/usr/share/wordlists/rockyou.txt pdf_hash.txt

John successfully recovered the password.

Result:

password1

John reported:

1g 0:00:00:00 DONE

"Screenshot: John the Ripper cracking the password" (Screenshot%202026-09-17%20124310.png)

---

7. Display the Cracked Password

I used "john --show" to display the recovered password:

john --show pdf_hash.txt

Output:

My-Locked-PDF1.pdf:password1

1 password hash cracked, 0 left

The recovered password was:

password1

---

8. Remove the Password from the PDF

After recovering the password, I used "qpdf" to create an unlocked copy:

qpdf --password=password1 --decrypt My-Locked-PDF1.pdf Unlocked.pdf

This created:

Unlocked.pdf

The new PDF could be opened without entering a password.

---

Result

Password Recovered

password1

Unlocked File

Unlocked.pdf

The password-protected PDF was successfully processed in the authorized lab environment.

---

Lessons Learned

- PDF files can contain encryption data that can be represented as password hashes.
- "pdf2john.pl" can extract information from supported password-protected PDFs for John the Ripper.
- Wordlists such as "rockyou.txt" can be used for password recovery in authorized security testing.
- Compressed wordlists must be decompressed before they can be used directly.
- Using the full path to a tool is useful when the command is not included in "$PATH".
- "qpdf" can be used to create a decrypted copy when the correct password is known.
- Password-cracking exercises should only be performed on files that you own or have explicit permission to test.

---

Disclaimer

This project is for educational and authorized cybersecurity laboratory purposes only.

The techniques demonstrated here should only be used on your own files, authorized security-testing environments, or legal CTF/lab exercises. Unauthorized password cracking or access to protected files may be illegal.