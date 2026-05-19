## 문제
1. 문제 코드는 CBC로 암호화하고 ECB로 복호화한다.

2. ciphertext에서 앞의 16바이트는 iv이고 나머지 32바이트는 암호화된 FLAG이다.

$$ciphertext = (iv \\ || \\ C1 \\ || \\ C2)$$

## 풀이

   $$P1 = Dec(C1) \oplus iv$$

   $$P2 = Dec(C2) \oplus C1$$

   $$Plaintext = P1 \\ || \\ P2$$
