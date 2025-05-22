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

## Command Breakdown

### Command 1: Extract Hash from Binary File
```bash
xxd -p level3.hash.bin | tr -d '\n' > hash.txt
```

**Breaking it down:**
- `xxd` - A hex dump utility that converts binary data to hexadecimal
- `-p` - "Plain" output format (just hex digits, no offsets or ASCII)
- `level3.hash.bin` - The input binary file containing the hash
- `|` - Pipe operator, sends output of first command to second command
- `tr -d '\n'` - Text replace command that deletes (`-d`) newline characters (`\n`)
- `>` - Redirect output to a file
- `hash.txt` - Output file containing the hex hash

**Why needed:** Hashcat expects hashes in hexadecimal text format, but the challenge gives us a binary file. This converts it to the right format.

### Command 2: Create Password Wordlist
```bash
echo -e "6997\n3ac8\n4b17\nec27\n4e66\n865e\nf0ac\n3ac8" > wordlist.txt
```

**Breaking it down:**
- `echo` - Command that prints text
- `-e` - Enable interpretation of backslash escapes (like `\n`)
- `"6997\n3ac8\n..."` - String with passwords separated by newlines (`\n`)
- `>` - Redirect output to file
- `wordlist.txt` - Output file containing one password per line

**Why needed:** Hashcat needs a wordlist file with potential passwords to try against the hash.

### Command 3: Crack the Hash with Hashcat
```bash
hashcat -m 0 hash.txt wordlist.txt
```

**Breaking it down:**
- `hashcat` - GPU-accelerated password cracking tool
- `-m 0` - Mode parameter specifying hash type (0 = MD5)
- `hash.txt` - File containing the target hash to crack
- `wordlist.txt` - File containing passwords to try

**Hash modes (some common ones):**
- `-m 0` = MD5
- `-m 1000` = NTLM
- `-m 1400` = SHA256
- `-m 3200` = bcrypt

### Command 4: Show Results Only
```bash
hashcat -m 0 hash.txt wordlist.txt --show
```

**Breaking it down:**
- Same as above, but with `--show` flag
- `--show` - Only display previously cracked hashes (no cracking process)
- Outputs format: `hash:password`

**Why useful:** Skips all the verbose output and just shows you the cracked password.

---

## Alternative Commands You Could Use

### Using John the Ripper instead:
```bash
# Convert hash format for john
echo "user:$(cat hash.txt)" > john_hash.txt
# Crack it
john --wordlist=wordlist.txt --format=Raw-MD5 john_hash.txt
```

### Using hashcat with more options:
```bash
# Force CPU mode (if GPU issues)
hashcat -m 0 hash.txt wordlist.txt --force

# Show progress every 10 seconds
hashcat -m 0 hash.txt wordlist.txt --status-timer=10

# Save results to file
hashcat -m 0 hash.txt wordlist.txt -o cracked.txt
```

### Manual verification with md5sum:
```bash
# Test if a specific password matches
echo -n "865e" | md5sum
# Compare with: cat hash.txt
```

---

## Flag
`picoCTF{m45h_fl1ng1ng_2b072a90}`

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
