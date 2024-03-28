# Challenge Descriptions

My friend (Fanous) is a hardcore gamer. Although I advised him not to download cracked games, he never listened to my advice, so he downloaded a cracked game, and unfortunately, he disabled his antivirus. Things have been going well for him until he complained about an annoying window that keeps popping when he presses the (SHIFT) key many times on his keyboard while he is playing the game. He met one of his online friends, who said he could help. They met, and Fanous reported that he had a magical USB flash drive that he inserted into his device, and he had done some things to his computer, and the annoying window disappered. A couple hours later, Fanous noticed his computer was acting weirdly. He suspects that his friend did something wrong to his computer.


# Fanous 1


Challenge Description


Welcome to the first challenge of the "Fanous" digital forensics series. Your mission is to answer the following questions:

Q1- What is the volume friendly name associated with USB flash drive?

Q2- Determine the exact time when the USB flash drive was connected to Fanous's computer (HH:MM:SS-DD/MM/YYYY) in UTC

Q3- What is the USB Device ID associated with the flash drive?

Assemble your findings into the flag format.

Flag Format: JUST{A1_A2_A3}

Flag Example: JUST{ExampleName_17:10:23-07/10/2023_ABCD0123456789}


<h3>Solution:</h3>


I used the USB forensics tracker tool that extracts USB device connection artifacts. We should extract the ```C:/Windows/System32/config/SYSTEM``` hive file and open it using the USB tracker tool. 

<img src="https://github.com/mrfa3i643/Writeups/blob/main/JUST.v5/Fanous/img/Registry-MountedDevice.png">

here i found Mounted Device Serial Number (```AA000000000399```)


<img src="https://github.com/mrfa3i643/Writeups/blob/main/JUST.v5/Fanous/img/USBSTOR.png">


so first connection time was ```2024-03-17 19:42:58```


<img src="https://github.com/mrfa3i643/Writeups/blob/main/JUST.v5/Fanous/img/name.png">


Friendly name ```STICK-FIX```

JUST{STICK-FIX_19:42:58-17/03/2024_AA000000000399}


# Fanous 2  


Challenge Description


This is the second challenge of the "Fanous" digital forensics series. Your mission is to answer the following questions:

Q1- Identify the name of the malicious executable that was executed on Fanous's computer.

Q2- Identify the IP address and port number utilized by the attacker during the malicious activity. (IP:PORT)

Q3- Determine the MITRE ATT&CK ID corresponding to the attack observed on Fanous's computer.

Assemble your findings into the flag format.

Flag Format: JUST{A1_A2_A3}


<h3>Solution:</h3>


he downloaded "dControl.exe" that disables windows defender, to install a cracked game


dControl.exe :


<img src="https://github.com/mrfa3i643/Writeups/blob/main/JUST.v5/Fanous/img/dControl.png">


Cracked game :


<img src="https://github.com/mrfa3i643/Writeups/blob/main/JUST.v5/Fanous/img/game.png">


first thing i thought that the cracked game was the malware but i was wrong then i noticed in the description ```he presses the (SHIFT) key many times on his keyboard while he is playing the game``` so the first thing that came to my mind was sticky keys 


sticky keys executable path ```c:\windows\system32\sethc.exe``` 


<img src="https://github.com/mrfa3i643/Writeups/blob/main/JUST.v5/Fanous/img/setch.png">


then gave it to virustotal and found the malware


<img src="https://github.com/mrfa3i643/Writeups/blob/main/JUST.v5/Fanous/img/virustotal.png">


Q1- ```sethc.exe``` 


Q2- Identify the IP address and port number utilized by the attacker during the malicious activity. (IP:PORT)


in Virus Total Behavior i found attacker IP and PORT 


<img src="https://github.com/mrfa3i643/Writeups/blob/main/JUST.v5/Fanous/img/BEHAVIOR.png">


Q2- (IP:PORT) ```3.67.112.102:16466```


Q3- and by understanting the malware and senario we can find  MITRE ATT&CK ID that was ```T1546.008``` https://attack.mitre.org/techniques/T1546/008/


Final flag ```JUST{sethc.exe_3.67.112.102:16466_T1546.008}```

