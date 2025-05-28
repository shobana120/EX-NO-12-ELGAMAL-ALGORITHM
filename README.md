# EX-NO-12-ELGAMAL-ALGORITHM

## AIM:
To Implement ELGAMAL ALGORITHM

## ALGORITHM:

1. ElGamal Algorithm is a public-key cryptosystem based on the Diffie-Hellman key exchange and relies on the difficulty of solving the discrete logarithm problem.

2. Initialization:
   - Select a large prime \( p \) and a primitive root \( g \) modulo \( p \) (these are public values).
   - The receiver chooses a private key \( x \) (a random integer), and computes the corresponding public key \( y = g^x \mod p \).

3. Key Generation:
   - The public key is \( (p, g, y) \), and the private key is \( x \).

4. Encryption:
   - The sender picks a random integer \( k \), computes \( c_1 = g^k \mod p \), and \( c_2 = m \times y^k \mod p \), where \( m \) is the message.
   - The ciphertext is the pair \( (c_1, c_2) \).

5. Decryption:
   - The receiver computes \( s = c_1^x \mod p \), and then calculates the plaintext message \( m = c_2 \times s^{-1} \mod p \), where \( s^{-1} \) is the modular inverse of \( s \).

6. Security: The security of the ElGamal algorithm relies on the difficulty of solving the discrete logarithm problem in a large prime field, making it secure for encryption.

## Program:
```
import random

def mod_exp(base, exp, mod):
    result = 1
    while exp > 0:
        if exp % 2 == 1:
            result = (result * base) % mod
        base = (base * base) % mod
        exp //= 2
    return result

def elgamal_keygen(p, g):
    x = random.randint(2, p-2)  # Private key (x)
    y = mod_exp(g, x, p)  # Public key (y)
    return (p, g, y), x  # Return public key and private key

def elgamal_encrypt(public_key, m, p):
    (p, g, y) = public_key
    k = random.randint(2, p-2)  # Random value
    c1 = mod_exp(g, k, p)  # c1 = g^k mod p
    c2 = (m * mod_exp(y, k, p)) % p  # c2 = (m * y^k) mod p
    return (c1, c2)

def elgamal_decrypt(private_key, ciphertext, p):
    (c1, c2) = ciphertext
    x = private_key
    s = mod_exp(c1, x, p)  # Compute shared secret (s = c1^x mod p)
    s_inv = mod_exp(s, p-2, p)  # Modular inverse of s (s^-1 mod p)
    m = (c2 * s_inv) % p  # Decrypt message (m = (c2 * s^-1) mod p)
    return m

def main():
    p = int(input("Enter a prime number p: "))
    g = int(input("Enter a primitive root g: "))
    
    public_key, private_key = elgamal_keygen(p, g)
    print(f"Public Key: {public_key}")
    print(f"Private Key: {private_key}")

    m = int(input("Enter a message (as a number): "))
    
    ciphertext = elgamal_encrypt(public_key, m, p)
    print(f"Ciphertext: {ciphertext}")
    
    decrypted_message = elgamal_decrypt(private_key, ciphertext, p)
    print(f"Decrypted Message: {decrypted_message}")

main()
```

## Output:

![image](https://github.com/user-attachments/assets/b6ae939c-1ef5-4c53-afec-62b663e0bbda)


## Result:
The program is executed successfully.
