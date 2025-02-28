Challenge Name: Hexed and Squared
Category: Cryptography
Flag Format: ACECTF{some_string}

Challenge Description:

The challenge suggests a custom encoding using the number 3 and provides a hint: “hex decode continuously”. The encoded file contains a long sequence of 3s with some variations.

Solution Approach:
    
Analyze the Data:
•    The provided file consists of a long string of the digit 3, which could represent hexadecimal values.
Continuous Hex Decoding:
•    Since the hint suggests decoding continuously, we attempt to interpret the string as hex and decode iteratively.
•    Convert the hex values to ASCII text multiple times until we retrieve meaningful text.
Extract the Flag:
•    After multiple decoding attempts, the flag appears in a readable format.
•    Some characters may be misplaced due to formatting issues, so a minor manual correction is needed.

Final Flag:

ACECTF{5uch_4_5qu4r3}
