```
def solve_ctf_flag():
    t1 = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/"
    output_pairs = ["SU", "IB", "VE", "Tz", "TE", "RF", "IE", "WT", "T1", "VU", "IE", "VG", "SH", "Qb", "VD", "IH",
                    "Qm", "QY", "Uz", "RU", "Nj", "NH", "IF", "TP", "RX", "Q3", "Tz", "RE", "ST", "Tl", "R1", "IP",
                    "SW", "Uz", "ID", "Tg", "Tz", "IA", "R2", "T8", "T3", "RN"]
    t = "I TOLD YOU THAT BASE64 DECODING IS NO GOOD"

    b_parts = []
    for i in range(min(len(t), 42)):
        char = t[i]
        bin_char = f"{ord(char):08b}"
        last_2_bits = bin_char[6:]

        
        second_index = t1.index(output_pairs[i][1])

        
        second_bin = f"{second_index:06b}"

        
        four_bits_from_b = second_bin[2:]
        b_parts.append(four_bits_from_b)

    
    b_binary = ''.join(b_parts)

    
    flag_chars = []
    for i in range(0, len(b_binary), 8):
        if i + 8 <= len(b_binary):
            byte = b_binary[i:i + 8]
            flag_chars.append(chr(int(byte, 2)))

    flag = ''.join(flag_chars)
    print(f"Extracted flag: {flag}")

    
    remaining_bits = len(b_binary) % 8
    if remaining_bits > 0:
        last_bits = b_binary[-remaining_bits:]
        print(f"Remaining bits that don't form a complete byte: {last_bits}")

    
    if len(flag) >= 1:
        last_char = flag[-1]
        print(f"Last recovered character: '{last_char}' (ASCII {ord(last_char)})")

        
        if ord(last_char) < 32 or ord(last_char) > 126:
            print("Warning: Last character is non-printable, flag might be truncated")

    return flag




recovered_flag = solve_ctf_flag()

```