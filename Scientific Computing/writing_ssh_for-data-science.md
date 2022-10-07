### How to SSH into a remote computer for data science (linux) 

Here we'll see how to ssh into a remote computer (Secure SHell, a protocol for remote connections), something you might have to do if you have heavy workloads. The objective will be to be able to open your IDE (be it VSCode or Rstudio for example) remotely, so that you can see the graphic interface as if you were running your IDE on your computer but with the compute power coming from the remote one (no more Anydesk or Teamviewer!). 

For that, we first have to set up SSH in both computers, yours and the remote one. 


##### Requirements
-   The remote computer must be turned on at all times and have a network connection.
-   The client and server applications need to be installed and enabled.
-   You need the IP address or the name of the remote machine you want to connect to. 
-   You need to have the necessary permissions to access the remote computer.
-   Firewall settings need to allow the remote connection.
- Both computers must have the OpenSSH client


#### How to set up SSH for your computer



Before you proceed with installing an SSH client, make sure it is not already installed. Many Linux distributions already have an SSH client.

To check if the client is available on your Linux-based system, you will need to:

1.  Load an SSH terminal. You can either search for “terminal” or press **CTRL** + **ALT** + **T** on your keyboard.
2.  Type in **`ssh`** and press **Enter** in the terminal.
3.  If the client is installed, you will receive a response that looks like this:

![[Pasted image 20221006145645.png]]
This means that you are ready to remotely connect to a physical or virtual machine. Otherwise, you will have to install the OpenSSH client:

1.  Run the following command to install the OpenSSH client on your computer:  
    `sudo apt-get install openssh-client`
2.  Type in your superuser password when asked.
3.  Hit Enter to complete the installation.

Make sure you installed it in your personal computer, and not on the remote one!

You are now able to SSH into any machine with the server-side application on it, provided that you have the necessary privileges to gain access, as well as the hostname or IP address.

#### How to set up SSH for your remote computer
Your remote compute will have to have the server-side of the SSH software, this is the OpenSSH server. 

In your remote computer, check if OpenSSH server is installed by running in your terminal `ssh localhost`.

If the remote computer doesn't have the OpenSSH server installed, you will see something like this
![[Pasted image 20221006150522.png]]

To install it, run 


```
sudo apt-get install openssh-server ii.
```

![[Pasted image 20221006150916.png]]


![[Pasted image 20221006151000.png]]

To check if the SSH server is running on the machine, type: 
```
sudo service ssh status
```

And if running properly, you will see something like this: 
![[Pasted image 20221006153910.png]]

And now the set up is done!


#### How to connect via SSH
Now that you have the OpenSSH client and server installed on your computer and the remote one, respectively, you can connect via SSH. 

To connect: 

1.  Get the IP adress of the remote machine by running on the remote computer's terminal `hostname -I`


2. Open the SSH terminal on your machine and run the following command: `ssh your_username@remote_machine_ip_address`        
    If the username on your local machine matches the one on the server you are trying to connect to, you can just type: `ssh host_ip_address` And hit **Enter**.


