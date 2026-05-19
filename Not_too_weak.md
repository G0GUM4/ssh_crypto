## 1. semi-weak key pairs in DES

  $$E_{k_1}(E_{k_2}(M)) = M$$

   - 0x011F011F010E010E and 0x1F011F010E010E01
   - 0x01E001E001F101F1 and 0xE001E001F101F101
   - 0x01FE01FE01FE01FE and 0xFE01FE01FE01FE01
   - 0x1FE01FE00EF10EF1 and 0xE01FE01FF10EF10E
   - 0x1FFE1FFE0EFE0EFE and 0xFE1FFE1FFE0EFE0E
   - 0xE0FEE0FEF1FEF1FE and 0xFEE0FEE0FEF1FEF1

## 풀이
같은 키를 쓰면 안 된다. 따라서 semi-weak key를 사용한다.

1. `key1 = 011F011F010E010E`로 flag를 암호화한다.
2. `key2 = 1F011F010E010E01`로 위에서 얻은 암호문을 다시 암호화한다.


## 코드
```python3
from pwn import *
from Crypto.Util.Padding import unpad

HOST = ...
PORT = ...

k1 = "011F011F010E010E"
k2 = "1F011F010E010E01"

p = remote(HOST, PORT)

p.sendlineafter(b"> ", b"2")
p.sendlineafter(b"key(hex)> ", k1.encode())

enc_flag = p.recvline().decode().split("> ")[1].strip()

p.sendlineafter(b"> ", b"1")
p.sendlineafter(b"key(hex)> ", k2.encode())
p.sendlineafter(b"msg(hex)> ", enc_flag.encode())

enc2 = p.recvline().decode().split("> ")[1].strip()
result = bytes.fromhex(enc2)

flag_padded = result[:len(bytes.fromhex(enc_flag))]
flag = unpad(flag_padded, 8)

print(flag.decode())
```
