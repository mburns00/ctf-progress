# PW Crack 3 – picoCTF 2025

## Challenge Info
**Name:** PW Crack 3  
**CTF Event:** picoCTF 2025  
**Category:** Reverse Engineering / Crypto  
**Points/Difficulty:** Medium  

---

## What I Did

1. **Downloaded the challenge files**, which included:
   - `level3.py`
   - `level3.flag.txt.enc`
   - `level3.hash.bin`

2. **Opened the Python file** to inspect the logic:
   ```bash
   cat level3.py
   ```

3. **Noticed the password was hashed with MD5** and compared against a binary hash file, with 7 possible passwords listed at the bottom.

4. **Extracted the hash from binary format** to hexadecimal:
   ```bash
   xxd -p level3.hash.bin | tr -d '\n' > hash.txt
   ```

5. **Created a wordlist** from the possible passwords in the code:
   ```bash
   echo -e "6997\n3ac8\n4b17\nec27\n4e66\n865e\nf0ac\n3ac8" > wordlist.txt
   ```

6. **Used hashcat to crack the MD5 hash**:
   ```bash
   hashcat -m 0 hash.txt wordlist.txt
   ```

7. **Found the correct password** from hashcat output:
   ```
   1b18e1316f9218cc5b053e1cea28e02e:865e
   ```

8. **Ran the original script** with the cracked password:
   ```bash
   python3 level3.py
   # Entered: 865e
   ```

---

## Flag
`picoCTF{[decrypted_flag_here]}`

---

## Notes
- The challenge used MD5 hashing to verify the password before XOR decryption.
- A list of 7 possible passwords was provided, making it perfect for a dictionary attack.
- Hashcat cracked the hash almost instantly with such a small wordlist.
- The `xxd` command was essential for converting the binary hash to the hex format hashcat expects.

---

## Tools Used
- `cat`
- `xxd`
- `tr`
- `echo`
- `hashcat`
- `python3`

---

## Checklist
- [x] Challenge solved  
- [x] Hash cracked using Kali tools  
- [x] Flag captured  
- [x] Writeup added
