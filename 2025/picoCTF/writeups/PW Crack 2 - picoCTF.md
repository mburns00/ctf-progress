# PW Crack 2 – picoCTF 2025

## Challenge Info
**Name:** PW Crack 2  
**CTF Event:** picoCTF 2025  
**Category:** Reverse Engineering / Crypto  
**Points/Difficulty:** Easy  

---

## What I Did

1. **Downloaded the challenge files**, which included:
   - `level2.py`
   - `level2.flag.txt.enc`

2. **Opened the Python file** to inspect the logic:
   ```bash
   cat level2.py
   ```

3. **Noticed the password was obfuscated** using hex character codes:
   ```python
   if user_pw == chr(0x34) + chr(0x65) + chr(0x63) + chr(0x39):
   ```

4. **Converted the hex values into ASCII** using a Python one-liner:
   ```bash
   python3 -c "print(''.join([chr(0x34), chr(0x65), chr(0x63), chr(0x39)]))"
   ```

5. **Got the password key** from the output:
   ```
   4ec9
   ```

6. **Opened CyberChef** and dragged in the `level2.flag.txt.enc` file.

7. **Added an XOR operation**:
   - Key: `4ec9`
   - Mode: ASCII
   - Enabled: "Repeat key"

8. **Adjusted decoding settings** until the decrypted flag became readable text.

---

## Flag

`picoCTF{tr45h_51ng1ng_9701e681}`

---

## Notes

- The challenge used XOR with a repeated key.
- The password was hidden using `chr()` calls, which made it slightly less obvious.
- CyberChef made the decryption very fast once the key was known.

---

## Tools Used

- `cat`
- `python3`
- [CyberChef](https://gchq.github.io/CyberChef/)

---

## Checklist

- [x] Challenge solved  
- [x] Flag captured  
- [x] Writeup added  
