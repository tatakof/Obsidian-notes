https://phoenixnap.com/kb/ssh-to-connect-to-remote-server-linux-or-windows

There are many ways to establish a connection with a remote machine depending on the operating system you are running, but the two most used protocols are:

-   Secure Shell (SSH) for Linux-based machines
-   Remote Desktop Protocol (RDP) for Windows-based machines


The two protocols use the client and server applications to establish a remote connection. These tools allow you to gain access and remotely manage other computers, transfer files, and do virtually anything you can do while physically sitting in front of the machine.

**Prerequisites**

Before you can **establish a secure remote desktop protocol** with a remote machine, there are a few basic requirements to meet:

-   The remote computer must be turned on at all times and have a network connection.
-   The client and server applications need to be installed and enabled.
-   You need the IP address or the name of the remote machine you want to connect to. LA IP CAMBIA CONSTANTEMENTE?
-   You need to have the necessary permissions to access the remote computer.
-   Firewall settings need to allow the remote connection.


### What is SSH
Secure Shell, sometimes referred to as **Secure Socket Shell**, is a protocol which allows you to [connect securely to a remote computer](https://phoenixnap.com/blog/secure-remote-access-best-practices) or a server by using a text-based interface.

When a secure [SSH connection](https://phoenixnap.com/kb/how-does-ssh-work) is established, a shell session will be started, and you will be able to manipulate the server by typing commands within the client on your local computer.

System and network administrators use this protocol the most, as well as anyone who needs to manage a computer remotely in a highly secure manner.

### How does SSH work?
In order to establish an SSH connection, you need two components: a client and the corresponding server-side component. An SSH client is an application you install on the computer which you will use to connect to another computer or a server. The client uses the provided remote host information to initiate the connection and if the credentials are verified, establishes the encrypted connection.

On the server’s side, there is a component called an SSH daemon that is constantly listening to a specific TCP/IP port for possible client connection requests. Once a client initiates a connection, the SSH daemon will respond with the software and the protocol versions it supports and the two will exchange their identification data. If the provided credentials are correct, SSH creates a new session for the appropriate environment.

The default SSH protocol version for SSH server and SSH client communication is version 2.

## How to Enable an SSH Connection

Since creating an SSH connection requires both a client and a server component, you need to make sure they are installed on the local and the remote machine, respectively. An open source SSH tool—widely used for Linux distributions— is OpenSSH. Installing OpenSSH is relatively easy. It requires access to the terminal on the server and the computer that you use for connecting. Note that Ubuntu does not have SSH server installed by default.

## How to Install an OpenSSH Client

Before you proceed with installing an SSH client, make sure it is not already installed. Many Linux distributions already have an SSH client.

To check if the client is available on your Linux-based system, you will need to:

1.  Load an SSH terminal. You can either search for “terminal” or press **CTRL** + **ALT** + **T** on your keyboard.
2.  Type in **`ssh`** and press **Enter** in the terminal.
3.  If the client is installed, you will receive a response that looks like this:

```
username@host:~$ ssh

usage: ssh [-1246AaCfGgKkMNnqsTtVvXxYy] [-b bind_address] [-c cipher_spec]
[-D [bind_address:]port] [-E log_file] [-e escape_char]
[-F configfile] [-I pkcs11] [-i identity_file]
[-J [user@]host[:port]] [-L address] [-l login_name] [-m mac_spec] [-O ctl_cmd] [-o option] [-p port] [-Q query_option] [-R address] [-S ctl_path] [-W host:port] [-w local_tun[:remote_tun]]
[user@]hostname [command]

username@host:~$
```

This means that you are ready to remotely connect to a physical or virtual machine. Otherwise, you will have to install the OpenSSH client:

1.  Run the following command to install the OpenSSH client on your computer:  
    `sudo apt-get install openssh-client`
2.  Type in your superuser password when asked.
3.  Hit Enter to complete the installation.
