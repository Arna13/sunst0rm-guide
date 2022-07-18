# sunst0rm dependency install

In this guide, I will walk you through the installation of all sunst0rm dependencies so you can start using the script right away! Please, be sure to read [the about secion](../ABOUT.md) before starting!

If you experience any issues, check the [troubleshooting section](../misc/TROUBLESHOOTING.md) before opening an issue or asking in the discord! If your problem is not solved from the troubleshooting section, feel free to open an issue or ask for help [in the discord](https://discord.gg/TqVH6NBwS3). You can mention me there (Arna13) on the support channel and I will try to help you.


## Requirements
  - You will require an Apple Mac to run this, or a hackintosh. VMs have mixed results and your mileage may vary, try it at your own risk.
  - This guide was written for 64bit macOS 10.15+. Compatibility with older versions may not be guaranteed.
  - Make sure to have some free time and patience :)

### Step 0: [Brew](https://brew.sh/)
Lets start simple, get yourself brew installed, you can find the instructions on [their website](https://brew.sh/). Run the command and let it finish, it will ask you to install XCode Command Line Tools, just let it install everything.

TLDR:
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

With homebrew installed, we will start getting ourselves some of the dependencies:
```
brew install automake autoconf pkg-config libtool libusb
```

With this done, we can start compiling some of the dependencies


### Step 1: [libirecovery](https://github.com/libimobiledevice/libirecovery)
To get libimobiledevice we can simply let brew install it so we don't have to compile it manually:
```
brew install libimobiledevice
```
Then enter:
```
brew install libirecovery
```

Now you should be able to run ``libirecovery`` on your terminal.

### Step 2: [futurerestore](https://github.com/futurerestore/futurerestore/)
This one is probably one of the trickiest to compile, thats why compiling futurerestore is beyond the scope of this "simple" guide.
Instead, we will be downloading the nightly build from its [github actions](https://github.com/futurerestore/futurerestore/actions). Bear in mind, a github account is needed for this. 
If you dont want to create a github account, or dont find the download link, try [this one instead](https://nightly.link/futurerestore/futurerestore/workflows/ci/test).

Make sure to always download the correct file for your computer, which in most cases is ``futurerestore-macOS-RELEASE.zip``.

Once you have downloaded the ``.zip`` file, extract the file if it has not automatically done so, and extract the ``.tar.gz`` inside it too. You may need an extra tool to extract tarfiles, you can use [The Unarchiver](https://theunarchiver.com/).

You should now have a binary named futurerestore.
We will give this binary execute permissions in case it doenst have it yet, and then we will move it to a location in our path:
```
chmod +x futurerestore
mv futurerestore /usr/local/bin/
```

Now, you should be able to launch ``futurerestore`` from the terminal.
If it says the program is from an untrusted source and doesn't let you run it, go to your Settings app, to the Security and Privacy icon and allow the execution of the program. This applies to any program that may get this error.

### Step 3: [iBoot64Patcher](https://github.com/Cryptiiiic/iBoot64Patcher)
This one is a bit tricky to compile too, but hopefully we have a binary available too, so we will use it.
The same way as before, you can get your binary via [github actions](https://github.com/Cryptiiiic/iBoot64Patcher/actions) or [nightly.link](https://nightly.link/Cryptiiiic/iBoot64Patcher/workflows/ci/main).
Make sure to download the correct binary for your device, which in most cases is ``iBoot64Patcher-macOS-x86_64-RELEASE``.


Same as before, we extract everything until ge get our iBoot64Patcher. We will give permissions and move it to path:
```
chmod +x iBoot64Patcher
mv iBoot64Patcher /usr/local/bin/
```
Now, you should be able to launch ``iBoot64Patcher`` from the terminal.

### Step 4: [Kernel64Patcher](https://github.com/iSuns9/Kernel64Patcher)
This one is pretty easy to compile. Simply ``git clone`` the repo, ``cd`` into it and use ``gcc`` to compile ``Kernel64Patcher.c``:
```
git clone https://github.com/iSuns9/Kernel64Patcher.git
cd Kernel64Patcher
gcc Kernel64Patcher.c -o Kernel64Patcher
```

Now that we have our binary compiled, we can move it into a directory in our path:
```
mv Kernel64Patcher /usr/local/bin/
```

You can then go back to your previous directory with ``cd ..`` and remove the ``Kernel64Patcher`` directory if you want. This applies to all compiled dependencies.

You should now be able to launch Kernel64Patcher from terminal.

### Step 5: [img4tool](https://github.com/tihmstar/img4tool/)
We will not be compiling this one either, but instead we will grab a precompiled binary.
Grab the latest ``.zip`` for your OS from the [releases tab](https://github.com/tihmstar/img4tool/releases), in this case its ``buildroot_macos-latest.zip``.

Extract the ``.zip`` file, you will now have a folder named ``buildroot_macos-latest``. We will ``cd`` inside the folder and ``cp`` all folders inside ``usr/local/`` folder into our ``/usr/local/`` directory:
```
cd buildroot_macos-latest
cp -r usr/local/* /usr/local/
```

Now, we will ``chmmod`` it to add execution permissions to the bin file:
```
chmod +x /usr/local/bin/img4tool
```

You now should be able to run ``img4tool`` on your terminal.

### Step 6: [img4](https://github.com/xerub/img4lib)
This one can be a bit tricky to compile, but we dont have a bin available so we will compile it manually.

First, we will ``git clone`` the repo with the ``--recursive`` flag, then we will ``cd`` into it and ``make`` lzfse and finally ``make`` img4lib using ``COMMONCRYPTO``:
```
git clone https://github.com/xerub/img4lib.git --recursive 
cd img4lib
make -C lzfse
make COMMONCRYPTO=1
```

If CommonCrypto fails, you might have to compile ``OpenSSL_1_1_1`` to ``make`` with OpenSSL instead of CommonCrypto, but that is beyond the scope of this guide.

You should now move the ``img4`` bin into path and any lib files into ``/usr/local/lib/``:
```
mv img4 /usr/local/bin/
mv libimg4.a /usr/local/lib/
```

Now you should be able to run ``img4`` on your terminal and to use ``img4lib``.

### Step 7: [ldid](https://github.com/ProcursusTeam/ldid)
This one is pretty easy, we can compile it but for this guide we will use brew to install it:
```
brew install ldid
```

This should now let us run ``ldid`` on the terminal.

### Step 8: [restored_external64patcher](https://github.com/iSuns9/restored_external64patcher)
This is an easy one too, but it needs to be compiled.

First, ``git clone`` the repo and ``cd`` into it. Then, just run ``make`` and ``mv`` the binary to path:
```
git clone https://github.com/iSuns9/restored_external64patcher.git
make
mv restored_external64patcher /usr/local/bin/
```

Now, you should be able to run ``restored_external64patcher`` from the terminal.

### Step 9: [asr64_patcher](https://github.com/exploit3dguy/asr64_patcher)
This one is identical to the last one:
```
git clone https://github.com/exploit3dguy/asr64_patcher.git
make
mv asr64_patcher /usr/local/bin
```

Now, ``asr64_patcher`` should be installed and accessible from the terminal.

### Step 10: [Python3](https://www.python.org/downloads/)
We need to install the latest version of ``Python3`` since the version bundled with macOS can have some issues with ``sunst0rm``. 

You just need to [download python](https://www.python.org/downloads/) with the big yellow button and install it. 

I will not guide you though the installation as its only a ``.dmg`` with an installer inside where you just need to click next until it installs, I think you can do this alone :)

Now you should have Python icons in your launchpad, that means it installed correctly.

### Step 11: [sunst0rm](./SUNST0RM.md)
With all external dependencies satisfied, we can start to [install sunst0rm and its pip dependencies](./SUNST0RM.md)
