# P13 [500 pts]


**Category:** Forensics


**Solves:** 1

Description


We captured this traffic from P13s computer so can you help him?(Note: some Osint required)


Q1 - we need help locating the hiding place of Cu713s script once u find it we need the full url ?


Q2 - Once you have retrieved the file, use it to find the location of the city where Cu713s friends went. What is the city name?flag format CATF{Q1_Q2}\


Author : MM0X


Firstly i found an encrypted php ( its an image inside a php file ) file in HTTP then i exported the file:


<img src="https://github.com/mrfa3i643/Writeups/blob/main/CATF%2023%20%3A%20P13%20(Digital%20Forensics)/img/1.webp">


<img src="https://github.com/mrfa3i643/Writeups/blob/main/CATF%2023%20%3A%20P13%20(Digital%20Forensics)/img/2.webp">


The challenge wants me to find the script that used to encrypt the image


<img src="https://github.com/mrfa3i643/Writeups/blob/main/CATF%2023%20%3A%20P13%20(Digital%20Forensics)/img/3.webp">


I filtered “data” in pcap file and i found this :


<img src="https://github.com/mrfa3i643/Writeups/blob/main/CATF%2023%20%3A%20P13%20(Digital%20Forensics)/img/4.webp">


I found this suspicious name so i did osint on this name


<img src="https://github.com/mrfa3i643/Writeups/blob/main/CATF%2023%20%3A%20P13%20(Digital%20Forensics)/img/5.webp">


Using sherlock tool i was able to find this github repo


<a href="https://github.com/Cu713?tab=overview&from=2023-05-01&to=2023-05-31&source=post_page-----7697a0f6edb7--------------------------------">Cu713 github </a>


<img src="https://github.com/mrfa3i643/Writeups/blob/main/CATF%2023%20%3A%20P13%20(Digital%20Forensics)/img/6.webp">


I found a 3 commites :


<h3>Q1 Answer:</h3>


<a href="https://github.com/Cu713/Secr3t/commit/d3c2ff53863d0fcc6f55c79d0d6799d40ca92820?source=post_page-----7697a0f6edb7--------------------------------">Cu713/Secr3t@d3c2ff5</a>


Encryption script :


<img src="https://github.com/mrfa3i643/Writeups/blob/main/CATF%2023%20%3A%20P13%20(Digital%20Forensics)/img/7.webp">


I reversed this code


```py
def unswap(bytearray_):
    if len(bytearray_) < 2:
        return bytearray_

    result = []
    for i in range(0, len(bytearray_) - 1, 2):
        result.extend([bytearray_[i+1], bytearray_[i]])
    if len(bytearray_) % 2 == 1:
        result.append(bytearray_[-1])
    return bytearray(result)
def dec(file):
    key = [255, 216, 255 ,224] #{FF D8 FF E0] 00 10 4A 46 49 46 00 01 ,key=file[:4] , .jpeg
    print("key =",key,sep="")
    decrypted = bytearray()
    for i in range(4, len(file)):
        decrypted.append(file[i] ^ key[(i-4) % len(key)])
    return decrypted
with open("panel.php", 'rb') as f:
    file_content = f.read()
unswapped_encrypted = unswap(file_content)
decrypted = dec(unswapped_encrypted)
with open("dec", 'wb') as f:
    f.write(decrypted)
```


<h2>NOTE : Don’t forget to Delete the “headers” and “data” from php file.</h2>


After that i run this script :


<img src="https://github.com/mrfa3i643/Writeups/blob/main/CATF%2023%20%3A%20P13%20(Digital%20Forensics)/img/8.webp">


<img src="https://github.com/mrfa3i643/Writeups/blob/main/CATF%2023%20%3A%20P13%20(Digital%20Forensics)/img/9.webp">


<img src="https://github.com/mrfa3i643/Writeups/blob/main/CATF%2023%20%3A%20P13%20(Digital%20Forensics)/img/10.webp">


The decrypted file its corrupted, so i edited the file by insert 8 bytes in the first line and delete the last 4 bytes to make it a valid “jpeg” file




<img src="https://github.com/mrfa3i643/Writeups/blob/main/CATF%2023%20%3A%20P13%20(Digital%20Forensics)/img/11.webp">


<img src="https://github.com/mrfa3i643/Writeups/blob/main/CATF%2023%20%3A%20P13%20(Digital%20Forensics)/img/12.webp">


then i got the valid image:


<img src="https://github.com/mrfa3i643/Writeups/blob/main/CATF%2023%20%3A%20P13%20(Digital%20Forensics)/img/13.webp">


I used google lens and i found this place in “Dublin”


<h2>Q2 Answer : Dublin</h2>


```The flag : CATF{https://github.com/Cu713/Secr3t/commit/d3c2ff53863d0fcc6f55c79d0d6799d40ca92820_Dublin}```


<img src="https://github.com/mrfa3i643/Writeups/blob/main/CATF%2023%20%3A%20P13%20(Digital%20Forensics)/img/14.webp">
