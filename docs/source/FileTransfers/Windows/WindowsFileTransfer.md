# Windows File Transfers

Windows doesn't support the SFTP protocol in a native way. Thankfully, there are lots of clients written to do just this for us.

## Sub-System for Linux

You can use the WSL for this - head on over to the [Linux](../Linux/LinuxFileTransfer.md) Guide.

## Potential Client List

This is not an exhaustive list - feel free to use whatever you wish that supports the SFTP protocol.

- [WinSCP](https://winscp.net/eng/index.php)
- [FileZilla](https://filezilla-project.org/?AFFILIATE=6732&__c=1)

This guide will focus on WinSCP.

## Getting Connected

Open WinSCP, enter deepthought.flinders.edu.au as the host to connect to, and click Login. You should have a screen that looks like this.

![](../../_static/WinSCPImage.png)

The first time you connect up you will get a warning - this is fine, just click YES to continue on.

![](../../_static/WinSCPSSHKeyNotice.png)

A connection to Deep Thought will then be created - login using your FAN and password. If all goes well, you will be treated to this screen:

![](../../_static/WinSCPConnected.png)
