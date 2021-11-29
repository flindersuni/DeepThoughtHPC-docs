Unix Connection Guide
=========================

MacOS / MacOSX shares a similar procedure to Unix/BSD Based system. 
Unix/Linux & MacOS systems have native support for the SSH Protocol, 
used to connect to the HPC.

Windows Sub-System For Linux
+++++++++++++++++++++++++++++

The windows Subsystem for Linux (WSL) allows you to run a Linux Distribution 
as a sub-system inside the Windows Operating System. When following these 
instructions, a 'terminal' is the same as starting your WSL Distribution. 

Logging In on Unix 
+++++++++++++++++++
The simplest manner is to open up a terminal windows and SSH into the HPC.

.. figure:: ../_static/shellPasswordPromtImage.png
    :align: center
    :alt: SSH Login Prompt
    
    SSH Login Prompt

1. Your Username is your FAN
2. Your Password is your FAN Password.


These are the same credentials you use to login to OKTA. When successful, you will be logged into the system and presented with a screen 
similar to the image below: 

.. figure:: ../_static/loginOKImage.png
    :align: center
    :alt: Successful Login
    
    Successful Login


You are now connected to the DeepThought HPC and ready to go.

SSH Keys on Unix
------------------

If you wish to setup password-less login via SSH Keys, you may do so.