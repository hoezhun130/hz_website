---
layout: "post"
title: "JuniorCrypt CTF"
categories: [JuniorCrypt_CTF]
tags: "One-timePadCipher"
image: /assets/CTF/JuniorCryptCTF/logo.png
---

## Cryto/Unrevealed secret

**Challenge Description:**

The `one-time_pad.py` will generate a key to encrypt the flag using a one-time pad cipher, and the encrypted flag stored in `encrypted_flag.txt`.

```python
import random

def generate_string(length):
    # This function generates a random string of the specified length
    byte_list = [(random.randint(0, 127) + 256)//2 for _ in range(length)]
    byte_string = bytes(byte_list)
    utf8_string = byte_string.decode('utf-8', errors='replace')
    return utf8_string

def xor_cipher(message, key):
    # This function performs XOR encryption on the message and key
    message_nums = [ord(c) for c in message]
    key_nums = [ord(c) for c in key]
    cipher_nums = [m ^ k for m, k in zip(message_nums, key_nums)]
    return ''.join(chr(i) for i in cipher_nums)

# Example usage
flag = "grodno{fake_flag}"
key = generate_string(len(flag))
print("key:", key)

if len(flag) > len(key):
    raise ValueError("The key length must not be less than the message length")
if len(flag) < len(key):
    key = key[:len(flag)]

encrypted_flag = xor_cipher(flag, key)
print("encrypted_flag:", encrypted_flag)
with open("encrypted_flag.txt", 'w', encoding='utf-8') as file:
    file.write(encrypted_flag)
```

**Solution:**

To decrypt the flag, we need to reverse the encryption process. This involves regenerating the same key and using the XOR cipher to decrypt the encrypted flag.

```python
import random

def generate_string(length):
    byte_list = [(random.randint(0, 127) + 256)//2 for _ in range(length)]
    byte_string = bytes(byte_list)
    utf8_string = byte_string.decode('utf-8', errors='replace')
    return utf8_string

def xor_cipher(message, key):
    message_nums = [ord(c) for c in message]
    key_nums = [ord(c) for c in key]
    cipher_nums = [m ^ k for m, k in zip(message_nums, key_nums)]
    return ''.join(chr(i) for i in cipher_nums)

# Read the encrypted flag from the file
with open('encrypted_flag.txt', 'r', encoding='utf-8') as file:
    encrypted_flag = file.read()

# Generate the key of the same length as the encrypted flag
key = generate_string(len(encrypted_flag))

# Decrypt the flag using the same xor_cipher function
decrypted_flag = xor_cipher(encrypted_flag, key)
print("Decrypted Flag:", decrypted_flag)
```

**Flag:**

`grodno{Utf8_3ncod1ng_fe4ture5_c4n_ru1n}`