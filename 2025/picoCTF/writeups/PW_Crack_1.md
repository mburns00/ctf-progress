# PW Crack 1 – picoCTF 2025

## Challenge Info
**Name:** PW Crack 1  
**CTF Event:** picoCTF 2025  
**Category:** Crypto  
**Points/Difficulty:** Easy  

---

## What I Did

1. **Downloaded the challenge files**, which included:
   - `level1.py`
   - `level1.flag.txt.enc`

2. **Opened the Python file in `nano`**:
   ```bash
   nano level1.py
   ```

3. **Immediately saw the password** hardcoded in plain text:
   ```python
   if user_pw == "1e1a":
   ```

4. **Ran the script** using Python:
   ```bash
   python3 level1.py
   ```

5. **Entered the password when prompted**:
   ```
   Please enter correct password for flag:
   1e1a
   ```

6. **Piped the output to a file** to capture the flag:
   ```bash
   python3 level1.py > flag.txt
   ```

7. **Removed the first line** from the output (the input prompt) so only the flag remained:
   ```bash
   sed -i '1d' flag.txt
   ```

---

## Flag

`picoCTF{545h_r1ng1ng_fa343060}`

---

## Notes

- The challenge was easy due to the hardcoded password.
- XOR logic was used, but reversing wasn't necessary because the password was already visible.

---

## Tools Used

- `nano`
- `python3`
- `sed`

---

## Checklist

- [x] Challenge solved  
- [x] Flag captured  
- [x] Writeup added  

