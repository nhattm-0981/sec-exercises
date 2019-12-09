# Bài 1
1234 (Dec)<br>
-> 10011010010 (Bin) [kt.gy](https://kt.gy/)<br>
-> 2322 (Oct) [kt.gy](https://kt.gy/)<br>
-> 4d2 (Hex) [kt.gy](https://kt.gy/)<br>
-> YA (B36) [translatorscafe.com](https://www.translatorscafe.com/unit-converter/en-US/numbers/39-13/base-36-base-10/)<br>
-> MG (B58) (tự code theo [wiki](https://en.wikipedia.org/wiki/Base58))<br>
-> BNI= (B64) [kt.gy](https://kt.gy/)<br><br>

# Bài 2
* encode B64<br>
```python
alphabet = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789=~'

def bin_to_dec(b):
    d = 0
    b = b[::-1]
    for i in range(6):
        d += pow(2, i) * (ord(b[i]) - 48)
    return d

def ascii_to_bin(s):
    b = ''
    for i in s:
        a = ord(i)
        while (a > 0):
            b = chr((a % 2) + 48) + b
            a = a // 2
    for i in range(8 - len(b) % 8):
        b = '0' + b
    return b

def ascii_to_b64(s):
    b64 = ''
    b = ''
    for i in s:
        b += ascii_to_bin(i)
    for i in range(0, len(b), 6):
        block = ''
        pad = ''
        if (len(b) - i < 6):
            print(len(b) - i)
            block = b[i:len(b)]
            for j in range(6 - (len(b) - i)):
                block += '0'
            for j in range((len(b) - i)):
                pad += '.'
        else:
            block = b[i:i+6]
        b64 += (alphabet[bin_to_dec(block)] + pad)
    return b64

print(ascii_to_b64('abc'))
```
