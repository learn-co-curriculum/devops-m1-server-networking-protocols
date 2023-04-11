# Server Networking

## Learning goals

- Understand basic server networking and the protocols used
- Learn to use SSH to remotely connect to a computer and run shell commands
- Understand how to transfer files between different servers and computers using FTP
- Learn the basic details regarding the email protocols SMTP, POP, and IMAP

## Introduction

In this lesson, we will be going over more internet protocols, focusing on protocols commonly used by server computers. Learning how these protocols work (and how to use them) is essential, as they cover use-cases such as file transfers and running remote commands.

## SSH

**SSH** (Secure Shell) is a network protocol that allows you to remotely connect to a computer and run shell commands on it as if you were using it directly (as we have been thus far). 

To use SSH there are only two requirements: an SSH *client* on the computer you want to *use*, and an SSH *server* on the computer you want to remote *into*. Most Linux distributions, Ubuntu included, already ship with an SSH server, so we don't have to worry about doing that setup on our virtual machines.

Likewise, most operating systems already ship with an SSH client as well, seeing as it is very commonly used. Usage is extremely simple:

Open your terminal of choice on your *host* computer (**Terminal** on MacOS, **Powershell** or **Command Prompt** on Windows, or whatever terminal you wish to use). This terminal is similar to the shell we have open on our virtual machines.

Now we're ready to run the `ssh` command, which looks like the following:

```bash
$ ssh <username>@<remote_host>
```

Replace *username* with your username on the remote computer (our virtual machine), and *remote_host* with the IP address of the same computer. The *username* portion can actually be omitted a lot of the time.

Try connecting to your own virtual machine! First find its IP address (under `inet` when using the `ifconfig` command), and then in your *host* computer, run the command above.

## FTP

**FTP** (File Transfer Protocol) is another popular network protocol like SSH that allows you to transfer files between different servers and computers. It's a method widely used for sharing files across the internet, especially when it comes to managing a server.

Just like with SSH, we need both an FTP *server* and *client*. Most Linux distributions also ship with an FTP server out of the box, so we don't have to do any setup in our virtual machine. As far as the client goes, there's no real standard, so we'll be using *FileZilla*, a free and open-source client that works on most operating systems.

To download it, go to the [FileZilla website](https://filezilla-project.org/) and follow the installation instructions.

Once you've installed FileZilla, we're ready to connect to a server! Open FileZilla up, and go to `File -> Site Manager...` to open the site manager. Click `New site` at the bottom, and call it whatever you want (e.g. `VM`). Fill the boxes as follows:

- **Port:** There are usually two ports to keep in mind when using FTP; 21 and 22. 21 is used by the standard FTP protocol, whereas 22 is used by the SFTP protocol (Secure FTP). Use port 22 (SFTP) for now!
- **Host:** Set this to your virtual machine's local IP, prepended by the protocol like with http/https. In this case, we are going to be using SFTP, so the host will look something like: `sftp://192.168.15.10`
- **User/Password:** Set to the name of the user on the machine you are connecting to (VM) that you want to transfer files as; keep in mind you will be limited to the folders that user has read/write access to.

All-in-all, it should look something like the following:

![FileZilla setup](https://curriculum-content.s3.amazonaws.com/6685/devops-m1-server-networking/filezilla-setup.png)

Once done, hit `OK` to save the changes. You will be prompted whether you want to save passwords, accept it again. Now go back to the site manager and click `Connect`!

A prompt will show up asking to verify the fingerprint; this is to make sure that you're connecting to the right server. Check the box to save it, and then accept the prompt.

You should be properly connected to the virtual machine with FTP now! Once you're connected to a server, you can start transferring files. Simply navigate to the local file on the left-hand pane, or in your operating system's file browser (`explorer`, `finder`, etc.) and drag a file into the right-hand pane.

By default, you will be in the `/home/<user>` directory. Make a `pictures` folder and throw a picture from your host PC into the VM to make sure everything is working properly!

## SMTP/POP/IMAP

The last server protocols we'll be looking at are *SMTP*, *POP*, and *IMAP*. These three are popular text-based protocols used for email communication. **SMTP (Simple Mail Transfer Protocol)** is used for for *sending* emails and lives on TCP port 25; sender composes an email and sends it to an SMTP server, which verifies the sender's identity and establishes a connection with the recipient mail server. Both **POP (Post Office Protocol)** and **IMAP (Internet Message Access Protocol)** are used for *receiving* emails and live on TCP port 110 and 143 respectively; client connects to either protocol server, which then downloads email messages for that client.

![SMTP/POP/IMAP illustration](https://curriculum-content.s3.amazonaws.com/6685/devops-m1-server-networking/protocols.png)

## Conclusion

Understanding how these protocols work is crucial for not only managing and operating Linux machines, but also for *understanding* how functionalities we take for granted actually operate under-the-hood. Don't worry if these seem a bit overwhelming; once you use them in practice it'll be a lot easier to remember. Just make sure you understand what each protocol is used for, and *how* to use FTP and SSH.