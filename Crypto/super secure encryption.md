```
from binascii import unhexlify


plaintext_msg = b'This is just a test message and can totally be ignored.'
encrypted_msg_hex = "d71f4a2fd1f9362c21ad33c7735251d0a671185a1b90ecba27713d350611eb8179ec67ca7052aa8bad60466b83041e6c02dbfee738c2a3"
encrypted_flag_hex = "c234661fa5d63e627bef28823d052e95f65d59491580edfa1927364a5017be9445fa39986859a3"
encrypted_msg = unhexlify(encrypted_msg_hex)
encrypted_flag = unhexlify(encrypted_flag_hex)
keystream = bytes([p ^ c for p, c in zip(plaintext_msg, encrypted_msg)])
flag = bytes([k ^ c for k, c in zip(keystream, encrypted_flag)])

print(flag.decode())  # This should print the flag

```