# Cryptography

<br>![miscellaneous image](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/resources/miscellany.jpg)

## Table of Contents
+ [Classical Cryptography](#classical-cryptography)
+ [Modern Cryptography](#modern-cryptography)
+ [Private-Key Encryption](#private-key-encryption)
+ [Message Authentication Codes](#message-authentication-codes)
+ [Number Theory](#number-theory)
+ [Key Exchange and Public-Key Encryption](#key-exchange-and-public-key-encryption)
+ [Digital Signatures](#digital-signatures)
+ [References](#references)


## Classical Cryptography

### Preliminaries

**Modular arithmetic**:

- $x = x'\mod N$ if and only if N divides $x-x'$   (i.e. x and x' have the same remainder when divided by N) (i.e. n divides x-x')
- $[x\mod N]$ = Remainder when x is divided by N
  - i.e. the unique value $x'\in\{0, ..., N-1\}$ such that $x = x'\mod N$

Example:

- $25 = 35\mod 10$ (because both have the same remainder)
- $25 \neq [35\mod 10]$
- $5 = [35\mod 10]$

**Numeric bases**:  

- **Binary** (base 2): Bit. Range [0, 1]
- **Decimal** (base 10): Range [0, 9]
- **Hexadecimal** (base 16): It's convenient because there's one to one correspondence between the 16 hex digits and the 16 possible sequences of 4 bits (half byte, nibble). Usually represented with prefix 0x. Ranges [0, 9] &cup; [A, F]. 

**Base conversions**:

- __Binary to Decimal__: Consider that each successive digit in a binary number has a value twice the preceding one, and add up only those that correspond to a digit 1. Example: 1101 = 8·1 + 4·1 + 2·0 + 1·1 = 13

- __Hex to Decimal__: Like binary to decimal, but each position has value 16 times (not twice) the previous one. Example: 0x1AF = 32·1 + 16·A + 1·F = 32·1 + 16·10 + 1·15 = 207

- __Hex to Binary__: Replace each hex digit with its corresponding nibble. Example: 0x1A = 0001 1010

How to store an hex value to a file? Two options: 

- Native hex: Use the bits it represents, though you get an unprintable character.
- Text: Use ASCII characters, though it will take more bytes (one byte per digit instead of half).

**ASCII**: Usual representation of characters (1 char = 1 byte = 2 hex digits). Example: 'F' = 0100 0110 = 0x46.

**Probability**:

**Event**: Particular occurrence in some experiment (Pr[E] = probability of even E).

**Conditional probability**: Probability that one event (A) occurs, assuming some other event (B) occurred (Pr[A|B] = Pr[A and B] / Pr[B]).

**Random variable**: Variable that takes on values (discrete or not) with certain probabilities. Its probability distribution specifies the probabilities with which the variable takes on each possible value.

**Independent random variables**: Two random values X, Y are independent if for all x, y: Pr[X=x | Y=y] = Pr[X=x] (i.e. the fact that Y takes any value is irrelevant for determining the probability with which X takes on a particular value.

**Law of total probability** (LTP): If we have a set of events $\{E_1, ..., E_n\}$ which are a partition of all possibilities (i.e. both $E_i$ and $E_j$ cannot occur simultaneously) (i.e. $E_i$ and $E_j$ are pairwise impossible), then for any A:  

$$Pr[A] = \sum_{i=0}^n Pr[A \land E_i] = \sum_{i=0}^nPr[A|E_i]·Pr[E_i]$$

**Bayes theorem** (BT): It's a way of switching the order of 2 events in a conditional probability statement. It says:  

$$Pr[A|B] = Pr[B|A]·Pr[A]/Pr[B]$$

### Classical Cryptography

Cryptography is everywhere: passwords, password hashing, secure internet credit-card transactions, encrypted Wi-Fi, disk encryption, digitally signed software updates, bitcoin, etc.

**Historical cryptography** (until 1970s): Art of writing and solving codes. It focused exclusively on ensuring secret communication between two parties sharing secret information in advance (key, or "codes").

**Modern cryptography**: Science about design, analysis, and implementation of mathematical techniques for securing information, systems, and computation against adversarial attack. Unlike old cryptography, modern cryptography has formal definitions. To get a formal definition of a scheme, we have to define "security", make some asumptions (we assume some problems cannot be solved efficiently), and prove that our scheme satisfies our "security" definition under these assumptions (security proof, instead of design-break-patch cycle). Still, it's partly an art (there is room for creativity): new definitions, new schemes, new proof of security, or validating assumptions and designing new primitives to satisfy them. Proof of security is a guarantee of security only for a security definition and a set of assumptions (if it's broken, then the security definition doesn't correspond to reality or assumption is invalid).

**Private-key cryptography** (AKA secret-key/shared-key/symmetric-key cryptography): Alice and Bob want to share secret information. Both have a shared secret key in advance. The sender encrypts a message/plaintext using the key, generating a ciphertext that is sent over a public communication channel. The receiver decrypts that ciphertext using the key to recover the original message. This is also commonly used for ensuring secrecy for a single user communicating with himself over time. This encryption scheme is defined by:

- **m**: Message from message space M (i.e. subset of M).
- **Gen** (key-generation algorithm): Generates k randomly (k belongs to K space).
- **Enc** (encryption algorithm): Takes m and k, and outputs ciphertext **c** ($`c&larr;Enc_{k}(m)`$)   (&larr; denotes output of randomized value, which can be different when running Enc differet times with same input k and m).
- **Dec** (decryption algorithm): Takes k and c, and outputs m ($`m:=Dec_{k}(c)`$)   (:= denotes assignment of deterministic value).
- For all $m \in M$ and k output by Gen, $Dec_{k}(Enc_{k}(m)) = m$

**The shift cipher**: Given $k \in \{0, 1, ... 25\}$ and m = plaintext, we encript m by shifting every letter of the plain text by k positions (with wrap around). Number of possible keys = 26. Decryption just does the reverse. This way, if we use key c (c=2), "helloworld" becomes "jgnnqyqtnf". This is not a secure encryption since there're only 26 possible keys.

- M = {strings over lowercase English alphabet}
- $Gen$: choose uniform $k \in \{0, ..., 25\}$
- $Enc_{k}(m_{1}...m_{t})$: output $c_{1}...c_{t}$, where $c_{i} := [m_{i} + k\mod 26]$
- $Dec_{k}(c_{1}...c_{t})$: output $m_{1}...m_{t}$, where $m_{i} := [c_{i} - k\mod 26]$

**Sufficient key space principle**: The key space (K) should be large enough to prevent brute-force, exhaustive-search attacks. However, this doesn't guarantee that our encryption scheme is secure.

**Kerckhoffs's principle**: The encryption scheme (algorithm) is not secret. The key is the only secret, which must be chosen at random and kept secret. This way, it's easier to keep/change the secret key than the secret algorithm. Also, allowing the encryption scheme to be public, it's easier to develop standardized encryption schemes (for everyone to use it), to deploy and adopt it, and to receive public scrutiny (thereby increasing our confidence in it).

**The Vigenère cipher**: The key is now a string, not just a character. Encrypt by shifting each character in the plaintext by the amount dictated by the next character of the key (wrap around in the key as needed). Decryption reverses the process. Number of possible keys (assuming keys are 14-character strings) = 26<sup>14</sup> &asymp; 2<sup>66</sup>. The key space is big enough to rule out brute-force attacks. However, this cipher is still not secure: if we assume the key has 14 characters, we realize that every 14th character is encrypted using the same shift, so looking at every 14th character is almost like looking a shift cipher encryption. According to letter frequencies table, the most common english letter is e (12.7%), so let's look for the most common character appearing at every 14th position (&alpha;). Most likely, &alpha; correspond to e, so the first key character is &alpha-e. Now, repeat for all other positions. This attack works with long ciphertexts, though other different attacks are possible. This cipher is perfectly secret if the length of the key is equal to the length of the messages in M.

**Variant Vigenére cipher**: The key is a string of bytes. The plaintext is a string of ASCII characters. Easier to implement. To encrypt, XOR (byte-wise) each character in the plaintext with the next character of the key (wrap around in the key as needed) (message XOR key). Decryption just reverses the process (ciphertext XOR key). Encryption implementation:

```c
#include <stdio.h>
#define KEY_LENGTH 2

main() {  
 unsigned char ch;  
 FILE *message, *ciphert;  
 int i;
 unsigned char key[KEY_LENGTH] = {0x00, 0x00};		// set keys here

 message = fopen("message.txt", "r");			// take message from file
 ciphert = fopen("ciphert.txt", "w");
 i=0;  
 while (fscanf(message, "%c", &ch) != EOF)
  if (ch != '\n') {					// newlines should be encrypted but we avoid it here
   fprintf(ciphert, "%02X", ch ^ key[i % KEY_LENGTH]);	// Apply XOR (^) to each character and save to file
   i++;
  }      
 
 fclose(message);  
 fclose(ciphert);  
 return;
} 
```

**Probability distribution**:

- ***M***: Likelihood of different messages being sent by the parties, given the attacker's prior knowledge. Example: "read me" has prob. 0.7 while "don't read" has 0.3.
- ***K***: Likelihood of different keys being generated by Gen.
- ***C***: Likelihood of getting a certain ciphertext. It depends upon the m and c used ($`c&larr;Enc_{k}(m)`$).

*Pr[K=k] = Pr[Gen outputs key k]*

Assumption: Random variables *M* and *K* are independent. The message that a party sends doesn't depend on the key used to encrypt that message.

Example 1 (Shift cipher):
- For all  $k \in \{0, ..., 25\},  Pr[K=k]  =  1/26$
- Say  $Pr[M='a'] = 0.7,  Pr[M='z'] = 0.3$
- What is $Pr[C='b']$?
  - Two possibilities: either $M='a'$ and $K=1$, or $M='z'$ and $K=2$
  - $Pr[C='b']  =  Pr[M='a']·Pr[K=1] + Pr[M='z']·Pr[K=2]  =  0.7·(1/26) + 0.3·(1/26)  = 1/26$

Example 2 (Shift cipher):
- Say  $Pr[M='cat'] = 0.5$,  $Pr[M='dog'] = 0.5$
- (LTP applied) $Pr[C='ecv']  =  Pr[M='cat']·Pr[C='ecv'|M='cat'] + Pr[M='dog']·Pr[C='ecv'|M='dog']  =  0.5·1/26 + 0.5·0  =  1/52$

**Threat model**: What (real-world) capabilities the attacker is assumed to have. Threat model types:

- __Ciphertext-only attack__: Attacker has a ciphertext. Most basic.
- __Known-plaintext attack__: Attacker has a ciphertext, and a plaintext with its ciphertext. Stronger.
- __Chosen-plaintext attack__: Attacker has a ciphertext, and he can obtain a ciphertext corresponding to a plaintext of the attacker's choice. Even more stronger.
- __Chosen-ciphertext attack__: Attacker has chosen-plaintext capabilities and is able to decrypt certain texts of the attacker's choice. Strongest.

**Security guarantee/goal**: What we want to prevent the attacker from doing.

**Perfect secrecy** (secure encryption) definition (for ciphertext-only attack, one ciphertext):

- __Informal definition__: An encryption scheme is secure if, regardless of any prior information the attacker has about the plaintext, the ciphertext leaks no additional information about the plaintext. In other words, it's secure as long as seeing the ciphertext doesn't make it easier for the attacker to guess a character of the plaintext.

- __Formal definition__: Encryption scheme (Gen, Enc, Dec) with message space M and ciphertext space C is perfectly secret if for every distribution over M, every m &isin; M, and every c &isin; C with $Pr[C=c]>0$, it holds that $Pr[M=m|C=c] = Pr[M=m]$

- Example 1 (Shift cipher):
  - $Pr[M='cat'] = 0.5,  Pr[M='dog'] = 0.5$
  - $Pr[M='dog'|C='ecv'] = 0$
    - $0 \neq Pr[M='dog']$, so shift cipher is not completely secret 

- Example 2 (Shift cipher):
  - $Pr[M='hi'] = 0.3,  Pr[M='no'] = 0.2,  Pr[M='in'] = 0.5$
  - (BT applied) $Pr[M='hi'|C='xy']  =  Pr[C='xy'|M='hi']·Pr[M='hi']/Pr[C='xy']  =  (1/26)·0.3/(1/52)  =  0.6$
    - $0.6 \neq Pr[M='hi']$, so shift cipher is not completely secret 
    - (LTP applied) $Pr[C='xy']  =  0.3·Pr[C='xy'|M='hi'] + 0.2·Pr[C='xy'|M='no'] + 0.5·Pr[C='xy'|M='in']  =  0.3·(1/26) + 0.2·(1/26) + 0.5·0  =  1/52$

**One-time pad cipher** (~1917): This scheme achieves perfect secrecy. The message, key, and ciphertext, have the same number of bits. Used in the red phone DC-Moscow (1980's).
  - M = {0,1}<sup>n</sup>  (set of all binary strings of length n)
  - Gen: choose a uniform key k &isin; {0,1}<sup>n</sup>
  - Enc<sub>k</sub>(m) = k &oplus; m   (bit-wise XOR)
  - Dec<sub>k</sub>(c) = k &oplus; c
  - Correctness:  Dec<sub>k</sub>(Enc<sub>k</sub>(m))  =  k &oplus; (k &oplus; m)  =  (k &oplus; k) &oplus; m  =  m
  - Perfect secrecy (BT applied):  Pr[M=m|C=c]  =  Pr[C=c|M=m]·Pr[M=m]/Pr[C=c]  =  Pr[K=m&oplus;c]·Pr[M=m] / 2<sup>-n</sup>  =  2<sup>-n</sup>·Pr[M=m] / 2<sup>-n</sup>  =  Pr[M=m]
    - (LTP applied) Pr[C=c]  =  &sum;<sub>m'</sub>Pr[C=c|M=m']·Pr[M=m']  =  &sum;<sub>m'</sub>Pr[K=m'&oplus;c]·Pr[M=m']  =  &sum;<sub>m'</sub>2<sup>-n</sup>·Pr[M=m']  =  2<sup>-n</sup>

**Random number generation**: A computer is a deterministic device that cannot generate random values. Nevertheless, we can get random numbers by continually collecting a "pool" of high-entropy (i.e., unpredictable) data taken from external inputs (random events like keystrokes, mouse movements, network access delays...) or hardware random-number generation (Intel chips...). Then, when we need random bits, we process this data to generate an independent, uniform sequence of bits (it may get blocked if there's insufficient entropy available). The OS handles all this. Random bits can be access at /dev/random (Unix), or using crypto libraries.

**One-time pad implementation**: Plaintext (ASCII), key/ciphertext (hex digits written in ASCII):

- __Random key generation__ implementation:

```c
#include <stdio.h>
#define LEN 12

int main() {
 FILE *randfile, *outfile;
 int i;
 unsigned char next;

 randfile = fopen("/dev/dandom", "r");
 outfile = fopen("key.txt", "w");
 if((randfile == NULL) || (outfile == NULL))
 {
  print("File error!\n");
  return 1;
 }

 for(i=0; i<LEN; i++)
 {
  fscanf(randfile, "%c", &next);	// read one byte
  fprint(outfile, "%02x", next);	// write that byte
 }

 fclose(randfile);
 fclose(outfile);

 return 0;
}
```

- __Encryption__ (key XOR message) and __decryption__ (key XOR ciphertex) (commented) implementation:

```c
#include <stdio.h>
#define LEN 12

int main() {
 FILE *keyfile, *pfile, *cfile;
 int i;
 unsigned char ch1, ch2;

 keyfile = fopen("key.text", "r");
 pfile = fopen("ptext.txt", "r");	// for decryption use:  pfile = fopen("ptext2.txt", "w");
 cfile = fopen("ctext.txt", "w");	// for decryption use:  cfile = fopen("ctext.txt", "r");
 if((keyfile == NULL) || (pfile == NULL) || (cfile == NULL))
 {
  print("File error!\n");
  return;
 }
 
 for(i=0; i<len; i++)
 {
  fscanf(keyfile, "%2hhX", &ch1);	// read byte
  fscanf(pfile, "%c", &ch2);		// read byte			// for decryption use:  fscanf(cfile, "%2hhX", &ch2);
  fprintf(cfile, "%02X", ch1^ch2);	// XOR both bytes together	// for decryption use:  fprintf(pfile, "%c", (char)ch1^ch2);
 }

 fclose(keyfile);
 fclose(pfile);
 fclose(cfile);
}
```


## Modern Cryptography

### One-time pad

The schemes achieving perfect secrecy (like One-time pad) have some **inherent limitations** (this is why One-time pad scheme is not used very often nowadays):

- The key is as long as the message.
- Parties must share keys of length equal to the length of all messages they might ever send.
- Only completely secure if each key is used to encrypt a single message.

If the __same key is used twice__ (c<sub>1</sub> = K &oplus; m<sub>1</sub>, c<sub>2</sub> = K &oplus; m<sub>2</sub>), the attacker can make the following computation; c<sub>1</sub> &oplus; c<sub>2</sub> = (k &oplus; m<sub>1</sub>) &oplus; (k &oplus; m<sub>2</sub>) = m<sub>1</sub> &oplus; m<sub>2</sub>, which leaks information about m<sub>1</sub> and m<sub>2</sub>. The result m<sub>1</sub> &oplus; m<sub>2</sub> reveals some information: 

- We can detect where both messages differ: When they're equal, it's 0; when it's 1, they are different.
- Frequency analysis is applicable: Similar to shift and Vigenère cipher, but more difficult.
- Some ASCII characteristics can be exploited: It's easy to identify XOR of a letter and space since all letters begin with 01, space character begins with 00, XOR of 2 letters give 00, and XOR of letter and space gives 01. When an attacker knows that one character is a XOR of a character and a space, he can find out easily the underlying character (if we know A is space and B is character, by computing space &oplus; (A &oplus B) we get character B) (ASCII space = 0x20).

**Optimality of One-time pad:**

Let's demonstrate the following theorem: Given some private-key encryption scheme (like One-time pad), if (Gen, Enc, Dec) with message space M is perfectly secret, then |K| &ge; |M|. So, there're up to |K| possible messages (it's ok if two keys map to the same message). Given any ciphertext, we can try to decrypt it under every possible key in K. 

- Let's assume |K| < |M| (i.e., some messages are not in the list). In this case, we should be able to demonstrate *Pr[M=m|C=c] &ne; Pr[M=m]*.
- Consider *M(c) = {Dec<sub>k</sub>(c)}<sub>k &isin; K</sub>*  (set of all decryptions of a ciphertext c using all the keys)
- |M(c)| &le; |K| < |M|, so there's some m not included in M(c). This means that *Pr[M=m|C=c] = 0 &ne; Pr[M=m]*.
- Conclusion: The encryption scheme, having a key space smaller than the message space, cannot be perfectly secret. So, One-time pad is perfectly secret and optimal.

### Computational secrecy

**Perfect indistinguishability**: Property of a scheme &Pi; where, given 2 messages (m<sub>0</sub>, m<sub>1</sub>) and one ciphertext (c) obtained after encrypting one of them using k, any attacker (A, adversary, eavesdropper) cannot guess correctly which message was used to obtain c with probability any better than 1/2. No attacker can do it better than 1/2. It's perfectly indistinguishable if and only if it's perfectly secret (i.e., this is an alternate definition of perfect secrecy).

- Pr[PrivK<sub>A,&Pi;</sub>=1] = 1/2 + &epsilon;   (the probability that PrivK = 1 (i.e., the probability that A succeeds) is 1/2 for all attackers A on encryption scheme &Pi;)

**Perfect secrecy** requires that no information about the plaintext is leaked, even to eavesdroppers with unlimited computational power. However, it has some drawbacks (seen before) and seems unnecessarily strong.

**Computational secrecy**: It allows some information to be leaked with tiny probability, and only considers "efficient" attackers. It relaxes the idea of perfect indistinguishability. Two approaches:

- **Concrete security**: &Pi; is (t, &epsilon;)-indistinguishable if for all attackers A running in time at most t, it holds that Pr[PrivK<sub>A,&Pi;</sub>=1] &le; 1/2 + &epsilon;

- **Asymptotic security**: Security may fail with probability negligible in n. Attention is restricted to attackers running in time polynomial in n.
  
  - **n** (n &isin; Z<sup>+</sup>): Security parameter (key length, for now). Positive integer. Fixed by honest parties at system initialization (when they choose and share their key). Allows users to tailor the security level. We assume it's known by adversary. Running times (integer) of all parties (honests and attackers), and adversary's (attacker) success probability, are functions of n.

  - **Polynomialy bounded**: For different values of n we have different adversary running times. A function f (that maps n to the attacker's running time) is polynomial if there exists a set of constants ({c<sub>i</sub>}) such that f(n) < &sum;<sub>i</sub>c<sub>i</sub>n<sup>i</sup> for all n.

  - **Negligible**: A function f(n) (that maps n to attacker's success probability) is negligible if for every polynomial p there is an N such that f(n) < 1/p(n) for n>N. Example: f(n) = poly(n)·2<sup>-cn</sup>. This means that f is negligible if it's asymptotically smaller than any inverse polynomial function (i.e., it decays faster than any inverse polynomial).

Examples:

- Low probability: Something that occurs with probability 2<sup>-60</sup>/sec is expected to occur once every 100 billion years.
- Bounded attackers: An attacker with a supercomputer that can test one key per clock cycle could find 2<sup>112</sup> keys since the Big Bang using brute-force search. Modern key spaces usually have 2<sup>128</sup> keys or more.


## Private-Key Encryption
## Message Authentication Codes
## Number Theory
## Key Exchange and Public-Key Encryption
## Digital Signatures

## References

- Jonathan Katz, Yehuda Lindell (2014) *Introduction to modern cryptography, 2nd ed*. Chapman and Hall/CRC. 