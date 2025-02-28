# Super Secure Encryption  

**Category:** Cryptography  

The challenge presents an encryption method that follows a **XOR-based stream cipher** approach. We are given a **plaintext message**, an **encrypted message**, and an **encrypted flag**. Our goal is to extract the keystream used in encryption and recover the original flag.  

---

### Challenge  

**Provided File:** `msg.txt`, `cipher.txt`  

**Given Data from `msg.txt`**:  
- **Encrypted message (hex)**:  
  ```
  d71f4a2fd1f9362c21ad33c7735251d0a671185a1b90ecba27713d350611eb8179ec67ca7052aa8bad60466b83041e6c02dbfee738c2a3
  ```
- **Encrypted flag (hex)**:  
  ```
  c234661fa5d63e627bef28823d052e95f65d59491580edfa1927364a5017be9445fa39986859a3
  ```

---

## Overview  

1. **Understanding the Encryption Method**  
   - The encryption uses **XOR** between the plaintext and a keystream.  
   - The keystream is **reused** to encrypt both the given plaintext and the flag.  
   - Since we have both plaintext and its corresponding encrypted form, we can **derive the keystream**.  

2. **Extracting the Keystream**  
   - XOR the plaintext with the encrypted message to obtain the keystream:  
     ```python
     keystream = plaintext ⊕ encrypted_message
     ```

3. **Decrypting the Flag**  
   - Once the keystream is extracted, XOR it with the encrypted flag to retrieve the original flag:  
     ```python
     flag = keystream ⊕ encrypted_flag
     ```

---

## Steps to Solve  

1. **Convert Hex to Bytes**  
   - Decode the given hex values into raw bytes.  

2. **Derive the Keystream**  
   - XOR the known **plaintext message** with the **encrypted message** to extract the keystream.  

3. **Decrypt the Flag**  
   - XOR the extracted **keystream** with the **encrypted flag** to recover the plaintext flag.  

---

## Script Used  

```python
from binascii import unhexlify

# Given data
plaintext_msg = b'This is just a test message and can totally be ignored.'
encrypted_msg_hex = "d71f4a2fd1f9362c21ad33c7735251d0a671185a1b90ecba27713d350611eb8179ec67ca7052aa8bad60466b83041e6c02dbfee738c2a3"
encrypted_flag_hex = "c234661fa5d63e627bef28823d052e95f65d59491580edfa1927364a5017be9445fa39986859a3"

# Convert hex to bytes
encrypted_msg = unhexlify(encrypted_msg_hex)
encrypted_flag = unhexlify(encrypted_flag_hex)

# Extract keystream using XOR
keystream = bytes([p ^ c for p, c in zip(plaintext_msg, encrypted_msg)])

# Decrypt flag using XOR
flag = bytes([k ^ c for k, c in zip(keystream, encrypted_flag)])

# Output the flag
print(flag.decode())  # This should print the flag
```

---


Executing the script successfully decrypts the flag:  
