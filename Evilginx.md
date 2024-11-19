# What is it


# How do we use it
It's quite a journey on how to configure and get this working, so here is a detailed guide (mostly taken from [here](https://janbakker.tech/running-evilginx-3-0-on-windows/)).
It's for running the Evilginx locally on a windows instance.

## Guide:
### Preparation
To set up your local installation, we need a couple of things:
- **Visual Studio code** for building and editing the .yaml phishlets files.
- **Go** since Evilginx is build in it. [here](https://go.dev/doc/install)
- **Git** for windows [here](https://gitforwindows.org/).
Download the files to your computer, and run the installer. When installing Go, please pick Visual Studio Code as your default editor.  
To check whether Go and Git are installed correctly, open the command prompt and run:
```
go version
git version
```

### Clone Evilginx
On your local hard drive, create a local folder. For example: **_C:\dev_**

Open a command prompt, and browse to the folder you just created. Next, run:
```
git clone https://github.com/SygniaLabs/evilginx3
```

After the repo is cloned, go into the folder using the command prompt:
```
cd evilginx3
```

Next, run the following command to build and run Evilginx:
```
build_run.bat
```

A few seconds later, Evilginx will start. The first time, Windows Defender Firewall will prompt you to allow access.

### Configure Evilginx for local use
Now that Evilginx is up and running, we’ll need to so dome additional configurations to start using/developing our first phishlet.
We set the IP address of the Evilginx instance to the local address **_127.0.0.1_** and the domain parameter to any domain you wish. This does not need to be a domain you actually own, as we only use this locally. In this demo, we use **_yourfakedomain.com_**
```
config ipv4 127.0.0.1
config domain yourfakedomain.com
```

Next, we need to install the root certificate from Evilginx. This can be found in the user profile folder:
```
%USERPROFILE%\.evilginx\crt\ca.crt
```
Install this as recommended.

### Load the phishlet
Now it’s time to install the first phishlet. This can be either one you developed yourself or one from a public source. For this demo, I use a Microsoft 365 phishlet I developed for Evilginx 3.0. Download the file, and place it in the .\evilginx3\phishlets folder.

Before Evilginx loads the new phishlet, you’ll need to “restart” Evilginx by running:
```
q
build_run.bat
```

### Configure the phishlet and lure
To use the new phishlet, we need to attach the domain name to the phishlet by running
```
phishlets hostname microsoft365 yourfakedomain.com 
phishlets enable microsoft365
```

Next, we need to edit the local DNS file to route all traffic to your local web server address (127.0.0.1)  
The easiest way to do this is by running this command from Evilginx:
```
phishlets get-hosts microsoft365
```

Copy the payload to your clipboard. Now, open Notepad.exe (**as administrator**). Browse to _C:/Windows/System32/drivers/etc_ and open the _**hosts**_ file. If you don’t see the hosts file, change the .txt filter to any file, as the hosts file does not have an extension. Add the payload to the hosts file, and save it. Traffic to yourfakedomain.com is now routed to 127.0.0.1, your local Evilginx server instance. _You can ignore the double entry for login.yourfakedomain.com._

The last step is creating the lure, our phishing URL.
```
lures create microsoft365
lures get-url 0
```

Now, let’s put this to the test. In a browser, past the lure URL, and if all goes well, the phishlet will load, and you are ready to develop your own phishlet!
If you like to proxy your traffic through BurpSuite or Fiddler, please reach out to the docs: [Proxy | Evilginx](https://help.evilginx.com/docs/guides/proxy)


## Custom phishlets
This is a repo that I personally use for phishlets
https://github.com/simplerhacking/Evilginx3-Phishlets
