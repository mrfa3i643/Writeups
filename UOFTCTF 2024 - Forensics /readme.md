<h1>No grep Challenge :</h1>


Use the VM from Hourglass to find the 2nd flag on the system !


Download Link : https://storage.googleapis.com/hourglass-uoftctf/ctf_vm.zip (.ova) 10 GB


After downloading the zip file, I extracted the **ctf_vm.ova** file and extracted the **ctf_vm0disk001.vmdk** (virtual machine disk) using **WinRAR**.


<img src="https://github.com/mrfa3i643/Writeups/blob/main/UOFTCTF%202024%20-%20Forensics%20/img/1.webp">


After that, I used <a href="https://www.autopsy.com/download/"> Autopsy </a> to analyze the image.


<img src="https://github.com/mrfa3i643/Writeups/blob/main/UOFTCTF%202024%20-%20Forensics%20/img/2.webp">


So the first thing I looked at was **Powershell history**.


```/Users/analyst/AppData/Roaming/Microsoft/Windows/PowerShell/PSReadLine/ConsoleHost_history.txt```


Here I found an interesting **PowerShell script (.ps1)**, so let’s take a look at the file contents.


<img src="https://github.com/mrfa3i643/Writeups/blob/main/UOFTCTF%202024%20-%20Forensics%20/img/3.webp">

It’s an **XOR**, so we have the **key*8 and the **cipher text**. Let’s decode it.


<img src="https://github.com/mrfa3i643/Writeups/blob/main/UOFTCTF%202024%20-%20Forensics%20/img/4.webp">


```flag1 : uoftctf{0dd_w4y_t0_run_pw5h}```

