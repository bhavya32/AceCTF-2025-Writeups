Decompile with IDA Pro or Ghidra there is function named `p3xr9q_t1zz`.

```c
int p3xr9q_t1zz()
{
  char v1[27]; // [rsp+20h] [rbp-20h]
  char v2; // [rsp+3Bh] [rbp-5h]
  unsigned int i; // [rsp+3Ch] [rbp-4h]

  v1[0] = 29;
  v1[1] = 27;
  v1[2] = 71;
  v1[3] = 25;
  v1[4] = 117;
  v1[5] = 31;
  v1[6] = 29;
  v1[7] = 26;
  v1[8] = 90;
  v1[9] = 90;
  v1[10] = 25;
  v1[11] = 78;
  v2 = 42;
  printf("Success! Here is your output: ");
  for ( i = 0; i <= 0xB; ++i )
    putchar(v2 ^ (unsigned __int8)v1[i]);
  return putchar(10);
}
```

Just xor `29, 27, 71, 25, 117, 31, 29, 26, 90, 90, 25, 78` with `42`.