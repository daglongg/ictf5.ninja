### Vault

Download the file and use the tool `Exeinfo PE` to check the information.
![image](https://github.com/daglongg/ictf5.ninja/assets/138242812/51b02671-ffb5-464f-a8cf-97f3971f2bd0)

Use IDA to debug. I see the program asks `Enter the secret code: `. And I entered the program compared with the flag. If the correct program displays `Access Granted!`. And I see the flag move into the rsi register. Check register RSI.

![image](https://github.com/daglongg/ictf5.ninja/assets/138242812/a04b50ae-ce7e-4a01-b417-6fed1b0127ca)

And i have flag: `ictf{welc0me_t0_rev3rs1ng}`

### Vault2

Download the file and use the tool `Exeinfo PE` to check the information.

![image](https://github.com/daglongg/ictf5.ninja/assets/138242812/b8cb7821-4827-47ef-9cb4-40260d7712af)

Here we see that what we enter will be copied into the dest variable through the `strncpy` funtion. And they will be transformed through the `mysteryFunction` function and then compared with variable `s2`.

![image](https://github.com/daglongg/ictf5.ninja/assets/138242812/e592aec4-02cc-45d7-b8f0-0c74b78bfbaf)

I wrote a script using py to decode

```
string = "hawb~w6q5dcn0[n2{\\|5s\x7F"
result = ""

for i in range(len(string)):
    char = string[i]
    if char == "\x00":  # Kiểm tra ký tự kết thúc chuỗi
        break
    result += chr(ord(char) ^ ((i % 5) + 1))

print("Kết quả sau khi XOR:", result)
```
And i have flag : `ictf{v4r1abl3_k3y_x0r}`

### Vault3

Download the file and use the tool `Exeinfo PE` to check the information.

![image](https://github.com/daglongg/ictf5.ninja/assets/138242812/fe60aed6-03e9-457e-b714-2d7ad85ef69f)

Here we can see that what we enter will be entered into the `checkFlag` function.

![image](https://github.com/daglongg/ictf5.ninja/assets/138242812/28943a19-9e12-49dd-874e-1e7d95ca036b)

Here we see that what we enter will be saved in the variable `dest` and that variable dest will be `encrypted` and then compared with function `s2`.

![image](https://github.com/daglongg/ictf5.ninja/assets/138242812/edc04be8-4808-4f7e-b517-db652ce94667)

Going into the encrypt function, we see that our input has been xor and rotated. So we need to rotate and then xor again. 

![image](https://github.com/daglongg/ictf5.ninja/assets/138242812/00dd9ef1-943f-4e35-8a0b-a14852be380b)

I have written a script to execute
 ```
def encrypt(data):
    result = []
    for i in range(len(data)):
        char = rotate_char(ord(data[i]), 3) ^ (i % 4)
        result.append(char)
    return result

def rotate_char(a1, a2):
    if 96 < a1 <= 122:
        return (a1 - 97 - a2) % 26 + 97
    if ( a1 <= 64 or a1 > 90 ):hace
        return a1
    return ((a1 - 65 - a2) % 26 + 65)

data = "leyh{V2z4x#3q^x\"wl][0V\x7F"
encrypted_data = encrypt(data)
# print(encrypted_data)
print("".join(chr(item) for item in encrypted_data))
```
And i have flag: `ictf{R0t4t!0n_w!th_X0R}`








 




