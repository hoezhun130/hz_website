---
layout: "post"
title: "Recette Secrète"
categories: [SKR_CTF, Cryptography]
tags: "Cryptography Salt Pepper"
---

## Challenge Overview
- **Challenge Description:**
>Godam send me a secret recipe from French, but I can't find the ingredient for Password! What does it mean? <br><br>
Flag format: SKR{flag}

- **Hint:**
>What is Salt and Pepper in Password Hashing?

## Provided Files
- |-- [**secret_recipe.zip**](/hz_website/assets/CTF/SKR_CTF/Cryptography/Recette_Secrète/secret_recipe.zip)
|   |-- Ingredients/<!-- Subfolder -->
|   |   |-- [Beans](/hz_website/assets/CTF/SKR_CTF/Cryptography/Recette_Secrète/secret_recipe/Ingredients/Beans)
|   |   |-- [Carrot](/hz_website/assets/CTF/SKR_CTF/Cryptography/Recette_Secrète/secret_recipe/Ingredients/Carrot)
|   |   |-- [Passwords](/hz_website/assets/CTF/SKR_CTF/Cryptography/Recette_Secrète/secret_recipe/Ingredients/Passwords)
|   |   |-- [Pepper](/hz_website/assets/CTF/SKR_CTF/Cryptography/Recette_Secrète/secret_recipe/Ingredients/Pepper)
|   |   |-- [Salt](/hz_website/assets/CTF/SKR_CTF/Cryptography/Recette_Secrète/secret_recipe/Ingredients/Salt)
|   |   |-- [Water](/hz_website/assets/CTF/SKR_CTF/Cryptography/Recette_Secrète/secret_recipe/Ingredients/Water)
|   |-- [Product](/hz_website/assets/CTF/SKR_CTF/Cryptography/Recette_Secrète/secret_recipe/Product)
|   |-- [recipe.png](/hz_website/assets/CTF/SKR_CTF/Cryptography/Recette_Secrète/secret_recipe/recipe.png)

## Solution
![light mode only](/hz_website/assets/CTF/SKR_CTF/Cryptography/Recette_Secrète/kali_output.png){: .light .w-75 .shadow .rounded-10 w='1212' h='668' }
![dark mode only](/hz_website/assets/CTF/SKR_CTF/Cryptography/Recette_Secrète/kali_output.png){: .dark .w-75 .shadow .rounded-10 w='1212' h='668' }

The first step was to read the contents of each provided files. By inpecting the files, I noticed that the files within the `Ingredients` folder seems to be the fragments of the flag. The begining and ending of the flag were identified as `SKR{Brut3_` and `P3pp3r}`. However, there remained a gap in the middle of the flag that required filling.

![light mode only](/hz_website/assets/CTF/SKR_CTF/Cryptography/Recette_Secrète/kali_output2.png){: .light .w-75 .shadow .rounded-10 w='1212' h='668' }
![dark mode only](/hz_website/assets/CTF/SKR_CTF/Cryptography/Recette_Secrète/kali_output2.png){: .dark .w-75 .shadow .rounded-10 w='1212' h='668' }

The `Passwords` file contained a list of passwords. At this stage, the purpose of this password lst was not entirely clear and further investigations are required.

![light mode only](/hz_website/assets/CTF/SKR_CTF/Cryptography/Recette_Secrète/secret_recipe/recipe.png){: .light .w-75 .shadow .rounded-10 w='1212' h='668' }
![dark mode only](/hz_website/assets/CTF/SKR_CTF/Cryptography/Recette_Secrète/secret_recipe/recipe.png){: .dark .w-75 .shadow .rounded-10 w='1212' h='668' }


As we know the flag had a starting point with `Beans` and concluded with `Pepper`, so I assumed that the `recipe.png` hinted at the arrangement of the flag. With this assumption, a temporarily constructed flag emerged: `SKR{Brut3_Forc1nG_Passwords_H4sH_W1tH_S4lt&P3pp3r}`. `Passwords` serves as a placeholder in the temporarily constructed flag because i didn't have a clear indication regrading the specific password to be inserted between `Forc1nG_` and `_H4sH_W1tH_`.

![light mode only](/hz_website/assets/CTF/SKR_CTF/Cryptography/Recette_Secrète/kali_output3.png){: .light .w-75 .shadow .rounded-10 w='1212' h='668' }
![dark mode only](/hz_website/assets/CTF/SKR_CTF/Cryptography/Recette_Secrète/kali_output3.png){: .dark .w-75 .shadow .rounded-10 w='1212' h='668' }

a

![light mode only](/hz_website/assets/CTF/SKR_CTF/Cryptography/Recette_Secrète/Password_Hashing.png){: .light .w-75 .shadow .rounded-10 w='1212' h='668' }
![dark mode only](/hz_website/assets/CTF/SKR_CTF/Cryptography/Recette_Secrète/Password_Hashing.png){: .dark .w-75 .shadow .rounded-10 w='1212' h='668' }

```python
import hashlib

# Provided ingredients
water = "Forc1nG_"
salt = "S4lt&"
pepper = "P3pp3r}"
beans = "SKR{Brut3_"
carrot = "_H4sH_W1tH_"
product_hash = "0edcbe97ba900dda8bbafe2498d38d8b"

# Read passwords from the file
with open("passwords.txt", "r") as file:
    # Assuming each line in the file is a password
    passwords = [line.strip() for line in file]

# Hash function
def hash_password(password):
    return hashlib.md5(password.encode()).hexdigest()

# Iterate through passwords and check against the product hash
for password in passwords:
    full_password = beans + water + password + carrot + salt + pepper

    # Hash the full password
    hashed_candidate = hash_password(full_password)

    # Print each full_password
    print(f"Testing: {full_password}")

    # Check if the hash matches the product hash
    if hashed_candidate == product_hash:
        print(f"Password found: {password}")
        break
else:
    print("Password not found in the provided list.")
```