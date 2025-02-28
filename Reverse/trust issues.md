Extract the XOR key from _strcmp:

```byte local_20[] = {0x06, 0x11, 0x1D, 0x72, 0x60, 0x1F, 0x18, 0x7C, ...};```

Reverse the XOR operation using Python:

```
xor_values = [0x06, 0x11, 0x1D, 0x72, ...]
expected_string = "GRX14YcKLzXOlW5iaSlBIrN7"
flag = "".join(chr(ord(c) ^ x) for c, x in zip(expected_string, xor_values))
```