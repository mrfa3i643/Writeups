Hack The Box(Forensics Challenge)

CHALLENGE DESCRIPTION: Our cybercrime unit has been investigating a well-known APT group for several months. The group has been responsible for several high-profile attacks on corporate organizations. However, what is interesting about that case, is that they have developed a custom command & control server of their own. Fortunately, our unit was able to raid the home of the leader of the APT group and take a memory capture of his computer while it was still powered on. Analyze the capture to try to find the source code of the server.

<h1>Solution:</h1> 


**Step 1**: I wanted to know what is the profile name provided within this memory:

**Step 2**:I searched all of the mem files and I found this (backup_development.zip) it seems like an interesting file:


<img src="https://github.com/mrfa3i643/Writeups/blob/main/HTB%3A%20TrueSecrets/img/1.webp">


**Step 3**: So by using (the dumpfiles) plugin I dumped this file and I wanted to see what is in the zip file :


<img src="https://github.com/mrfa3i643/Writeups/blob/main/HTB%3A%20TrueSecrets/img/2.webp">


**Step 4**:After I extracted it, I found a (.tc) file “TrueCrypt”;


I used VeraCrypt (https://veracrypt.eu/en/Downloads.html) to mount the file but it has a password, I found The password by using the “truecryptpassphrase” plugin like that:


<img src="https://github.com/mrfa3i643/Writeups/blob/main/HTB%3A%20TrueSecrets/img/3.webp">


<img src="https://github.com/mrfa3i643/Writeups/blob/main/HTB%3A%20TrueSecrets/img/4.webp">


**Step 5**: I opened the file By VeraCrypt and mount it with a password


<img src="https://github.com/mrfa3i643/Writeups/blob/main/HTB%3A%20TrueSecrets/img/5.webp">


<img src="https://github.com/mrfa3i643/Writeups/blob/main/HTB%3A%20TrueSecrets/img/6.webp">


Inside the disk, I found the folder **“malware_agent”** which contains four files:



1-C# Encryption Script.


2-Three files are Encrypted by the given script(DES).


<img src="https://github.com/mrfa3i643/Writeups/blob/main/HTB%3A%20TrueSecrets/img/7.webp">


Step 6: Inside the C# script I found “iv+key” I used it to decrypt the files



<img src="https://github.com/mrfa3i643/Writeups/blob/main/HTB%3A%20TrueSecrets/img/8.webp">


I used this online tool (DES): https://devtoolcafe.com/tools/des


**Note: Decode the files line by line.**


I tried to decrypt all the files


File1:


<img src="https://github.com/mrfa3i643/Writeups/blob/main/HTB%3A%20TrueSecrets/img/9.webp">


File2:


<img src="https://github.com/mrfa3i643/Writeups/blob/main/HTB%3A%20TrueSecrets/img/10.webp">


File3:


<img src="https://github.com/mrfa3i643/Writeups/blob/main/HTB%3A%20TrueSecrets/img/11.webp">


And found the flag in the third file:

<img src="https://github.com/mrfa3i643/Writeups/blob/main/HTB%3A%20TrueSecrets/img/12.webp">
