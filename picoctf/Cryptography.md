# 1. rsa_oracle

> Can you abuse the oracle? <br>
> An attacker was able to intercept communications between a bank and a fintech company. They managed to get the [message](https://artifacts.picoctf.net/c_titan/151/secret.enc) (ciphertext) and the [password](https://artifacts.picoctf.net/c_titan/151/password.enc) that was used to encrypt the message.

## Solution:

- The challenge provided us with secret file containing the flag and a password or ciphertext file
- We couldnt put the ciphertext directly onto the RSA as it would decline to solve it
- Upon searching about it a bit online I found a tool RSHack which can be used to solve such problems
- RSHack had a Chosen Plaintext Attack which was a part of hint 1
- I tried putting my ciphertext into RSHack but I still needed N and e
- In the challenge instance, I gave the value of `1` to be encoded and got m which was the plaintext in hex and c, which was the ciphertext and we know `c = m^e % N` which in python is `pow(m, e, N)
- I found a website having the code to recover the modulus function and it used a list of tuples of known plaintexts and ciphertexts to decode
- The program worked by finding the greatest common divisor of all of them
- The python code still needed the value of e and on searching I found that the most common and secure value of e used is `65537`
- By giving a bunch of inputs to decode to the server like `1,2,3,4,p,i,c,o` and using those m and c values

```py
import gmpy2


def recover_n(pairings, e):
    pt1, ct1 = pairings[0]
    N = ct1 - pow(pt1, e)
   
    # loop through and find common divisors
    for pt,ct in pairings:
        val = gmpy2.mpz(ct - pow(pt, e))
        N = gmpy2.gcd(val, N)
    return N


e = 65537    
pairings = [
    (int("31", 16), 4374671741411819653095065203638363839705760144524191633605358134684143978321095859047126585649272872908765432040943055399247499744070371810470682366100689),
    (int("32", 16), 4707619883686427763240856106433203231481313994680729548861877810439954027216515481620077982254465432294427487895036699854948548980054737181231034760249505),
    (int("33", 16), 1998517197048216725617978890728205902760633363770165103499700157925986170022682604311921651991344892635565706489644418147980643978563559991322776155635395),
    (int("70", 16), 1461426647664698068743640376156472069576551400878225400057062913712955002540353833231221591310248412410392740112271354164199413625355445994523646651837989),
    (int("69", 16), 3069835462055155318378432136248008611151838797644431760883733340350022430175764846557500338023103949640166966331994328181107595981122483691278012885239325),
    (int("63", 16), 3061426502965174255236075437569800176022631320865021697888460291364365699048320842872713108319469773309489427692627911178717134147921190139416935382337046),
    (int("34", 16), 3993239489061277327472930109138093827255646312769901312414509207541733524779884801267968848884701166599834406248783129646083261476137481855550108336137485),
    (int("6f", 16), 4102388542565429766272369447475071490748604547853866619176086761714960913050037982340484722426709442959980763610654558359263034061440324190872663407417406),
    (int("30", 16), 1243958178683320908070161277021530462031994559804812917604345413992816962699847617028301295671668162470014721804001815030262979327683265430847247544407395)
]

print(recover_n(pairings, e))
```

- By running this code, we got the value of N as `5507598452356422225755194020880876452588463543445995226287547479009566151786764261801368190219042978883834809435145954028371516656752643743433517325277971` 
- Now on RSHack we had everything to use incuding N, e and the original c which was our password
- On running the command we got back a ciphertext to be decoded on the server which was `990697120775230856574439803659146329858964453829047603650864484022180711966698660789555176809321985177954300097930385277067316563032607003856781104113231` and it gave us the result of `c8c2607272` and directly putting this into RSHack gave an error
- Again trying it but this time, converting it to decimal and inputting `862254559858` we get the plaintext as `431127279929` or **da099** which is our password
- Now using the second hint which was the openssl command we can get the flag
- Running `openssl enc -aes-256-cbc -d -in secret.enc -pass pass:"da099"` got us the flag

## Flag:

```
picoCTF{su((3ss_(r@ck1ng_r3@_da099d93}
```

## Concepts learnt:

- I learnt how the RSA encryption algorithm worked

## Resources:

- https://cryptohack.gitbook.io/cryptobook/untitled/recovering-the-modulus
- https://github.com/zweisamkeit/RSHack


***


# 2. Custom encryption

> Can you get sense of this code file and write the function that will decode the given encrypted file content.
> Find the encrypted file here [flag_info](https://artifacts.picoctf.net/c_titan/18/enc_flag) and [code file](https://artifacts.picoctf.net/c_titan/18/custom_encryption.py) might be good to analyze and get the flag.


## Solution:

- The custom encrypter was a python file
- It was taking the message along with a test_key of `trudeau`
- The program was taking the ciphertext first and multiplying it by the len of test_key which was 8 and then multiplying that by 311 to get semi_cipher
- It then takes the semi_cipher with the test_key and applies a XOR encrpytion and then reverses everything
- To find the flag we need to reverse the order of the program

```py
def decrypt(cipher_text, key):
    flag = ""
    for i in cipher_text:
        flag += chr(i // 311 // key)
    return flag

def dynamic_xor_decrypt(cipher_text, text_key):
    decoded = ""
    key_length = len(text_key)
    for i, char in enumerate(cipher_text):
        key_char = text_key[i % key_length]
        decrypted_char = chr(ord(char) ^ ord(key_char))
        decoded += decrypted_char
    return decoded

def test(cipher_text, text_key):
    p = 97
    g = 31
    a = 94
    b = 29
    u = generator(g, a, p)
    v = generator(g, b, p)
    key = generator(v, a, p)
    b_key = generator(u, b, p)
    shared_key = None
    if key == b_key:
        shared_key = key
    else:
        print("Invalid key")
        return
    semi_cipher = decrypt(cipher_text, shared_key)
    flag = dynamic_xor_decrypt(semi_cipher, text_key)
    print(f'flag is: {flag[::-1]}')

if __name__ == "__main__":
    message = [260307, 491691, 491691, 2487378, 2516301, 0, 1966764, 1879995, 1995687, 1214766, 0, 2400609, 607383, 144615, 1966764, 0, 636306, 2487378, 28923, 1793226, 694152, 780921, 173538, 173538, 491691, 173538, 751998, 1475073, 925536, 1417227, 751998, 202461, 347076, 491691]
    test(message, "trudeau")
```

## Flag:

```
picoCTF{custom_d2cr0pt6d_751a22dc}
```


***


# 3. miniRSA

> What happens if you have a small exponent? There is a twist though, we padded the plaintext so that (M ** e) is just barely larger than N. Let's decrypt this: [ciphertext](https://mercury.picoctf.net/static/a24cf907007a19dbf30310acad0df9e5/ciphertext)

## Solution:

- The challenge provides us with a RSA challenge having the N, e and C
- I decided to put the values on dcode and try solving it there
- Putting those values on [dcode](https://www.dcode.fr/rsa-cipher) and we can directly get the solution

## Flag:

```
picoCTF{n33d_a_lArg3r_e_ccaa7776}
```

## Concepts learnt:

- RSA encrypting workds as: `C = M^e mod(N)` but when M is small and `M^e < N` then `C = M^e` is not possible 

## Resources:

- https://www.dcode.fr/rsa-cipher

