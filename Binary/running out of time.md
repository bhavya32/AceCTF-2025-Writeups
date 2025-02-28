# Running Out of Time  

**Category:** Reverse Engineering  

A mysterious program prompts for a specific number, but the correct value changes every time it's executed. Your task is to analyze the binary, reverse-engineer the logic, and predict the correct input to trigger the win condition.  

---

### Challenge  

**Provided File:** `Running_Out_Of_Time.exe`  

---

## Overview  

1. **Understanding the Program Logic**  
   - The binary contains a function named `p3xr9q_t1zz`.  
   - This function operates on a predefined set of values, applying a transformation to generate an output.  

2. **Reverse-Engineering the Function**  
   - Decompiling the binary using **IDA Pro** or **Ghidra** reveals the logic inside `p3xr9q_t1zz`.  
   - The function stores a set of predefined values and XORs each of them with `42` before printing the result.  

3. **Extracting the Hidden Output**  
   - By manually performing the XOR operation, we can retrieve the intended output, which is the flag.  

---

## Steps to Exploit  

1. **Decompile the Binary**  
   - Load `Running_Out_Of_Time.exe` into **IDA Pro** or **Ghidra**.  
   - Locate the function `p3xr9q_t1zz`.  

2. **Extract the Hidden Data**  
   - Inside the function, we find a predefined array of numbers:  
     ```plaintext
     29, 27, 71, 25, 117, 31, 29, 26, 90, 90, 25, 78
     ```
   - These values are XORed with `42` before being printed as characters.  

3. **Reconstruct the Flag**  
   - Apply the XOR operation manually to each value:  
     ```python
     values = [29, 27, 71, 25, 117, 31, 29, 26, 90, 90, 25, 78]
     key = 42

     flag = ''.join(chr(v ^ key) for v in values)
     print("Extracted Flag:", flag)
     ```
   - This reveals the flag when executed.  

---

## Exploit Script  

```python
# Reverse-Engineering the XOR Operation
values = [29, 27, 71, 25, 117, 31, 29, 26, 90, 90, 25, 78]
key = 42

# XOR each value with 42 to get the original characters
flag = ''.join(chr(v ^ key) for v in values)
print("Extracted Flag:", flag)
```

---
