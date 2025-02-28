Decompile the program with IDA Pro or Ghidra reveal there are some step to encrypt the data with XOR.

Because options 3 if i remember check if the input bytes is correct or wrong with `108, 44, 224, 239, 141, 96, 220, 117, 13, 255, 214, 89, 244, 93, 222, 155, 227, 215, 82, 153, 90, 124, 163, 201, 78, 27, 69, 229, 192, 41, 154` so this should be the end output of encryption.

So we need to reverse that bytes back to the plain text.

```py
def xor_encrypt_decrypt(data, key):
    return bytearray([b ^ key[i % len(key)] for i, b in enumerate(data)])

def reverse_xor_prev(data):
    decrypted = bytearray(len(data))
    prev = 0
    for i in range(len(data)):
        decrypted[i] = data[i] ^ prev
        prev = data[i]
    return decrypted

data = bytes([108, 44, 224, 239, 141, 96, 220, 117, 13, 255, 214, 89, 244, 93, 222, 155, 227, 215, 82, 153, 90, 124, 163, 201, 78, 27, 69, 229, 192, 41, 154])
key = bytes([123, 46, 241, 235, 139, 118, 231, 104, 119, 163, 239, 82, 246, 60, 218, 170, 246, 167, 67, 235, 33, 36, 195, 156, 125, 8, 51, 183, 247, 44, 180])

data = xor_encrypt_decrypt(data, key)
data = reverse_xor_prev(data)
data = bytearray([b ^ 86 for b in data])

print(''.join(chr(b) for b in data))
```