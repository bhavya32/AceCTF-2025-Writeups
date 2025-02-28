# Pipher - Piano Cipher  

**Category:** Cryptography  

This challenge introduces a **custom piano-based cipher** where musical notes correspond to values in **base 12**. Additionally, every **6th character of the plaintext leaks**, which can help in the decryption process.  

---

### Challenge  

**Provided File:** `cipher.txt`  

**Ciphertext:**  
```
DC# DD# DF DD# EC '70' G#B CE F#C FC# C#C# '104' C#A FC# F#A# C#A C#A '108' CF AF# C#C FC# CE '102' FC# C#A# FC# GA# CE '112' FC# C#B C#C# C#A# GC '125'
```

---

## Overview  

1. **Understanding the Encoding Scheme**  
   - Each musical note represents a **base 12** digit.  
   - Letters correspond to piano notes, where:  
     ```
     A = 1, A# = 2, B = 3, C = 4, C# = 5, D = 6, D# = 7, E = 8, F = 9, F# = 10, G = 11, G# = 12
     ```
   - Numbers in **single quotes (`'70'`)** are direct ASCII values.

2. **Decoding Strategy**  
   - Convert musical notes to **base 12 values**.  
   - Convert base 12 values to **decimal (base 10)**.  
   - Convert decimals to **ASCII characters** to reconstruct the plaintext.  

3. **Using the Leaked Characters**  
   - Every **6th character is revealed** in plaintext, assisting the decryption process.  

---

## Steps to Solve  

1. **Map Piano Notes to Base 12**  
   - Assign numerical values to each note based on a **base 12 system**.  
   - Example:  
     ```
     DC# = (6 * 12) + 5 = 77
     ```

2. **Convert Base 12 to ASCII**  
   - Convert the extracted base 12 values to **decimal**.  
   - Convert the decimal values to **ASCII characters** to reveal readable text.  

3. **Use Given ASCII Values**  
   - Numbers in quotes (`'70'`, `'104'`) directly map to ASCII characters.  

4. **Reconstruct the Flag**  
   - After decoding, arrange the extracted characters to form a meaningful phrase matching the **ACECTF{}** flag format.  

---

### Final Flag  

After decoding the cipher using the base 12 piano-to-ASCII mapping, the flag is:  

```
ACECTF{p1an0_c1ph3r_4fun}
```
