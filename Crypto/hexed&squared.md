# Hexed and Squared  

**Category:** Cryptography  

This challenge presents an encoded file filled with repeated occurrences of the digit **3**, with some variations. The hint suggests "hex decode continuously," indicating that the data has undergone multiple rounds of hex encoding. The goal is to decode the sequence iteratively until the flag is revealed.  

---

### Challenge  

**Provided File:** `encoded.txt`  

**Flag Format:** `ACECTF{some_string}`  

---

## Overview  

1. **Understanding the Encoding Scheme**  
   - The content consists of a long sequence of the digit **3** with some variations.  
   - The data likely represents **hexadecimal** values that need repeated decoding.  

2. **Continuous Hex Decoding**  
   - Start interpreting the content as hexadecimal.  
   - Decode iteratively until readable ASCII text appears.  
   - Some characters may be misplaced due to formatting issues, requiring manual correction.  

3. **Extracting the Flag**  
   - The decoded output should eventually reveal a string matching the flag format.  

---

## Steps to Solve  

1. **Inspect the Encoded Data**  
   - Use a command-line tool to check the structure:  
     ```bash
     cat encoded.txt
     ```  
   - Convert hex to ASCII iteratively:  
     ```bash
     xxd -r -p encoded.txt
     ```  

2. **Perform Continuous Hex Decoding**  
   - The output from the first decoding may still be encoded.  
   - Repeat the hex-decoding process until meaningful text is extracted.  

3. **Extract the Flag**  
   - Once a readable format appears, verify if it follows the `ACECTF{}` flag pattern.  
   - Make minor adjustments if any characters are misplaced.  

---

### Final Flag  

After multiple rounds of decoding, the flag retrieved is:  

```
ACECTF{5uch_4_5qu4r3}
```
