1. Triple DES

   $$ciphertext = E_{k_3}(D_{k_2}(E_{k_1}(plaintext)))$$

   $$plaintext = D_{k_1}(E_{k_2}(D_{k_3}(ciphertext)))$$

2. Weak keys in DES

   $$E_k(E_k(M)) = M$$
   
   - Alternating ones + zeros (0x0101010101010101)
   - Alternating 'F' + 'E' (0xFEFEFEFEFEFEFEFE)
   - '0xE0E0E0E0F1F1F1F1'
   - '0x1F1F1F1F0E0E0E0E'

3. `DES3.new(key, *args, **kwargs)`

   - `key(byte string)`: The secret key to use in the symmetric cipher. It must be 16 or 24 bytes long. The parity bits will be ignored.
  

# 풀이

1. `key = '0101010101010101FEFEFEFEFEFEFEFE'`로 FLAG를 암호화한다.
2. 위에서 얻은 암호문을 똑같은 key로 다시 암호화한다.
