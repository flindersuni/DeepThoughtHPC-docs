Windows Connection Guide 
========================
To connect to Deep Thought a SSH client such as PuTTy is required. 
Below is a short list of the possible programs you can use as a client to connect to the HPC. 
This guide will focus on Putty - but will be equally applicable to the other programs.


Windows SSH Client Options
----------------------------

.. _Putty: https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html
.. _KiTTY: http://www.9bis.net/kitty/#!pages/download.md
.. _BitVise Client: https://www.bitvise.com/download-area
.. _MobaXTerm: https://mobaxterm.mobatek.net/


Windows SSH Connection Guide
--------------------------------
Open PuTTy, and you are presented with this screen:

.. figure:: ../_static/puttyAccessImage.png
    :align: center
    :alt: PuTTY Connection Detail Screen 

    PuTTY Connection Detail Screen 


1. Fill in the hostname to be: deepthought.flinders.edu.au,
2. Change the Connection Type to SSH
3. Set the Port Number to 22
4. Click Open


Logging In on Windows
++++++++++++++++++++++
If all has gone well, you will be presented with a login prompt similar to the following image.

.. figure:: ../_static/puttyLoginImage.png
    :align: center
    :alt: PuTTY Login Prompt
    
    PuTTY Login Prompt


1. Your Username is your FAN
2. Your Password is your FAN Password.
 
These are the same credentials you use to login to OKTA.

When successful, you will be logged into the system and presented with a screen 
similar to the image below: 

.. figure:: ../_static/loginOKImage.png
    :align: center
    :alt: Successful Login
    
    Successful Login


You are now connected to the DeepThought HPC and ready to go.

SSH Keys on Windows 
*********************
As with the Unix/Linux/MacOS system, you may also setup SSH Keys for password-less logins. 
Be sure to follow the specific instructions for your client, as they will differ.