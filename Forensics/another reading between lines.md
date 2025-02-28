# Another Reading Between the Lines?  

**Category:** Steganography / Encoding  

This challenge involves analyzing a **text file with hidden data** embedded within **line break formats**. The goal is to extract the encoded information by converting **newline variations** into binary and then decoding it into ASCII text.  

---

### Challenge  

**Provided File:** `hidden`  

---

## Overview  

1. **Understanding the Encoding Technique**  
   - The file appears to contain text formatted with a mix of **Carriage Return + Line Feed (CRLF)** and **Line Feed (LF)**.  
   - These line break variations can be interpreted as **binary values**:  
     - `CRLF (\r\n) → 1`  
     - `LF (\n) → 0`  

2. **Extracting Hidden Data**  
   - By reading the file’s **newline formatting**, a binary string is formed.  
   - This binary data can be **converted to ASCII characters** to reveal the flag.  

---

## Steps to Solve  

1. **Identify Line Break Patterns**  
   - Use a command-line tool to inspect different newline characters:  
     ```bash
     cat -A hidden  # Displays hidden characters (LF = $, CRLF = ^M$)
     ```
   - Verify if `CRLF` and `LF` follow a consistent **binary pattern**.  

2. **Convert Newline Encodings to Binary**  
   - Map `CRLF` to **1** and `LF` to **0**.  
   - Construct a binary string by reading the line endings.  

3. **Convert Binary to ASCII**  
   - Split the binary string into **8-bit segments**.  
   - Convert each segment to **ASCII characters**.  

---

### Final Flag  

After decoding the binary pattern hidden in newline formatting, the extracted flag is:  

```
ACECTF{n0_r34d1n6_be7w33n_7h3_l1n35}
```
