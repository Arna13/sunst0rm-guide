# Getting sunst0rm on Linux using QEMU

This part of the guide focuses on getting sunst0rm on Linux using a KVM (Kernel Virtual Machine) using USB passthrough

This is only necessary if you want to follow this guide. You can always use [the linux version of the script](https://github.com/MCApollo/sunst0rm)

### This only works on Linux. Do not even bother trying to do this on Windows.

### This part of the guide has only been done on Ubuntu 22.04. Other distros should work too.



## Getting started

First off, you need to create the KVM. You can use any method you'd like but personally, I'd recommend using [this](https://github.com/kholia/OSX-KVM). Any other method would work too.

Follow the guide in the linked repo (or for whatever method you're using)

### Notes
For the KVM, I'd recommend using either Big Sur or Catalina (Monterey and up could work too but I don't recommend it).

You only need about 50GB to restore with sunst0rm.

You need at the very least 4GB of RAM allocated to the KVM to run macOS.

I've only done this on Ubuntu 22.04 for now. Other distros *should* work fine, however.

The install **will** take a while. On my machine, it took over 45 minutes to download and install.

Depending on your machine, the VM can be very slow.

## Getting your USB controller passed to macOS

### This part can be a bit tricky. If you're having any issues with this part, feel free to ask in the [Discord server](https://discord.gg/TqVH6NBwS3)

At this point, macOS should be fully working! If it is, give yourself a well deserved pat on the back!

Now, you should add the KVM to virt-manager. The method I linked earlier shows you how to do it.

### This goes without saying that you need to have virt-manager installed for this.

Once the KVM is added to virt-manager, it should appear on the main menu. Try launching the VM now

#### If the VM doesn't boot due to a permission related error, try launching virt-manager with `sudo virt-manager`.

Now, you need to passthrough your USB controller to the VM. To do this, shut down the VM and open the details page in virt-manager.

![image](https://user-images.githubusercontent.com/45905959/198859377-70c9df94-ce47-4b39-82fa-326d1a7b0b5a.png)
The page should look like this 

Next, click add hardware and go to "PCI Host Device"

![image](https://user-images.githubusercontent.com/45905959/198859403-5bebabfb-87cf-4ad2-bde6-7db3292056b4.png)
You should see something similar to this

Add anything related to USB. In my case, `Intel Corporation 8 Series USB xHCI HC` is my USB 3.0 port and `Intel Corporation 8 Series USB EHCI #1` is my USB 2.0 controller

Once you add the USB controller(s), there should be something new that looks like this 

![image](https://user-images.githubusercontent.com/45905959/198860052-08dded3e-560c-4843-852f-33293addfb05.png)

## Booting the KVM
If you try booting the VM and you see this, you'll have to do [this](https://bit.ly/3DkkNqI)

![image](https://user-images.githubusercontent.com/45905959/198859967-57e8d530-df79-4d8a-8e31-d0f0ee35410e.png)

If the above doesn't fix the issue, ask in the previously linked Discord server.

If the above *does* fix the issue, try connecting a USB device to the controller you forwarded. If that works, congratulations, you can proceed to the next step!

You have to start with the [dependencies](docs/install/DEPENDENCIES.md).