If the computer you are trying to remotely connect to is on the same network, then it is best to use the private IP address instead of the public IP address. Otherwise, you will have to use the public IP address only. Additionally, make sure that you know the correct TCP port OpenSSH is listening to for connection requests and that the [port forwarding settings](https://phoenixnap.com/kb/ssh-port-forwarding) are correct. The default port is 22 if nobody changed configuration in the sshd_config file. You may also just append the port number after the host IP address.

Here is the example of a connection request using the OpenSSH client. We will specify the port number as well:

```
username@machine:~$ ssh phoenixnap@185.52.53.222 –p7654 phoenixnap@185.52.53.222’s password:

The authenticity of host '185.52.53.222 (185.52.53.222)' can't be established. ECDSA key fingerprint is SHA256:9lyrpzo5Yo1EQAS2QeHy9xKceHFH8F8W6kp7EX2O3Ps. Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added ' 185.52.53.222' (ECDSA) to the list of known hosts. 

username@host:~$
```

You are now able to manage and control a remote machine using your terminal. If you have trouble connecting to a remote server, make sure that:

-   The IP address of the remote machine is correct.
-   The port SSH daemon is listening to is not blocked by a firewall or forwarded incorrectly.
-   Your username and password are correct.
-   The SSH software is installed properly.

**Note:** If SSH responds with a message “Connection refused”, please refer to our article [How To Fix The SSH “Connection Refused” Error](https://phoenixnap.com/kb/ssh-connection-refused) for possible reasons and solutions.

## SSH Further Steps

Now that you are able to establish a connection to your server using SSH, we highly recommend a few further [steps to improve SSH security](https://phoenixnap.com/kb/linux-ssh-security). When you leave the setup with the default values, it is more likely to be hacked and your server can easily become a target of scripted attacks.

Some of the suggestions for hardening SSH by editing the sshd configuration file include:

-   Change the default TCP port where SSH daemon is listening. Change it from 22 to something much higher, for example 24596. Make sure you do not use a port number that is easy to guess, such as 222, 2222 or 22222.
-   Use SSH key pairs for authentication for [passwordless SSH login](https://phoenixnap.com/kb/setup-passwordless-ssh). They are both safer and also allow logging in without the need to use your password (which is faster and more convenient).
-   Disable password-based logins on your server. If your password gets cracked, this will eliminate the possibility of using it to log into your servers. Before you disable the option to log in using passwords, it is important to make sure that authentication using key pairs is working properly.
-   Disable root access to your server and use a regular account with the [su – command to switch to a root user](https://phoenixnap.com/kb/su-command-linux-examples).

You can also use TCP wrappers to restrict access to certain IP addresses or hostnames. Configure which host can connect using TCP wrappers by editing the `/etc/hosts.allow` and `etc/hosts.deny` files.

Note that allowed hosts supersede the denied hosts. For example, to allow SSH access to a single host you will first deny all hosts by adding these two lines in the `etc/hosts.deny`:

`sshd : ALL`  
`ALL : ALL`

Then, in the `etc/hosts.allow` add a line with the allowed hosts for the SSH service. That can be a single IP address, an IP range, or a hostname: `sshd : 10.10.0.5, LOCAL`.

Make sure to keep your log in information secure at all times and to apply security at multiple layers. Use different methods to limit SSH access to your servers, or use services that will block anyone who tries to use [brute force to gain access](https://phoenixnap.com/blog/brute-force-attack) to your servers. [Fail2ban](https://phoenixnap.com/kb/fail2ban) is one example of such service.

### VNC Over SSH

For users who are used to working in a graphical desktop environment with Virtual Network Computing (VNC), it is possible to completely encrypt connections using SSH tunneling. In order to tunnel VNC connections over SSH, you will need to run this command in the terminal on your Linux or UNIX machine:

```
$ ssh -L 5901:localhost:5901 -N -f -l username hostname_or_IP
```

Here is the breakdown of the command above:

-   **ssh** : this starts the SSH client program on your local machine and enables secure connection to the SSH server on a remote computer.
-   **-L 5901:localhost:5901** : states that the local port for the client on the local machine is to be forwarded to the specified host and port of the remote machine. In this case, local port 5901 on the local client is being forwarded to the same port of the given remote server.
-   **-N** : instructs to only forward ports, and not to execute a remote command.
-   **-f** : sends SSH to background after the password is provided, just before the command is executed. Then, you can freely use the terminal to type commands on the local machine.
-   **-l username** : the username you insert here will be used for logging in to the remote server you specified.
-   **hostname_or_IP** : this is the remote system with a VNC server. An example of an IP address would be 172.16.0.5 and the example of a hostname would be myserver.somedomain.com.

You can also connect to a remote server via SSH tunnel from a Windows machine by using PuTTY. In the PuTTY configuration window:

![ssh putty configuration](https://phoenixnap.com/kb/wp-content/uploads/2021/04/ssh-hrd-putty-configuration.png)

1.  Go to Connection -> SSH -> Tunnels
2.  In the Source port field type in 5901
3.  In the Destination field type in localhost:5901
4.  Start the SSH session as you normally would.
5.  Connect to your server with a VNC client of your choice.

**Note:** If you are using Ubuntu, refer to our installation guide [How to Install PuTTY on Ubuntu](https://phoenixnap.com/kb/how-to-install-putty-on-ubuntu).