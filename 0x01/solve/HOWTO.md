# Bài 1
1234 (Dec)<br>
-> 10011010010 (Bin) [kt.gy](https://kt.gy/)<br>
-> 2322 (Oct) [kt.gy](https://kt.gy/)<br>
-> 4d2 (Hex) [kt.gy](https://kt.gy/)<br>
-> YA (B36) [translatorscafe.com](https://www.translatorscafe.com/unit-converter/en-US/numbers/39-13/base-36-base-10/)<br>
-> MG (B58) (tự code theo [wiki](https://en.wikipedia.org/wiki/Base58))<br>
-> BNI= (B64) [kt.gy](https://kt.gy/)<br><br>

# Bài 2
- encode/decode B64<br>
```python
alphabet = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789=~'

def bin_to_dec(b):
    d = 0
    b = b[::-1]
    for i in range(len(b)):
        d += pow(2, i) * (ord(b[i]) - 48)
    return d

def dec_to_bin(d):
    b = ''
    while (d > 0):
        b = chr((d % 2) + 48) + b
        d = d // 2
    for i in range(8 - len(b) % 8):
        b = '0' + b
    return b

def ascii_to_b64(s):
    b64 = ''
    b = ''
    for i in s:
        b += dec_to_bin(ord(i))
    print(b)
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

def b64_to_ascii(s):
    b = ''
    pads = 0
    for i in s:
        if (i == '.'):
            pads += 1
        else:
            b += dec_to_bin(alphabet.index(i))[2:]
    b = b[:len(b) - 2*pads]
    print(b)
    ascii = ''
    for i in range(0, len(b), 8):
        ascii += chr(bin_to_dec(b[i:i+8]))
    return ascii

print(ascii_to_b64('abc'))
print(b64_to_ascii('YWJj'))
```

# Bài 3<br>
Quẳng bừa vào [kt.gy](https://kt.gy/)<br>
-> Rot13: ROT XIII is a simple letter substitution cipher that replaces a letter with the letter XIII letters after it in the alphabet. ROT XIII is an example of the Caesar cipher, developed in ancient Rome. Flag is FLAGSwzgxBJSAMqwxxAU. Insert an underscore immediately after FLAG.<br>
-> Flag: **FLAG_SwzgxBJSAMqwxxAU**<br>

# Bài 4<br>
Phân tích qua bằng code thì đoạn cipher gồm A-Za-z0-9<br>
-> Nghi ngờ là B64 -> Quẳng [kt.gy](https://kt.gy/)<br>
Kết quả lại là 1 cục tương tự thế, nhưng ngắn hơn tẹo<br>
-> Nghi ngờ là encode B64 nhiều lần -> Quẳng [kt.gy](https://kt.gy/) tiếp<br>
... Sau 1 số lần ... Xuất hiện ký tự '=' ở cuối
-> Sure là encode B64 nhiều lần -> Quẳng [kt.gy](https://kt.gy/) tiếp<br>
Sau **vô số** lần thì đoạn B64 co ngắn về còn:<br>
> YmVnaW4gNjY2IDxkYXRhPgo1MURRITFVXSY5NFFHNCMtMzo0JTc5N0k3NCRBVQogCmVuZAo=<br>

Decode tiếp phát cuối được:<br>
> 51DQ!1U]&94QG4#-3:4%797I74$AU (bắt đầu với begin 666)

Google "begin 666" thì được kết quả đó là UUencode -> UUdecode :3<br>
Tool: [decode.urih.com](https://decode.urih.com/data/)<br>
Flag: **FLAG_FeLgP3SiAWezWPHu**<br>
