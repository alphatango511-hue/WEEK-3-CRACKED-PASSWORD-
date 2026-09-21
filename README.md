# WEEK-3-CRACKED-PASSWORD-
# README: Cracking a Password-Protected PDF with John the Ripper

## Objective
Recover the password of a locked PDF file (`My-Locked-PDF1.pdf`) using John the Ripper and a wordlist, then create an unlocked copy.

## Tools Used
- John the Ripper – password cracking tool
- pdf2john.pl – extracts password hash from PDF files
- rockyou.txt – common password wordlist
- qpdf – removes password from PDF once known
- Kali Linux – operating system

## Step-by-Step Process

### 1. Navigate to the correct directory
```bash
cd ~/Desktop
ls
```
Confirmed the file `My-Locked-PDF1.pdf` exists.

### 2. Extract the hash from the PDF
```bash
/usr/share/john/pdf2john.pl My-Locked-PDF1.pdf > pdf_hash.txt
```
- Used full path because `pdf2john.pl` was not in `$PATH`.
- Output redirected to `pdf_hash.txt`.

### 3. Verify the hash file
```bash
cat pdf_hash.txt
```
Output showed a hash line like:
```
My-Locked-PDF1.pdf:$pdf$4*4*128*-1060*1*16*55d1a5c1...
```

### 4. Locate the wordlist
```bash
find / -name "rockyou*" 2>/dev/null
```
Found `/usr/share/wordlists/rockyou.txt.gz` (compressed).

### 5. Decompress the wordlist
```bash
sudo gunzip /usr/share/wordlists/rockyou.txt.gz
```
Now `/usr/share/wordlists/rockyou.txt` exists (~140 MB).

### 6. Run John the Ripper
```bash
cd ~/Desktop
john --wordlist=/usr/share/wordlists/rockyou.txt pdf_hash.txt
```
Result:
```
password1  (/home/kali/Desktop/My-Locked-PDF1.pdf)
1g 0:00:00:00 DONE
```

### 7. Show the cracked password
```bash
john --show pdf_hash.txt
```
Output:
```
My-Locked-PDF1.pdf:password1
1 password hash cracked, 0 left
```

### 8. Remove the password from the PDF (optional)
```bash
qpdf --password=password1 --decrypt My-Locked-PDF1.pdf Unlocked.pdf
```
Created `Unlocked.pdf` with no password.

## Result
- Password found: `password1`
- Unlocked file: `Unlocked.pdf`

## Lessons Learned
- PDF passwords are stored as hashes; they can be cracked with wordlists.
- `pdf2john.pl` converts PDF encryption into a crackable hash.
- `rockyou.txt` must be decompressed before use on Kali.
- Use full paths when a command is not in `$PATH`.
- Always run cracking tools only on files you own or have permission to test.

## Disclaimer
This README is for educational purposes only. Use these techniques only on your own files or in authorized environments (CTFs, labs, etc.). Unauthorized password cracking is illegal.