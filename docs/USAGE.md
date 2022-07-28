# sunst0rm usage

The sunst0rm script is mainly split in two parts: 
  - Restoring the device
  - Preparing the boot files

First, we will need to restore the device. **This will erase all your data!** Back up any important data before proceeding.

Before we start, you have to download an IPSW for your device from a [SEP compatible](https://docs.google.com/spreadsheets/u/0/d/1Mb1UNm6g3yvdQD67M413GYSaJ4uoNhLgpkc7YKi3LBs/htmlview) iOS version. IPSWs can be easily found on the internet, the IPSW site of choice is [ipsw.me](https://ipsw.me/).

Once you have your IPSW, move it to your ``sunst0rm`` dir.

Now, you will need to get some blobs to restore. **You do not need blobs from the version you are trying to restore!** Any version blobs will work.
I will not get into details on how to get blobs for your device since there are lots of tutorials online, you will need to get blobs for your specific ECID and boardconfig.

ECID and boardconfig can be found running ``irecovery -q`` on a terminal with an iPhone connected **in DFU mode**. 

Save your boardconfig (shown in MODEL), you will need it in a moment.

To restore our device, as well as to boot it, we need a Pwner for our device. Different CPUs will need different Pwners.
I will not be getting further into how to get your iPhone into pwndfu, you should be able to find online how to enter pwndfu on your specific device model.

We will need a pwner with the ability to remove sigchecks! For example, in ipwndfu: ``python2 ipwndfu -p --rmsigchecks``.
If you dont remove sigchecks, the restore will hang at sending iBSS/iBEC and will not restore/boot!
## Placing the device into pwndfu mode with gaster or ipwndfu. ##
- Compiling and running gaster. 
```
git clone https://github.com/0x7ff/gaster
cd gaster
make
mv gaster /usr/local/bin/gaster
gaster pwn
```
- Using ipwndfu.
```
git clone https://github.com/hack-different/ipwndfu.git
cd ipwndfu
./dev_install.sh
ipwndfu -p && ipwndfu --patch-sigchecks && ipwndfu --repair-heap
```

Once you have your iPhone in pwndfu with sigchecks removed, you may continue.

We will start typing our command into our terminal but **do not hit enter just yet!**

First, if you are not in the ``sunst0rm`` directory, ``cd`` into it.

Now, type this command filling the information in caps with your own:
```
python3 sunstorm.py -i 'IPSW' -t 'SHSH2' -r -d 'BOARDCONFIG'
```

Where:
  - IPSW: This is the path to the IPSW you just downloaded, you can drag it from finder into the terminal while youre typing the command.
  - SHSH2: This is the blob you got before. You can also drag and drop it into the terminal.
  - BOARDCONFIG: This is the boardconfig I told you to save from ``irecovery -q`` before.

An example command may look as follows:
```
python3 sunstorm.py -i ios14.3.ipsw -t blobs.shsh2 -r -d n71map
```

Now, **before pressing enter**, we will find out if we need to remove Kernel Patch Protections (kpp) or not. This is very simple, if your device is A9 or lower, then **YOU NEED** to add the ``--kpp`` flag. If you have a device A10 or greater, you **DO NOT NEED** them.

Therefore, following my example with an A9 device:
```
python3 sunstorm.py -i ios14.3.ipsw -t blobs.shsh2 -r -d n71map --kpp
```
**Note: If your device does not have baseband such as iPod Touch or Wifi Only iPads pass --skip-baseband to sunst0rm arguments.**
Example Usage: 
```
python3 sunstorm.py -i IPSW -t blob.shsh2 -r -d j81ap --kpp --skip-baseband
```

If you are using an A10+ device, **DO NOT** add ``--kpp``

Now we are ready to execute the command. After a while, it will ask you if you want to restore your device and if your device is in pwndfu with sigchecks removed. Type ``y`` in both statements to continue.

Hopefully futurerestore will start restoring your device, your screen will flash different colours and it will start the restore progress bar.

If you get any error, please check [the troubleshooting section](./misc/TROUBLESHOOTING.md) before opening an issue or asking in the discord!

If the progress completed fine, you should be now looking at an iphone with a blank screen after the restore bar completed, we are very close to booting now!

Pay attention to this part since its very important. You will now enter the same command as before, except you will change the ``-r`` to ``-b``, and you will add your device identifier at the end of it like this: 

```
python3 sunstorm.py -i 'IPSW' -t 'SHSH2' -b -d 'BOARDCONFIG' -id 'IDENTIFIER'
```

Where:
  - IDENTIFIER: is your [iPhone model identifier](https://www.theiphonewiki.com/wiki/Models#iPhone) (Check the identifier column)

Following my A9 device example:
```
python3 sunstorm.py -i ios14.3.ipsw -t blobs.shsh2 -b -d n71map --kpp -id iPhone8,1
```

**Note that since I am using an A9 or lower device, I am putting ``--kpp`` on this command too!**

This command will end pretty soon and we should have a folder named ``boot`` in our ``sunst0rm`` directory.

We are on our final steps now. The next steps will need to be repeated every time we want to boot the device.

First of all, our device is now in some sort of "fake/broken" DFU mode. We need to get into the real DFU mode.

Just get into DFU as you did before, even if the screen is blank it will work. For example for my iPhone6S: Press Home + Pwr for 10s, then let Pwr go and keep holding Home for another 10s.

Your iPhone should reconnect to your computer. Now, you need to get into pwndfu with sigchecks removed just like before. If the exploit fails, try to get into the real DFU mode again until it works.

Once we are in pwndfu with sigchecks removed, we only need to run ``./boot.sh`` or ``./boot-a10.sh`` depending on our device.

The screen should light up and you will soon start seeing verbose. Your iPhone will finish to restore and then, it may power off again. 

Repeat this process to boot it up again and you should be greeted with the Hello screen of your iOS version of choice!

Now you can use the device normally, just try avoid letting it turn off or you will need your PC to turn it back on again.
