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
```
0 or 0 = 0
0 or 1 = 1
1 or 0 = 1
1 or 1 = 0
```
Knowing this I decided to convert the ciphertext into binary since it will be easier to xor in binary.

The challenge description also states that a single byte may be the key to unlocking the mystery.  One hex value is a nibble (4 bits) and two hex values is equal to a byte (8 bits).

I checked the length of the ciphertext and saw it was 56 characters long, so I could split it into 23 sections with 2 characters in each section.

The flag format for the ctf usually begins with actf{ so knowing this we can try to solve for the start of the ciphertext.

I converted fb into its byte format which was:
```
11111010
```
Then I checked for the ascii binary value of the letter a which was:
```
01100001
```
Knowing that the binary value of a was the desired output I had to find a byte value to xor with fb that would equal a, and that value was:
```
10011010
```
We now check the second byte of f9 to see if when xor'ed with the key will equal to the ascii value of c, since c is the next value in the flag format actf{.

```
11111001
10011010
________
01100011
```

Converting 01100011 into ascii we see that it is indeed equal to c.

At this point I can make a simple python script to finish the rest of the flag.
```
#ciphertext
value = "fbf9eefce1f2f5eaffc5e3f5efc5efe9fffec5fbc5e9f9e8f3eaeee7"

#changes the ciphertext from hex to binary
b = bin(int(value, 16))
b = b[2:]

#splits the binary list value into byte-sized sections
x = [b[i:i+8] for i in range(0, len(b), 8)]

#For loop to iterate through the list of seperated values.
for n in x:
	
   #Turns the byte into a decimal value
   l = int(n,2)
	
   #XOR's the decimal value with our key 10011010, which in decimal is 154
   l = l ^ 154
   
   #Prints the flag
   print(chr(l), end='')
 ```
We then get the flag of: actf{hope_you_used_a_script}


