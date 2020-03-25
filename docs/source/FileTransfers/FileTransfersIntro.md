# Transferring Files to the HPC

Transferring files to the HPC will change depending upon your OS. Thankfully, there are some excellent tools that take this from 'potentially-scary' to 'click a button or two'.

## Before we Get Started

The HPC is a little different that your desktop at home when it comes to storage (not just computing power!). It's a shared resource, so we cant store everybody's data for all time - there just isn't enough space!

So, we have two main storage locations we use; Linux Guru's some of this is old hat - please keep reading, it'll get to new things soon!

- /home/$FAN
- /scratch/$FAN

### /Home

Your 'home' directories. This is a small amount of storage to store your small bits and pieces. This is the analogous to the Windows 'Documents' folder.

At a command promp, your home directory usually gets shortened to ~/ - we will cover this more in the Linux Guide.

#### What to Store in /home

Here is a rough guide as to what should live in your /home/$FAN directory. In general, you want small, little things is here.

- SLURM Scripts
- Results from Jobs.
- 'Small' Data-Sets (<1GB)

### /Scratch

Scratch is your working space. Whenever you are running a job, it should be running in the the /scratch area. This storage area is quicker and isolated from the others - meaning that even under high usage you are not going to slow down much (if at all) waiting to read data to or from the disks.

It's also much, much larger than your /home area. Some of the working data-sets we have seen on Deep Thought have gotten out to Multiple Terabytes! Thankfully, /scratch can handle this, however /home would not.

#### What to Store in /scratch

Here is a rough guide as to what should live in your /scratch/$FAN directory. In general, anything large, bulky and only needed for a little while should go here.

- Job Working Data-sets
- Intermediate files

## Transferring Files

All file-transfers are done via Secure File Transfer Protocol (SFTP). As was the same with the 'Getting Access', pick your platform:

### MacOS

[Link](Mac/MacFileTransfer.md) to MacOS page

### Unix/Linux

[Link](Linux/LinuxFileTransfer.md) to unix page

### Windows

[Link](Windows/WindowsFileTransfer.md) to Windows page
