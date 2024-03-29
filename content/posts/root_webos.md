---
title: "Comó obtener acceso Root en su LG TV con WebOS"
date: 2023-05-04T01:00:00Z
image: /images/post/root_webos/webOS-6.0-New-Home.webp
categories: ["webos", "root", "mod"]
featured: true
draft: false
---


# How to root your LG TV with WebOS installed
Information taken from this [post](https://gist.github.com/throwaway96/e811b0f7cc2a705a5a476a8dfa45e09f)

## Note: 2023 models (2023-03-29)
*If you have a 2023 LG TV, please contact us on [Discord](https://discord.gg/xWqRVEm) or reply here.*

## Update: Dev Mode app workaround (2023-03-08)
To work around LG's latest Dev Mode app update, the instructions below now have you overwrite `jail_app.conf` instead of deleting it.

# Introduction
This guide explains how to root an LG TV using a vulnerability in `crashd`. It works on webOS 4 and above and is currently unpatched (as of 2023-01-28). This means that as long as your TV is running at least webOS 4.0 (i.e., it is a 2018 model or newer), it should be vulnerable. If you are running an older version of webOS, your options are:
* [RootMyTV](https://github.com/RootMyTV/RootMyTV.github.io/) — Firmware released since roughly mid-2022 is probably not vulnerable. [This document](https://gist.github.com/throwaway96/da6ba0d899720b0dedb0b68ea2b957de) lists vulnerable versions for certain SoCs.
* [GetMeIn](https://forum.xda-developers.com/t/getmein-one-time-rooting-jailbreaking-tool-for-webos-lg-tvs.3887904/) — Only works on certain SoCs (maybe just Realtek). I'm not sure which webOS versions are vulnerable, but I have seen it work on webOS 2.2 and 3.4.2. GetMeIn modifies `start-devmode.sh`, which will result in apps being removed on webOS versions that have RootMyTV patched.
* [modifying debugstatus in the NVM](https://gist.github.com/throwaway96/827ff726981cc2cbc46a22a2ad7337a1) — Involves opening your TV and directly accessing the an EEPROM IC. After enabling debug mode, you'll need to spawn a root shell and use it to permanently enable developer mode and install/elevate Homebrew Channel.

**Please don't ask me whether a specific firmware version is vulnerable.** First, I probably don't know. Second, I'll update this document if LG starts releasing patched firmware. Also note that a firmware version without the corresponding model number is practically meaningless.

It is recommended that anyone attempting this procedure do their own research in order to understand how the process works. In general, unless you understand exactly why you're doing something, you shouldn't do it. While there is relatively low risk of permananent damage to your TV, **you're ultimately responsible if anything goes wrong.**

Where PuTTY is used in this guide, any telnet client will work. You can also use LG's CLI tools or any SSH client instead of the Dev Manager program, although instructions for those are not (yet) provided.

# Steps
1. Enable Developer Mode: See [this guide](https://webostv.developer.lge.com/develop/getting-started/developer-mode-app) from LG. If you have trouble (e.g., not getting the prompt to sign in), try rebooting. A reboot is required after setting Dev Mode Status to ON. The Developer Mode app should look something like this:  
    <img src="https://user-images.githubusercontent.com/68320646/223638186-8bff2c84-0de1-4fd5-b909-0a3d6813e442.png" alt="Developer Mode app" width="500"/>


2. Download Software:  
    a. [WebOS-Dev-Manager](https://github.com/webosbrew/dev-manager-desktop/releases)  
    b. [PuTTY](https://www.puttygen.com/download-putty)  
    c. [Homebrew Channel IPK](https://github.com/webosbrew/webos-homebrew-channel/releases) (Latest version, currently 0.6.3)

3. Disable Quick Start+. This is in the menu, but its exact location depends on the webOS version. For example, on webOS 5, after pressing the menu button on the remote, it can be found in All Settings > General > Additional Settings. On webOS 6, it is under All Settings > General > Devices > TV Management.

4. Reboot the TV (e.g., by turning it off and then back on) again. This is in addition to the reboot required when enabling developer mode. *Make sure Quick Start+ is disabled!*  
**Note: If you have an OLED TV, it may stay on for a while (to run the Pixel Refresher) despite appearing to be off. Thus, when you turn it back on, it won't have actually rebooted. You can unplug it to be sure it's off.**

5. In the LG Developer Mode app, enable the Key Server. It should look like this:  
    <img src="https://user-images.githubusercontent.com/68320646/223635272-863dab74-2ede-44df-ad52-ee18294d6f57.png" alt="Key Server enabled"/>

6. In Dev Manager, perform these steps:  
    a. Click "+ Add Device"  
    b. Enter IP address of your TV in "Host Address" field  
    c. Enter passphrase displayed on LG Developer Mode app in "Passphrase" field  
    d. Keep other settings at default, click "Add"  
    e. Click "Install" in the top right corner  
    f. Choose Homebrew Channel IPK  
    g. Make sure Homebrew Channel is installed on your TV  
    h. Click on "Terminal"  
    i. Input this command into the terminal prompt ("Input command here"), then press enter:  
    ```sh
    echo lol>/media/developer/jail_app.conf
    ```
    *Hint: You can copy and paste commands into recent versions of Dev Manager.*  
    There will be no output if the command is successful.  
    **If you are getting a "permission denied" error, you didn't properly reboot the TV.**  
    If you are typing these commands by hand, the shorter `echo>jail_app.conf` should also work as long as you are still in the default `/media/developer` directory.

7. Reboot the TV (e.g., by turning it off and then back on) for a third time. *Make sure Quick Start+ is disabled!*  

8. In Dev Manager, go to "Terminal" and input this command **EXACTLY**, then press enter:
    ```sh
    touch /var/log/crashd/"x;telnetd -l sh"
    ```
    *Note: The character after the dash is a lowercase L, not a one.*  
    If you get an error like `sh: touch: not found`, just repeat the command. When successful there should be no output.  
    If you get a "Permission denied" error, you probably didn't complete the previous steps regarding `jail_app.conf` correctly or did not reboot afterward.  

9. In PuTTY perform these steps:  
    a. Type your TV's IP address in "Host Name" field  
    b. Validate that "Other" and "Telnet" are selected under "Connection type"  
    ![image](https://user-images.githubusercontent.com/68320646/213391395-1c13888d-b1bf-470b-8d6c-c3d12b570583.png)  
    *Note: The default port of 23 is correct.*  
    c. Open the telnet connection to your TV  
    d. Execute this to give root permissions to Homebrew Channel (you can paste into PuTTY by right clicking or pressing Shift+Insert):
    ```sh
    /media/developer/apps/usr/palm/services/org.webosbrew.hbchannel.service/elevate-service
    ```  
    e. Execute this command to ensure developer mode does not expire after 48 hours:
    ```sh
    rm -rf /var/luna/preferences/devmode_enabled && mkdir -p /var/luna/preferences/devmode_enabled
    ```  
    f. If you have used RootMyTV before (even unsuccessfully), execute this command to remove leftover files:
    ```sh
    rm /var/lib/webosbrew/startup.sh /mnt/lg/cmn_data/wam/extra_conf.sh
    ```

10. Uninstall developer mode app from TV home menu.  
**WARNING: Do NOT reinstall the LG Developer Mode app while your TV is rooted!**

11. Power off your TV. *Make sure Quick Start+ is disabled!*  
*Note: If an "Install Homebrew Channel" prompt appears (unlikely), don't choose "yes".*

12. After restart, confirm that "Root status" in Homebrew Channel is "ok"  

13. Turn on SSH in Homebrew Channel and restart  

14. Enjoy your rooted TV!

*Based on instructions by Shadow0304*

# Notes
## Authentication
The default root password (for SSH/SFTP) is `alpine`. Installing a public key for SSH authentication is recommended and will disable the default password. (The default password is not set on boot when `/home/root/.ssh/authorized_keys` exists.) This can be accomplished with the following commands:

```sh
mkdir -p /home/root/.ssh
chmod 700 /home/root/.ssh
echo '<key>' > /home/root/.ssh/authorized_keys
chmod 600 /home/root/.ssh/authorized_keys
```  
Replace `<key>` with your key. It will look something like `ssh-rsa LongBase64String== comment`. See [this guide](https://gist.github.com/throwaway96/dfa4d9ac830d5d53a0ed055eb1c8d107) for more information on setting up public key SSH authentication.

## Homebrew Channel Version
Make sure you're using the latest version of [Homebrew Channel](https://github.com/webosbrew/webos-homebrew-channel/) (currently 0.6.3).

## Versions
*Note: The webOS version is **not** the same as the firmware version.*

### webOS versions
The TV models for each year all run the same major version of webOS. It is not possible to update from one major version to another. Note that webOS 3.0 and 3.5 are separate "major" versions despite having he same leading digit. This is also true for webOS 4.0 and 4.5.

|Year|Version |Codename     |
|----|--------|-------------|
|2014|1.x     |`afro`       |
|2015|2.x     |`beehive`    |
|2016|3.0–3.4 |`dreadlocks` |
|2017|3.5–3.9 |`dreadlocks2`|
|2018|4.0–4.4 |`goldilocks` |
|2019|4.5–4.9 |`goldilocks2`|
|2020|5.x     |`jhericurl`  |
|2021|6.x     |`kisscurl`   |
|2022|7.x (22)|`mullet`     |
|2023|8.x (23)|`number1`    |

Each major version has a codename that is a hairstyle. Each minor version has a codename that is a national park (or similar). The full codename of webOS 4.5, for example, is `goldilocks2-grandcanyon`.

With webOS 7, LG added a marketing name of "webOS 22", with the 22 indicating the year (2022). The upcoming webOS 8/23 situation appears to be similar.

### Firmware versions
The firmware version is often called "software version". Firmware versions look like `03.44.55`, with each of the three components being zero-padded to two digits. Production firmware versions all have a first component of at least 03, as lower numbers are reserved for testing.

# FAQ
## General
### How do I know what version of webOS I am running?

This information can be found in the menu (accessed by pressing the button with a gear on the remote). The exact location within the menu varies across webOS versions.

You also may be able to find the webOS major version by pressing the mute button three times rapidly. This is an example on a webOS 6 TV:  
![webos6-mute-x3](https://user-images.githubusercontent.com/68320646/213929826-76393892-9a58-400b-bd3f-ccaf87e1d1c4.png)  
Note that the firmware version and model number are also shown.

On webOS 3.5, only the firmware version is shown:  
![webos3 5-mute-x3](https://user-images.githubusercontent.com/68320646/214161075-1e2efd91-8f3c-4303-8c8e-da29818525c0.png)

#### webOS 6
To find the version number through the menu on webOS 6, first press the menu button on the remote, then choose "All Settings":  
![image](https://user-images.githubusercontent.com/68320646/213930072-53e20d24-5556-4d38-8100-a211b255fe83.png)

Next, choose "Devices" under "General":  
![image](https://user-images.githubusercontent.com/68320646/213930317-5a6c99e8-017c-4ea5-8558-071eeacdf82e.png)

Then select "TV Management", followed by "TV Information":  
![image](https://user-images.githubusercontent.com/68320646/213930344-6e0a47c6-58c3-4145-a605-3fada916a4b9.png)
![image](https://user-images.githubusercontent.com/68320646/213930392-c8964d05-6f2b-46f1-83ee-cb51877a18e9.png)

The webOS version is under "webOS TV Version":  
![webos6-tvinfo](https://user-images.githubusercontent.com/68320646/213930236-1e777a8a-c00e-4dfa-89f6-51f69316163a.png)


### How can I find my TV's IP address?

The TV may have up to two IP addresses: one for the wired connection, and one for Wi-Fi. You can find the IP address for each interface by in the settings menu under "Network".

You can check whether you have the right IP address for your TV by connecting to either `http://<tv ip>:3000/` or `https://<tv ip>:3001/` in a web browser. At least one of these ports should be open as long as you have screen share/second screen/"LG Connect" enabled. Port 3000 should show a `Hello world` message, while you will likely get a certificate error on port 3001.


### How do I reboot the TV?

If your TV is already rooted, you can use the "System reboot" feature on the Homebrew Channel settings screen or run the `reboot` command via SSH or telnet. These are effective regardless of whether Quick Start+ is enabled.

If Quick Start+ is not enabled, turning the TV off (so that the red standby LED comes on) and back on is usually sufficient. However, OLED TVs will sometimes appear to be off when they are actually running the Pixel Refresher. The Pixel Refresher is triggered on shutdown when the TV has been on for more than four hours since its previous run. To make sure that an OLED (or any TV) is actually off, you can unplug it. Unplugging the TV will also force a fresh boot when Quick Start+ is enabled.


## Rooting
### Why do I get a `No such file or directory` error?

As of 2023-01-26, LG seems to have released a new developer mode jail configuration that does not mount `/var/log/crashd`. It results in an error like this:
```
~ $ touch /var/log/crashd/"x;telnetd -l sh"
touch: /var/log/crashd/x;telnetd -l sh: No such file or directory
```

This configuration is downloaded by the Developer Mode app. It is located in `/media/developer` and named `jail_app.conf`. It is accompanied by `jail_app.conf.sig`, a cryptographic signature used to prevent a modified configuration from working. However, if `jail_app.conf` is not present a default configuration will be used. Since the default configuration does mount `/var/log/crashd`, it will work for our purposes.

Deleting `/media/developer/jail_app.conf` and rebooting the TV would allow the exploit to work. Unfortunately, LG's March 2023 update to the Developer Mode app restricts the permissions of `/media/developer` so that `jail_app.conf` can't be deleted. However, its contents can still be overwritten with the same result.

### Why didn't I see any output after running a command?

Some commands, such as `touch`, do not produce output when successful. As long as you do not see an error message, it likely worked.


### Why am I unable to connect to telnet with PuTTY?

Make sure your PuTTY configuration is correct:
* Under "Connection type", select "Other" and "Telnet"
* "Port" should be 23 (the default when "Telnet" is selected)
* Ensure you are using the correct IP address for your TV

You can check whether the exploit was sucessful by running `pgrep telnetd` in the Dev Manager terminal. If the telnet server is running, this command will output a number. (The number itself is the process ID of the telnet server and is not important.)

### Why am I seeing `LD_PRELOAD` errors while rooting?

These errors appear because LG set an environment variable incorrectly. They are harmless, but you can prevent them from appearing by running this command:
```sh
unset LD_PRELOAD
```

### Why isn't `telnetd` starting?

Certain EULAs must be accepted in order for this exploit to work. If the `touch` command is successful but `telnetd` does not start, this may be the problem. There are two primary EULAs ("Terms of Use" and "Privacy Policy") that are known to be needed, at least in the United States. Other regions may require additional EULAs and/or have a single UI option control multiple underlying EULA settings. You can use the command below to check what you're actually enabling.

![webos6-eula](https://user-images.githubusercontent.com/68320646/216712611-7231e361-32f4-4f99-b95b-9fc62b65000c.png)  
*Two EULAs accepted on webOS 6.*

Changing "Privacy Policy" via the UI requires a reboot. How to find the EULA screen depends on the webOS version. On webOS 6, it can be reached by pressing the menu button then choosing All Settings > Support > Privacy & Terms > User Agreements.  
![webos6-privacy_terms](https://user-images.githubusercontent.com/68320646/216713442-7ccc8f95-6469-4b1d-bf80-dc61f9430f5d.png)
![webos6-useragreements](https://user-images.githubusercontent.com/68320646/216713457-148c70ce-eec3-4013-9318-1c25d9282c93.png)

This command will tell you which EULAs have been accepted:
```
luna-send-pub -f -n 1 'luna://com.webos.settingsservice/getSystemSettings' '{"keys":["eulaStatus"]}'
```

The "Terms of Use" and "Privacy Policy" agreements correspond to `networkAllowed` and `generalTermsAllowed`, respectively.


### How do I download the key for the developer mode SSH server?

To download the private key, named `webos_rsa`, "Key Server" must be enabled in the Developer Mode app. You don't need to reboot after enabling it. When it's enabled, the key file will be available via HTTP on port 9991. Thus it can be downloaded with a web browser at `http://<TV IP>:9991/webos_rsa`.

The `webos_rsa` file is encrypted. The passphrase needed to decrypt it is the 6-character string shown in the LG Developer Mode app.


### Can I use something other than Dev Manager?

The [webOS CLI tools](https://webostv.developer.lge.com/develop/tools/cli-installation) can run commands and install apps on webOS TVs. You can find some additional information about using these on the [webosbrew](https://www.webosbrew.org/pages/configuring-sdk.html) site. Note that there are some differences between the [webOS OSE CLI tools](https://github.com/webosose/ares-cli) and the webOS TV ones.

Any decent SSH client can also be used to run commands on the TV. The OpenSSH `ssh` client is commonly available on Linux and is an optional feature on recent versions of Windows. Assuming you've downloaded the private key file from the TV and have it in the current directory, you can SSH to the TV with the following command:
```
ssh -i webos_rsa -p 9922 prisoner@<TV IP>
```

The passphrase for the key is the 6-character string displayed in the LG Developer Mode app. It is case-sensitive. If you get an erorr like `PTY allocation request failed on channel 0`, you won't have a prompt or some shell features, but you should still have sufficient functionality to run commands and see their output.

Note that you may need additional options to allow older SSH features depending on your client. For example, you may get an error like this:
```
Unable to negotiate with 192.168.1.123 port 9922: no matching host key type found. Their offer: ssh-rsa
```
You should be able to solve the problem by adding the options `-oHostKeyAlgorithms=+ssh-rsa -oPubkeyAcceptedAlgorithms=+ssh-rsa` to the `ssh` command above.

If you want to use PuTTY, you'll have to convert the key file to PuTTY's PPK format using PuTTYgen. Open PuTTYgen and import the key using "Import key" in the "Conversions" menu. You'll need the 6-character passphrase displayed in the LG Developer Mode app to decrypt it. After it's loaded, you can optionally change or remove the passphrase for the generated PPK by editing the "Key passphrase" and "Confirm passphrase" fields. (If you leave them alone, the PPK will have the same passphrase as the original key.) To save the PPK file, click the "Save private key" button.
    
Apps can be installed by transferring the IPK using SFTP then running `luna-send-pub` on the TV with the appropriate arguments. To connect with the OpenSSH command-line `sftp` client, you can use:
```
sftp -i webos_rsa -P 9922 prisoner@<TV IP>
```


### How do I install an app from the command line?

App installation is triggered over the Luna bus. The `prisoner` user available in developer mode has limited access to the Luna bus using the `luna-send-pub` command. To install an app, the IPK file must already be on the TV. Files can be transferred using SFTP.

The Luna endpoint for installing developer mode apps is `luna://com.webos.appInstallService/dev/install`. Luna calls include a JSON payload. For this endpoint, the `id`, `ipkUrl`, and `subscribe` paramters are required. The path of the IPK is supplied in `ipkUrl`. Setting `subscribe` to `true` (along with the `-i` flag) means that multiple response messages will be sent as the status of the request changes. The contents of `id` are not important here.

For example, if the IPK of the app you want to install exists at `/tmp/app.ipk`, you could use the following command to install it:
```
luna-send-pub -i 'luna://com.webos.appInstallService/dev/install' '{"id":"com.ares.defaultName","ipkUrl":"/tmp/app.ipk","subscribe":true}'
```

There will be a series of messages as the installation progresses. After the process completes, you'll have to press control+C to kill `luna-send-pub`.

Note that developer mode apps are installed in a different location than apps installed via the store, and they are deleted when developer mode is disabled or expires.


## After rooting
### Why do I still see update notifications?

Homebrew Channel's startup scripts currently run relatively late in the boot process. This means the TV's update program has already started by the time Homebrew Channel's "Block system updates" option has had a chance to take effect. If you want to make sure updates are completely disabled (and not see the notifications), block these domains (e.g., on your router):
```
snu.lge.com
su.lge.com
su-ssl.lge.com
snu-ssl.lge.com
snu-dev.lge.com
su-dev.lge.com
nsu.lge.com
```  
(Listed roughly in order of importance.)


### Why doesn't SSH (or telnet/other services) start at boot?

Note that the autostart method used by Homebrew Channel 0.5.1+ on webOS 4.5+ only works when certain EULAs have been accepted. Which EULAs are required depends on your region but seem to be the same as those discussed in [this section](#why-isnt-telnetd-starting).

#### webOS 4.0–4.4
The method used for autostart by Homebrew Channel 0.5.1+ only works on webOS 4.5+. You can try the [webosbrew-autostart](https://github.com/webosbrew/webosbrew-autostart) app as a workaround.

#### webOS 4.5–4.9
There is a bug in Homebrew Channel 0.5.1 that may prevent the `startup.sh` file from being automatically installed on webOS versions older than 5.0. This was fixed in Homebrew Channel 0.6.0. You can also install the startup script manually:
```sh
mkdir -p /var/lib/webosbrew
cp /media/developer/apps/usr/palm/services/org.webosbrew.hbchannel.service/startup.sh /var/lib/webosbrew/startup.sh
chmod 755 /var/lib/webosbrew/startup.sh
chown root:root /var/lib/webosbrew/startup.sh
```

#### webOS 7/22
If you are using Homebrew Channel 0.5.1 on webOS 22 (internally, webOS 7), the included SSH server won't work. Homebrew Channel 0.6.0 and later include binaries that are compatible with webOS 22. If for some reason you can't update Homebrew Channel, patched binaries are attached to previous revisions of this guide.


### Should I re-enable Quick Start+ after rooting?

It's up to you. Just be aware that when Quick Start+ is on, turning the TV off won't actually shut it down. If you need to perform a proper reboot (e.g., so that startup scripts will run), you can use "System reboot" on the Homebrew Channel settings page.


### Can I update to a new firmware release?

In general, updating is not recommended because LG could fix vulnerabilities used for rooting. However, as of this writing, the `crashd` vulnerability has not been patched, and you should retain root during a firmware update with Homebrew Channel 0.5.1+. (Note that this does not necessarily apply if your TV was rooted with RootMyTV or GetMeIn.)


### How do I perform a firmware downgrade?

LG has blocked firmware downgrades, even with "expert mode" enabled. Downgrades are only allowed when an AccessUSB device is connected. (AccessUSB devices are hardware tokens that enable debug access. They are presumably provided to LG partners on a limited basis.)


### Can I update to a new webOS version?

While updating your firmware may increase the webOS minor version, it is not possible to update across major verions. This includes updating from 3.4 to 3.5+ or 4.4 to 4.5+.

### How do I disable automatic firmware updates?

The "Auto Update" setting can be found in the menu. The steps to reach this setting vary across webOS versions.

On webOS 6, it can be found by pressing the menu button, choosing "All Settings", "Support", then "Software Update":   
![image](https://user-images.githubusercontent.com/68320646/213930586-a1c8a1b2-4929-422d-86e5-056629444387.png)

The firwmare version is also displayed here.


### Why are all my apps deleted after 48 hours (or after rebooting)?

If all your installed apps are being deleted after roughly 48 hours (due to the expiration of the development mode timer) or on boot, your TV is likely not properly rooted. The `/var/luna/preferences/devmode_enabled` directory created during the above procedure should stop development mode apps from being deleted.

You should not install the LG developer mode app when rooted, as it can cause all apps to be removed. The existence of `/var/luna/preferences/devmode_enabled` as a directory may prevent LG's developer mode app from working. If you lose root access while this directory exists, a factory reset may be required in order to get the developer mode app working.


### Why did I lose root after updating the Homebrew Channel app?

LG changed something in webOS 7 that causes Homebrew Channel's self-update feature to fail in all versions prior to 0.6.3. **If you have webOS 22/7, don't update Homebrew Channel from within the app** unless it's at least version 0.6.3. Updating Homebrew Channel using current versions of Dev Manager (at least through v1.9.11) will also cause root to be lost.

You can use the [Homebrew Channel Updater](https://repo.webosbrew.org/apps/org.webosbrew.safeupdate) tool, which is in the default Homebrew Channel repo, to safely update on webOS 7. It is also possible to update manually as long as you keep a telnet/SSH session open to run `/media/developer/apps/usr/palm/services/org.webosbrew.hbchannel.service/elevate-service` after the update completes and before rebooting.


### Why can't I connect to my TV with Dev Manager after uninstalling the LG Developer Mode app?

The SSH server on port 9922 is provided by LG's Developer Mode app, which is uninstalled at the end of the rooting process. After rooting, you can enable Homebrew Channel's SSH server, which uses port 22. You'll need to reconfigure Dev Manager to use this new SSH server, including changing the login credentials. The easiest way to accomplis this is adding a new device within Dev Manager.

![Dev Manager Add Device](https://user-images.githubusercontent.com/68320646/222486211-839b029c-ce59-4a68-82f9-6849d0f3e30d.png)  
*How to configure Dev Manager to connect to a TV using the default password.*

The username is `root`. If you have not set up public key authentication, you must select "Password" from the "Authentication Method" dropdown and enter the password `alpine`. If you are using a public key, you'll need to choose the "Local Private Key" authentication method, then enter its name and passphrase. The key file itself must be placed in the `~/.ssh` directory (or `%USERPROFILE%\.ssh` on Windows). Note that current versions of Dev Manager support a somewhat limited range of key types.

### How do I determine what SoC my TV has?

The name of the SoC is displayed in the Instart menu next to "Chip Type".

![instart-soc-k7lp](https://user-images.githubusercontent.com/68320646/230500582-c417d2dc-2d54-4fec-87f4-8c784c1eee32.png)  
*This TV has a Realtek K7Lp SoC.*

You can also find it by running this command:
```
nyx-cmd DeviceInfo query device_name
```
The same information can be found in the file `/var/run/nyx/device_info.json`, which is created at boot from the output of `nyx-cmd`.

# Donations

I have a large collection of TV boards and supporting hardware that I use for development and testing of stuff like this. It can get expensive (especially with all the weird cables LG likes to use). If you can afford to, please [donate via ko-fi](https://ko-fi.com/throwaway96) to support my work. I also may be interested in TV parts (and other electronics or test/measurement gear).

