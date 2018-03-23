# Angstrom CTF : XOR

**Category:** Crypto 
**Points:** 40
 

> We found these mysterious symbols (fbf9eefce1f2f5eaffc5e3f5efc5efe9fffec5fbc5e9f9e8f3eaeee7) hidden in ancient (1950s-era) ruins. We think a single byte may be key to unlocking the mystery. Can you help us figure out what they mean?
> 
> 
>  HINTS
> 
> I cancel myself out, create from nothing, and negate from everything. What am I?



## Write-up

We are only given a ciphertext of fbf9eefce1f2f5eaffc5e3f5efc5efe9fffec5fbc5e9f9e8f3eaeee7 to decrypt for this challenge.

The ciphertext looks like it is in hex because the values range from numbers up until the letter f, which is the largest single hexadecimal value.

XOR is exclusive-or which is basically:
>0 or 0 = 0
>0 or 1 = 1
>1 or 0 = 1
>1 or 1 = 0
Knowing this I decided to convert the ciphertext into binary since it will be easier to xor in binary.

The challenge description also states that a single byte may be the key to unlocking the mystery.  One hex value is a nibble, or 4 bits so two hex values is equal to a byte which is 8 bits.

I checked the length of the ciphertext and saw it was 56 characters long, so I could split it into 23 sections with 2 characters in each section.

The flag format for the ctf usually begins with actf{ so knowing this we can try to solve for the start of the ciphertext.

I converted


