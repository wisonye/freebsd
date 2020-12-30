# Install process

Start your `FreeBSD` virtual machine, after booting, press `Enter` and wait for loading,
then you will see this UI:

![install-4.png](./images/install-4.png)

Press `Install`.

</br>

![install-5.png](./images/install-5.png)

Press `Enter` to accept the default keymap (`us`) or choose the you use.

</br>

![install-6.png](./images/install-6.png)

Fill your `hostname` and `OK`.

</br>

![install-7.png](./images/install-7.png)

Select which components you want to install:

- **`base-dbg`** - Base tools like cat, ls among many others with debug symbols activated.

- **`kernel-dbg`** - Kernel and modules with debug symbols activated.

- **`lib32-dbg`** - Compatibility libraries for running 32-bit applications on a 64-bit version of FreeBSD with debug symbols activated.

- **`lib32`** - Compatibility libraries for running 32-bit applications on a 64-bit version of FreeBSD.

- **`ports`** - The FreeBSD Ports Collection is a collection of files which automates the downloading, compiling and installation of third-party software packages. Chapter 4, Installing Applications: Packages and Ports discusses how to use the Ports Collection.

- **`src`** - The complete FreeBSD source code for both the kernel and the userland. Although not required for the majority of applications, it may be required to build device drivers, kernel modules, or some applications from the Ports Collection. It is also used for developing FreeBSD itself. The full source tree requires 1 GB of disk space and recompiling the entire FreeBSD system requires an additional 5 GB of space.

- **`tests`** - FreeBSD Test Suite. 

Then `Ok`.

</br>

![install-8.png](./images/install-8.png)

Choose the file system format you want, I highly recommend you choose `Auto (ZFS)`, as `FreeBSD` support it natively and you got the `snapshot`
feature with zero cost!!!

</br>

![install-9.png](./images/install-9.png)

Choose your `USB` drive which should mark as `da0`.

</br>

![install-10.png](./images/install-10.png)

A few things here:

- As you're installing `FreeBSD` to `USB`, then you don't need `SWAP` (especially your `USB` drive is `SSD`), make sure set it to `0`.

- For the `Partition Scheme`, use `GPT (UEFI)`!!! I have a bad experinece when I choose `GPT (BIOS + UEFI)` (not sure that's the problem or not).

Then, go to the top one `Pool Type/Disk` and press `Enter` to go to the next settings.

</br>

![install-11.png](./images/install-11.png)

Press `Enter` to choose the default `stripe`.

</br>

![install-12.png](./images/install-12.png)

Make sure to choose your `USB` drive. It will go back to the prev setting UI.

</br>

![install-13.png](./images/install-13.png)

Go to the most top one `Install     Proceed with Installation` and press `Enter`.

</br>

![install-14.png](./images/install-14.png)

Press `Enter` to confirm, all data in your `USB` will be wiped.

</br>

![install-15.png](./images/install-15.png)

Now, it will fetch all the files.

</br>

![install-16.png](./images/install-16.png)

Pay attention:

_This is what happened to me when I choosed `GPT (BIOS + UEFI)`, it will hang on there and you have to reboot the virtual machine and repeat the steps_
_above._

</br>

![install-18.png](./images/install-18.png)

After fetching all the files, copying files step will happen.

</br>

![install-19.png](./images/install-19.png)

Then, set the new root password.

</br>

![install-20.png](./images/install-20.png)

Press `Enter` to accept the default `NIC` (Network Interface Card).

</br>

![install-21.png](./images/install-21.png)

Press `Enter` to config `IPv4`.

</br>

![install-22.png](./images/install-22.png)

Press `Enter` if you want `dhcp` to be endabled, or choose `No` and add your customized IP settings.

</br>

![install-23.png](./images/install-23.png)

Choose `No` if you don't need `IPv6`.

</br>

![install-24.png](./images/install-24.png)

If you choosed `dhcp` in the prev step, then it should fill the `DNS` settings automatic. Otherwise, just fill your own settings there.

</br>

![install-25.png](./images/install-25.png)

Pick your time zone and `Enter`.

</br>

![install-26.png](./images/install-26.png)

Pick your time zone and `Enter`.

</br>

![install-27.png](./images/install-27.png)

Just `Skip`, as you will enable `ntpd` service later.

</br>

![install-28.png](./images/install-28.png)

Just `Skip`, as you will enable `ntpd` service later.

</br>

![install-29.png](./images/install-29.png)

Enable the service you want,  then `Enter`.

</br>

![install-30.png](./images/install-30.png)

Choose the right option for you, `clean_tmp` will be useful.

</br>

![install-31.png](./images/install-31.png)

Press `Enter` to add new user.

</br>

![install-32.png](./images/install-32.png)

Fill everything you needed, make sure to add the new user to the `wheel` group!!!

</br>

![install-34.png](./images/install-34.png)

Type `Yes` to confirm.

</br>

![install-35.png](./images/install-35.png)

Type `No` if you don't need another user.

</br>

![install-36.png](./images/install-36.png)

Press `Enter` to exit the installation process.

</br>

![install-37.png](./images/install-37.png)

Installation is done so far, choose `No` if you don't have extra config at this moment.

Then `reboot` and poweroff the virtual manchine.

</br>

If you run `sudo fdisk -l` right now, you should able to see your `USB` drive has similar partition info like below:

![install-38.png](./images/install-38.png)
