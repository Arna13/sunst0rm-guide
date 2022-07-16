# sunst0rm-guide
WIP

## Guide to install and use sunst0rm on macOS x86.
First of all, we need all dependencies satisfied. This will take some time so please, be patient with the process :)

### Step 0: Brew
Lets start simple, get yourself brew installed, you can find the instructions on [their website](https://brew.sh/). Run the command and let it finish, it will ask you to install XCode Command Line Tools, just let it install everything.

TLDR:
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Step 0.1: Brew initial dependencies
With homebrew installed, we will start getting ourselves some of the dependencies:
```
brew install automake autoconf pkg-config libtool libusb
```

With this done, we can start compiling some of the dependencies


### Step 1: [libirecovery](https://github.com/libimobiledevice/libirecovery)
First of all, ``git clone`` the repo and ``cd`` into it:
```
git clone https://github.com/libimobiledevice/libirecovery.git
cd libirecovery
```

Then, simply run the ``autogen.sh`` script and compile it normally with ``make``. When its done compiling, install it with ``sudo make install``
```
./autogen.sh
make
sudo make install
```

After it finishes, you can go back to your previous directory with ``cd ..``. You can now remove the ``libirecovery`` directory if you want.

Now you should be able to run libirecovery on your terminal.

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

Now, you should be able to launch futurerestore from the terminal.
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
Now, you should be able to launch iBoot64Patcher from the terminal.

