# Linux/Unix File Transfers

Linux / Unix based system shave native support for the SFTP Protocol, and can also use the Secure Copy Protocol - which can sometimes be quicker. 

## The Windows Sub-System for Linux

The windows Subsystem for Linux (WSL) allows you to run a Linux Distribution as a sub-system in windows. When following these instructions, a 'terminal' is the same as starting your WSL Distribution.

## Transferring Files to the HPC

To upload documents to Deep Thought, the simplest method is to open a Terminal window.


### The Quick Version

Subsitute your filename, FAN and Password, type scp FILENAME FAN@deepthought.flinders.edu.au:/home/FAN then hit enter.
Enter your password when prompted. This will put the file in your home directory on Deep Thought. It looks (when substitured accordingly) similar to:

![Alt SCP Example Command](../../_static/SCPExampleImage.png)

### The Longer Version

To transfer files off Deep Thought, you simply need to invert that command to point to either: 

- A name of a Computer that Deepthough 'knows' about.
- An IP Address that Deepthought can reach.

#### Transfers By Computer Name

If you know the hostname of the computer, you can substitute this to transfer files back to your machine. The command stays the same, mostly. You still follow the same idea, we just change where we are pointing it. This one assumed you are transferring it to a Linux/Unix based machine. 

The command will take this form:

![Alt SCP Transfer By Hostname](../../_static/SCPByHostname.png)

#### Transfer By IP Address

If you don't know your compuer IP, then the commands of:

- ip addr
- ifconfig

Will be your friend to figure out what it is. Just like above, we slightly change the command, and sub-in an IP instead of a host-name.

![Alt SCP Transfer By IP](../../_static/SCPByIp.png)
