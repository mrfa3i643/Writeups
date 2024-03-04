<h1>No grep Challenge :</h1>


Use the VM from Hourglass to find the 2nd flag on the system !


Download Link : https://storage.googleapis.com/hourglass-uoftctf/ctf_vm.zip (.ova) 10 GB


After downloading the zip file, I extracted the **ctf_vm.ova** file and extracted the **ctf_vm0disk001.vmdk** (virtual machine disk) using **WinRAR**.


<img src="https://github.com/mrfa3i643/Writeups/blob/main/UOFTCTF%202024%20-%20Forensics%20/img/1.webp">


After that, I used <a href="https://www.autopsy.com/download/"> Autopsy </a> to analyze the image.


<img src="https://github.com/mrfa3i643/Writeups/blob/main/UOFTCTF%202024%20-%20Forensics%20/img/2.webp">


So the first thing I looked at was **Powershell history**.


**Powershell history** Path :


```/Users/analyst/AppData/Roaming/Microsoft/Windows/PowerShell/PSReadLine/ConsoleHost_history.txt```


<img src="https://github.com/mrfa3i643/Writeups/blob/main/UOFTCTF%202024%20-%20Forensics%20/img/3.webp">


Here I found an interesting **PowerShell script (.ps1)**, so let’s take a look at the file contents.


<img src="https://github.com/mrfa3i643/Writeups/blob/main/UOFTCTF%202024%20-%20Forensics%20/img/4.webp">


It’s an **XOR**, so we have the **key** and the **cipher text**. Let’s decode it.


<img src="https://github.com/mrfa3i643/Writeups/blob/main/UOFTCTF%202024%20-%20Forensics%20/img/5.webp">


```uoftctf{0dd_w4y_t0_run_pw5h}```
<h1>Hourglass Challenge :</h1>


```No EDR agent once again, we imaged this workstation for you to find the evil !In this challenge, I used a simple way, and it’s useful to understand what the newest files are that were created or renamed by the users or attackers.```


I recommend reading this article about the <a href="https://www.orionforensics.com/forensics-tools/ntfs-journal-viewer-jv/"> **NTFS $UsnJrnl** </a> file.


NTFS **$UsnJrnl** Path :


**$Extend\$USNJrnl**


**$J** (where the most important data reside) and **$Max**.


**$USNJrnl:** provides high-level monitoring of file and folder changes, such as creation, deletion, and renaming.


<img src="https://github.com/mrfa3i643/Writeups/blob/main/UOFTCTF%202024%20-%20Forensics%20/img/6.webp">


extract the **$USNJrnl$J** file and use the <a href="https://ericzimmerman.github.io/#!index.md"> MFTCmd Eric Zimmerman tool> </a> to parse the file.


<img src="https://github.com/mrfa3i643/Writeups/blob/main/UOFTCTF%202024%20-%20Forensics%20/img/7.webp">


then open the CSV file via the <a href="https://ericzimmerman.github.io/#!index.md"> Timeline Explorer Zimmerman tool </a>.


<img src="https://github.com/mrfa3i643/Writeups/blob/main/UOFTCTF%202024%20-%20Forensics%20/img/8.webp">


Here we can see a new text file was created, **“New Text Document.txt.”** I used the **RenameOldname** to filter the **Update Reasons column** to find the old name of the text file before renaming it to the new name.


So let’s see what the new name of the file is. Now I will use the **entry number** value as a filter, so let’s see what the “New **Text Document.txt”** file with the **entry number (111631)** was renamed to:


<img src="https://github.com/mrfa3i643/Writeups/blob/main/UOFTCTF%202024%20-%20Forensics%20/img/9.webp">


**flag.txt** Path :


```/Users/analyst/Desktop/flag.txt.txt```


It was renamed **flag.txt**, and it contains a fake flag.


<img src="https://github.com/mrfa3i643/Writeups/blob/main/UOFTCTF%202024%20-%20Forensics%20/img/10.webp">


So let’s see the other one with **entry number 36441**, which was renamed to:


<img src="https://github.com/mrfa3i643/Writeups/blob/main/UOFTCTF%202024%20-%20Forensics%20/img/11.webp">


**settings.txt** file Path :


```/Windows/DiagTrack/Settings/settings.txt```


<img src="https://github.com/mrfa3i643/Writeups/blob/main/UOFTCTF%202024%20-%20Forensics%20/img/12.webp">


I found this base64 in the file contents, and after decoding it, I got the flag:


```sh
echo "Ky0tCiB1b2Z0Y3Rme1Q0c0tfU2NoM0R1bDNyX0ZVTn0KKy0t" | base64 -d
+--
 uoftctf{T4sK_Sch3Dul3r_FUN}
+--
```
