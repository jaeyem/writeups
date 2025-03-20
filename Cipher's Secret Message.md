# CTF Challenge: Decoding the Secret Message

[![CTF Challenge](https://img.shields.io/badge/CTF-Challenge-blue)](https://github.com/your-repo)

---

## Overview

In this challenge, a secret message was recovered from an old system along with its encryption algorithm. Your task is to decode the message and extract the hidden flag.

---

## Challenge Details

**Task:**  
Help Void decode the secret message!

**Encrypted Message:**  
a_up4qr_kaiaf0_bujktaz_qm_su4ux_cpbq_ETZ_rhrudm


**Encryption Algorithm:**  
The algorithm used to encrypt the message is provided as a photo. Please refer to the image below for the complete instructions.

![Encryption Instructions](https://github.com/user-attachments/assets/5e5fdd9d-4056-43b3-9273-94678cb55824)  
*Figure: Photo of the encryption algorithm instructions*

---

## How the Encryption Works

The algorithm processes each character of the message following these steps:

1. **Alphabet Check:**  
   - Verify if the character is an alphabetical letter.
   
2. **Determine Base Value:**  
   - Use `ord('A')` for uppercase letters.
   - Use `ord('a')` for lowercase letters.

3. **Convert to a 0–25 Range:**  
   - Compute the letter's position by calculating `ord(c) - base`.

4. **Shift by Character Index:**  
   - Subtract the character's index (its position in the string) from its calculated position.

5. **Wrap Around Using Modulo:**  
   - Apply `% 26` to ensure the shift stays within the bounds of the alphabet.

6. **Convert Back to a Character:**  
   - Convert the shifted number back to a letter using `chr(... + base)`.

7. **Non-Alphabetical Characters:**  
   - Leave characters like numbers and underscores unchanged.

---
## Code Walk-through

Below is the Python function that implements the decryption process:

```python
def dec(ciphertext):
    # Initialize an empty string to store the decrypted message.
    result = ""
    
    # Loop over each character in the ciphertext along with its index.
    for i, c in enumerate(ciphertext):
        # Check if the current character is an alphabetical letter.
        if c.isalpha():
            # Determine the base ASCII value:
            # - If the character is uppercase, use ord('A') as the base.
            # - If the character is lowercase, use ord('a') as the base.
            base = ord('A') if c.isupper() else ord('a')
            
            # Decrypt the character:
            # 1. Convert the character to its position in the alphabet (0-25) using ord(c) - base.
            # 2. Reverse the encryption by subtracting the character's index (i).
            # 3. Use modulo 26 to handle wrap-around within the alphabet.
            # 4. Convert back to the character by adding the base and using chr().
            result += chr((ord(c) - base - i) % 26 + base)
        else:
            # For non-alphabetical characters (e.g., numbers, underscores), keep them unchanged.
            result += c
    
    # Return the complete decrypted message.
    return result

# Encrypted message from the system.
ciphertext = "a_up4qr_kaiaf0_bujktaz_qm_su4ux_cpbq_ETZ_rhrudm"

# Decode the message using the decryption function.
plaintext = dec(ciphertext)

# Print the decrypted message to the console.
print("Decrypted message:", plaintext)
```

## Decrypted message: 
a_sm4ll_crypt0_message_to_st4rt_with_THM_cracks

## What is the flag?
THM{a_sm4ll_crypt0_message_to_st4rt_with_THM_cracks}
