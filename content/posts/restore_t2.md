---
title: "How to Restore BridgeOS on a T2 Mac + Boot a Mac to DFU Mode"
date: 2022-04-04T04:00:00Z
image: /images/post/post-8.png
categories: ["robotics", "programming", "apple"]
featured: false
draft: false
---

###How to Restore BridgeOS on a T2 Mac + Boot a Mac to DFU Mode
 ![alter-text](/images/post/restore_t2/RestoreBridgeOSDFUMode-768x522.png)
*How to Restore BridgeOS on a 2018+ T2 Mac using Apple Configurator 2. How to Boot your Mac into DFU Mode*

How to Restore BridgeOS on a 2018+ T2 Mac using Apple Configurator 2. How to Boot your Mac into DFU Mode

##Did a macOS Update Brick your T2 Mac? I will Show you how to Boot your Mac into DFU Mode so you can Restore BridgeOS.
This article will go over how to restore BridgeOS on your T2 Mac. This is not something that you will ever normally have to do. Restoring or reinstalling BridgeOS firmware would only be needed in the following situations.

1. Failed macOS Upgrade
2. Failed macOS Combo or Delta Update
3. Failed macOS Security Update
4. Failed macOS Reinstall
5. Failed BridgeOS or Failed Firmware Update
6. “Command Option R” fails to boot your T2 Mac to the newest version of macOS Internet Recovery. (Example: 10.14 is out but the Mac boots to 10.13)
This link shows the different ways you can boot to the Recovery Partition or Internet Recovery [support.apple.com/en-us/HT204904](https://support.apple.com/en-us/HT204904)

Typical symptoms that you might see that would indicate a failed or bricked update.

Mac Seems dead
Will not turn on
Black Screen
No Fan Noise
Power on LED Light does not turn on (Mac Mini or 2020 iMac)
If you find yourself in one of these situations you can follow the instructions below.


My quick 4 min video on how to boot your into DFU mode + restore / revive BridgeOS.

Deep Dive explanation on how to boot your Mac into DFU Mode + How to Reinstall BridgeOS with Apple Configurator 2 – Mr. Macintosh YouTube live demo.
Table of Contents
1. Updates
2. Warning!
3. List of T2 Compatible Macs
4. How do I find my T2 Mac BridgeOS Version?
5. Setup and Cable Requirements before you begin
6. Download Apple Configurator 2 app
7. How to Boot your T2 Mac into DFU Mode
8. Instructions for the MacBook Pro & Air (2018-2020)
9. Instructions for the iMac & iMac Pro (2017 & 2020)
10. Instructions for the Mac Mini (2018-2020)
11. Instructions for the Mac Pro (2019)
12. You made it! Apple Configurator 2 Steps
13. Begin BridgeOS Revive / Restore
14. Finishing Up
15. Can I Downgrade from a Beta Version of BridgeOS to a Production version?
16. Troubleshooting DFU Mode & BridgeOS Update Problems
1. Updates
2. Warning about “Restore” Full Erase! Please Read
The new version of Apple Configurator 2 (2.12.1+) and newer has different options!

Actions > Advanced > Revive Device = Reinstall BridgeOS Only – Revive should be the first option to try. If a Revive does not work, move to the second option Restore.
Actions > Restore = Reinstall BridgeOS & ERASE OS AND USER DATA! – This option will reinstall BridgeOS and erase the SSD. This option is for more serious issues where the Mac does not respond after installing an update.
3. List of T2 Compatible Macs
This is a list of T2 Mac that you can can have BridgeOS restored.

2019-2020 16″ MacBook Pro
2018-2019 13″ & 15″ Macbook Pro
2018-2020 MacBook Air
2018 Mac Mini
2020 iMac
2017 iMac Pro
2019 Mac Pro
4. How do I find the BridgeOS Version on my T2 Mac?
From support.apple.com/en-us/HT203001 – “Choose Apple menu  > About This Mac. This opens an overview of your Mac, including your Mac model, processor, memory, serial number, and version of macOS. To see the greater detail provided by the System Information app, click the System Report button.”

MrMacintosh.com - About my Mac > System Report > BridgeOS version = 17.16.10525
About my Mac > System Report > BridgeOS version = 17.16.10525
5. Setup and Cable Requirements before you begin.
You will need to meet the following requirements –

(The Host Mac will do the work and the Target Mac is the Mac you need to Restore)

1. USB-C Mac as the Host Machine.
2. The Host Mac must have at least macOS 10.13.5 and Apple Configurator 2.6 or newer installed. (Version 2.12.1 is the latest)
3. The Host Mac Must be on the same OS version as the Target Mac that you want to Restore. (Example – If the Target Mac is on 10.15 you will need the Host Mac to be on 10.15. If the Host Mac is on 10.14 you will get an error 10)
3. Internet access on the Host Mac – “You may need to configure your web proxy or firewall ports to allow all network traffic from Apple”
4. USB-C to USB-C Cable – The white Apple USB-C Charge will work fine.(USB-C Cable MUST Support Power & Data). Apple notes that a Thunderbolt 3 to Thunderbolt 3 cable is not supported but I’ve tested it and it works fine.
5. The Host Mac can have the cable plugged in anywhere.
6. The Target Mac MUST have the USB-C Cable Plugged in to the Left Hand side USB-C port. This is First port in line (Port closest to the front of the Mac or trackpad) If you are still confused look at the picture below.
If you don’t meet all the prerequisites booting to DFU Mode or BridgeOS Upgrade might fail.
6. Download Apple Configurator 2
MrMacintosh.com - Download Apple Configurator 2 app from the Mac App Store. Version 2.6 or higher is required.
Download Apple Configurator 2 app. Version 2.6 or higher is required.
If you do not have Apple Configurator 2, you can download it now from the Mac App Store with this link.

https://apps.apple.com/us/app/apple-configurator-2/id1037126344?mt=12

7. How to Boot your T2 Mac into DFU Mode
With all the startup keyboard commands you can issue a Mac, booting into DFU Mode should be pretty simple right?

NOPE!

You have to follow a very particular sequence to get this to work. I have attempted to find the exact way to get this to work every time. Even then sometimes the system will refuse to Boot into DFU mode.

MrMacintosh.com - Me trying to get my T2 Mac into DFU mode without turning it off or booting into macOS.
Me trying to get my T2 Mac into DFU mode without turning it off or booting into macOS.
Apple’s Instructions
You can find Apple’s instructions for booting into DFU mode here.

help.apple.com/configurator/mac/2.7.1/#/apd0020c3dc2

UPDATE 4/13/20: New Apple Support Document

support.apple.com/guide/apple-configurator-2/revive-or-restore-mac-firmware-apdebea5be51/mac

MrMacintosh.com - Apple's instructions for booting your T2 MacBook Pro into DFU mode.
Apple’s instructions for booting your T2 MacBook Pro into DFU mode. Image: Apple Inc
8. My Instructions for the MacBook Pro & Air
Bottom line, it’s hard to get your T2 Mac into DFU mode. You could try Apple’s instructions 10 times and STILL not get into DFU mode.

Once you have meet all of the pre requisites above, follow the instructions below to get into DFU Mode every time.

1. The Target Mac must be OFF to begin.
2. Press the Power button and hold for 1 second.
3. While STILL holding power immediately hold down Right Shift, Left Control and Left Option.
Hold down all 4 keys for 8 Seconds (count 1 one thousand) then let go of all keys.
You will not see anything on the Target Mac screen.
Keep an eye on the Host Mac’s Apple Configurator 2 Application. The App should say “Connect Devices”
When the Target Mac is booted into DFU mode correctly, the host will show a big DFU icon in Apple Configurator 2.
After you see the DFU picture pop up on the Host Mac you can let go of the keys.
MrMacintosh.com - DFU T2 Booting Instructions - Make sure the Mac is OFF. Hold down power for 1 second then also hold Right Shift, Left Control and Left Option for 8 total seconds then let go.
DFU T2 Booting Instructions – Make sure the Mac is OFF. Hold down power for 1 second then also hold Right Shift, Left Control and Left Option for 8 total seconds then let go.
9. Instructions for the iMac (2020) & iMac Pro (2017)
The iMac 2020 & iMac Pro 2017 are a little different yet are super simple to get into DFU Mode.

1. Disconnect the power cord from the iMac Pro or Mac Mini.
2. Plug USB-C/Thunderbolt cable into the USB-C port next to the Ethernet Port.
3. Plug the other end into the Host Mac.
4. While holding down the power button, connect the iMac Pro or Mac Mini to power and continue to hold the power button for about 3-5 seconds
5. You should now see the DFU logo on the Host Mac.
10. Instructions for the Mac Mini (2018)
The Mac Mini 2018 instructions are close to the iMac Pro but the USB-C port that you need is next to the HDMI port instead of the Ethernet port like the iMac Pro.

MrMacintosh.com - How to boot a Mac Mini 2018 into DFU mode to restore BridgeOS - Image: Apple Inc
How to boot a Mac Mini 2018 into DFU mode to restore BridgeOS – Image: Apple Inc
1. Disconnect the power cord from the Mac Mini.
2. Plug USB-C/Thunderbolt cable into the USB-C port next to the HDMI Port.
3. Plug the other end into the Host Mac.
4. While holding down the power button, connect the Mac Mini to power and continue to hold the power button for about 3-5 seconds
5. You should now see the DFU logo on the Host Mac.
11. Instructions for the Mac Pro (2019)
The Mac Pro 2019 instructions were just added to the DFU instruction guide.

MrMacintosh.com - How to boot a Mac Pro 2019 into DFU mode to restore BridgeOS - Image: Apple Inc
How to boot a Mac Pro 2019 into DFU mode to restore BridgeOS – Image: Apple Inc
1. Disconnect the power cord from the Mac Pro.
2. Plug USB-C/Thunderbolt cable into the USB-C port farthest from the power button.
3. Plug the other end into the Host Mac.
4. While holding down the power button, connect the Mac Pro to power and continue to hold the power button for about 3-5 seconds.
5. You should now see the DFU logo on the Host Mac.
12. You made it! Apple Configurator 2 Steps
The hard part is now over. Now we can restore BridgeOS on the Target Mac. When you first open Apple Configurator 2 the screen will look like this.

MrMacintosh.com - This is what you will see if the Mac is NOT booted to DFU mode.
This is what you will see if the Mac is NOT booted to DFU mode.
Once your Mac is booted to DFU mode, you will see this screen on Apple Configurator 2. You are now ready for the next step.

MrMacintosh.com - When you see a big DFU icon when your Mac is properly booted into DFU Mode.
When you see a big DFU icon when your Mac is properly booted into DFU Mode.
13. Begin BridgeOS Revive
You are now ready to restore BridgeOS on the Target Mac. Click Actions > Advanced > Revive Device.

(DO NOT CLICK RESTORE YET) Only run Restore if Revive does not work. (Restore Erases your Hard drive!!!!!!!)

MrMacintosh.com - Apple Configurator 2. Actions > Restore.
OLD PICTURE – Select Actions > Advanced > Revive Device (NOT Restore) 1st
You will now see a warning message. Do you want update “iBridge” to the latest firmware version? You cannot undo this action. This means that once you update BridgeOS/iBridge you cannot go back to the previous version.

An updated Apple support document shows that we now have 2 different options.

Actions > Advanced > Revive Device = Reinstall BridgeOS Only
Actions > Restore = Reinstall BridgeOS & ERASE OS AND USER DATA!
MrMacintosh.com - Apple Configurator 2 version 2.12.1 - New Message that warns that the BridgeOS Restore will ERASE ALL OS AND USER DATA!
AC2 version 2.11 – 2.12.1 ??? New Message that warns that the BridgeOS Restore will ERASE ALL OS AND USER DATA!
The message below is what you will see on at least AC2 version 2.10 and below. OR if you click Revive instead of restore.


AC2 Version 2.10 and below – Do you want to restore and update “iBridge” to the latest firmware version?
Click the Restore Button to begin. Step one will download the latest BridgeOS update from Apple.

MrMacintosh.com - Step 1. Downloading the latest BridgeOS from Apple.
Step 1. Downloading the latest BridgeOS from Apple.
Step 2. Unzipping BridgeOS

MrMacintosh.com - Step 2. Unzipping the BridgeOS Update.
Step 2. Unzipping the BridgeOS Update.
Step 3. Installing BridgeOS Update.

MrMacintosh.com - Step 3. Installing BridgeOS
Step 3. Installing BridgeOS
14. Finishing Up
If you would like to see more information you can click View and see a new activity window.

MrMacintosh.com - Apple Configurator 2 Activity window.
Apple Configurator 2 Activity window.
The entire process will only take about 4-10 Minutes. Most of the time is spent downloading the 400-600MB BridgeOS Update. The Unzip and Install parts only take about 1 minute each. When complete the Mac will automatically Boot up.

NOTE: with version 2.12.1, the entire process may never finish correctly and get stuck at the final part (probably a bug). Once your Target Mac is at the login window the restore is complete. The error that you might see is 0xFA5 (4005)

15. Can I Downgrade from a Beta Version of BridgeOS to a Production version? i.e Bug Sur BridgeOS to Catalina Version?
Let’s say that you installed Big Sur Beta 6, and are now having a ton of problems. You probably want to downgrade to Catalina so you can work again. The only problem is, you are still on Big Sur Beta 6 BridgeOS version 18.16.12370. Keep in mind, your Mac SHOULD still work fine with this version. An example of this is if you have Catalina 10.15.6 installed on your Mac, your BridgeOS version is 17.16.16610. Let’s say that you need to test something on version 10.15.3. After installing Catalina 10.15.3, your BridgeOS version will NOT be downgraded to the period correct version of 17.16.13050. It will run just fine on the 10.15.6 version of 17.16.16610 BridgeOS. The same is the case if you have a Big Sur Beta version of BridgeOS and you downgrade to Catalina.

The answer is YES, follow the link below for an explanation.

mrmacintosh.com/how-to-downgrade-t2-bridgeos-beta-to-a-production-version/

16. Troubleshooting DFU Mode & BridgeOS Update Problems
I can’t get my Mac to boot into DFU mode. This is the toughest part of the whole process as I mentioned above. Keep trying the steps I listed above. Sometimes it takes multiple attempts to get his to work.
You can use System Information to see if the USB-C port lists your Mac in DFU Mode.
MrMacintosh.com - System Information showing a Mac plugged in booted to DFU Mode.
System Information showing a Mac plugged in booted to DFU Mode.
BridgeOS Restore Error 79- The OS Cannot be restored on this device. The Operation couldn’t be completed. (AMRestoreErrorDomain error 79 – Failed to handle message type StatusMsg) [AMRestoreErrorDomain – 0x4F (79)] – If you get this error it means that the BridgeOS update has failed and is unable to complete. The system will be unable to boot. When powered on the screen will be black. The Mac will have to be brought to an Apple Store for Service.
MrMacintosh.com - BridgeOS Restore Error - The OS Cannot be restored on this device. The Operation couldn't be completed.
BridgeOS Restore Error – The OS Cannot be restored on this device. The Operation couldn’t be completed.
BridgeOS Restore Error 10 – The BridgeOS Restore failed! This is most likely because the host Mac was 1 or 2 OS Versions behind the Target Mac. The Host and Target Mac need to be on the same OS Version.

If your Target Mac is on 10.15, then your Host Mac needs to be on 10.15.

The OS Cannot be restored on this device.

The operation couldn’t be completed. (AMRestoreErrorDomain error 10 – Failed to handle message type StatusMsg) [AMRestoreErrorDomain – 0xA (10)]

MrMacintosh.com - BridgeOS Restore Error 10 - The Host and Target Mac need to be on the same OS Version.
BridgeOS Restore Error 10 – The Host and Target Mac need to be on the same OS Version.
Host Mac and Target Mac Disconnected during restore. – Error 4005

The OS Cannot be restored on this device.

Gave up waiting for device to transition from RestoreOS state to BootedOS State. [com.apple.MobileDevice.MobileRestore – 0xFA5 (4005)]

MrMacintosh.com - BridgeOS Restore Error 4005
BridgeOS Restore Error 0xFA5 (4005)
This error will come up when the restore process has been interrupted.

Or, you might get this using Apple Configurator 2 version 2.12.1, as the process never seems to complete properly. If the Target Mac awakes to the login window the process is complete even though the progress bar is at 100%. After unplugging the USB-C cable you will get the error above.

Apple Configurator 2 Reports RECOVERY instead of DFU Status.

MrMacintosh.com - Apple Configurator 2 Reports RECOVERY instead of DFU Status.
Apple Configurator 2 Reports RECOVERY instead of DFU Status.
If you see RECOVERY this means that BridgeOS is unable to boot and is the default status when you power on the Mac.
Failed BridgeOS Restore due to OS Version Mismatch! The Target Mac is a previous OS i.e 10.14 trying to restore a 10.15 Mac, the update will fail with an Error 10
If the Mac already failed the Upgrade, it could already be in this status. If so, you can attempt a BridgeOS restore.
Configurator could not perform the requested action. Apple Controller devices do not support this action.

This means that you selected Actions > Update, which is not supported. You need to select Actions > Advanced > Revive Device


Apple Configurator 2 BridgeOS Firmware Download Location.

Thanks MrMacintosh Reader Max C for letting me know the location of the BridgeOS Firmware files.

~/Library/Group Containers/Group.com.apple.configurator/Library/Caches/Firmware

Apple Configurator 2 Log Location

~/Library/Group Containers/xxxxxxx.group.com.apple.configurator/Library/Logs

Note that for version 2.12.1 the log does not seem to be working.

If you have any additional information or questions Contact Me!

tio expedita praesentium est adipisci dolorem ut eius!

## Covid-19 Situation

Nam ut rutrum ex, venenatis sollicitudin urna. Aliquam erat volutpat. Integer eu ipsum sem. Ut bibendum lacus vestibulum maximus suscipit. Quisque vitae nibh iaculis neque blandit euismod.

> Lorem ipsum dolor sit amet consectetur adipisicing elit. Nemo vel ad consectetur ut aperiam. Itaque eligendi natus aperiam? Excepturi repellendus consequatur quibusdam optio expedita praesentium est adipisci dolorem ut eius!

Lorem ipsum dolor sit amet consectetur adipisicing elit. Nemo vel ad consectetur ut aperiam. Itaque eligendi natus aperiam? Excepturi repellendus consequatur quibusdam optio expedita praesentium est adipisci dolorem ut eius!

![alter-text](/images/post/post-1.png)
*Example Caption*

Lorem ipsum dolor sit amet consectetur adipisicing elit. Nemo vel ad consectetur ut aperiam. Itaque eligendi natus aperiam? Excepturi repellendus consequatur quibusdam optio expedita praesentium est adipisci dolorem ut eius! Lorem ipsum dolor sit amet consectetur adipisicing elit. Nemo vel ad consectetur ut aperiam. Itaque eligendi natus aperiam? Excepturi repellendus consequatur quibusdam optio expedita praesentium est adipisci dolorem ut eius!
