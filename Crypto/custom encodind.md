# Custom Encoding Scheme  

**Category:** Cryptography  

This challenge involves a **custom encoding scheme** that modifies Base64-like encoding. Instead of explaining the logic, we are given an encryption script (`encrypt.py`) and an encoded output (`output.txt`). Our task is to reverse the encoding process and retrieve the original flag.  

---

### Challenge  

**Provided Files:**  
- `encrypt.py` (contains the encoding logic)  
- `output.txt` (contains the encoded message)  

---

## Overview  

1. **Understanding the Encoding Script (`encrypt.py`)**  
   - The script defines a function `e1(t, b, o)`, which takes:  
     - `t`: A fixed text (`"I TOLD YOU THAT BASE64 DECODING IS NO GOOD"`)  
     - `b`: A required input of 168 bits (`{REDACTED}` in the script)  
     - `o`: The output file where encoded pairs are written  
   - It encodes each character from `t` into **two Base64 characters** using a transformation.  

2. **Decoding Process**  
   - The **first** character of each encoded pair is derived from the first **6 bits** of the ASCII character of `t`.  
   - The **second** character is created using a combination of the last **2 bits** of `t`'s ASCII character and an external input (`b`).  
   - The `output.txt` file stores these encoded character pairs, which need to be reversed to retrieve the original flag.  

---

## Steps to Solve  

1. **Extract the Encoding Logic**  
   - The encoding script maps characters using the standard Base64 alphabet:  
     ```
     "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/"
     ```
   - The encoding involves bitwise transformations and an unknown **168-bit secret value (`b`)**.  

2. **Reverse the Encoding Process**  
   - Identify the second character from each encoded pair.  
   - Find its index in the Base64 table and extract relevant bits.  
   - Reconstruct the original ASCII values from the combined extracted bits.  

3. **Reconstruct the Flag**  
   - Convert the retrieved binary sequence into readable characters.  

---

## Script Used  

The following script was used to extract the flag from the encoded output:  

```python
def solve_ctf_flag():
    t1 = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/"
    output_pairs = ["SU", "IB", "VE", "Tz", "TE", "RF", "IE", "WT", "T1", "VU", "IE", "VG", "SH", "Qb", "VD", "IH",
                    "Qm", "QY", "Uz", "RU", "Nj", "NH", "IF", "RP", "RX", "Q3", "Tz", "RE", "ST", "Tl", "R1", "IP",
                    "SW", "Uz", "ID", "Tg", "Tz", "IA", "R2", "T8", "T3", "RN"]
    t = "I TOLD YOU THAT BASE64 DECODING IS NO GOOD"

    b_parts = []
    for i in range(min(len(t), 42)):
        char = t[i]
        bin_char = f"{ord(char):08b}"
        last_2_bits = bin_char[6:]

        
        second_index = t1.index(output_pairs[i][1])

        
        second_bin = f"{second_index:06b}"

        
        four_bits_from_b = second_bin[2:]
        b_parts.append(four_bits_from_b)

    
    b_binary = ''.join(b_parts)

    
    flag_chars = []
    for i in range(0, len(b_binary), 8):
        if i + 8 <= len(b_binary):
            byte = b_binary[i:i + 8]
            flag_chars.append(chr(int(byte, 2)))

    flag = ''.join(flag_chars)
    print(f"Extracted flag: {flag}")

    
    remaining_bits = len(b_binary) % 8
    if remaining_bits > 0:
        last_bits = b_binary[-remaining_bits:]
        print(f"Remaining bits that don't form a complete byte: {last_bits}")

    
    if len(flag) >= 1:
        last_char = flag[-1]
        print(f"Last recovered character: '{last_char}' (ASCII {ord(last_char)})")

        
        if ord(last_char) < 32 or ord(last_char) > 126:
            print("Warning: Last character is non-printable, flag might be truncated")

    return flag

recovered_flag = solve_ctf_flag()
```

---

### Extracted Flag  

After executing the script, we get the flag:  

```
Extracted flag: ACECTF{7h47_w45_c00l}
```
