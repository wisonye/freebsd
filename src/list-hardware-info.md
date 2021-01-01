# List hardware info

- List all disks

    ```bash
    sudo camcontrol devlist

    # This is the AFS (Apple File System) driver, /dev/ses0
    # <AHCI SGPIO Enclosure 2.00 0001>  at scbus1 target 0 lun 0 (ses0,pass0)

    # This is the USB 3, /dev/da0
    # <SanDisk Ultra USB 0.0 1.00>      at scbus2 target 0 lun 0 (da0,pass1)

    # This is the USB 3 SSD, /dev/da1
    # <SanDisk Extreme Pro 0>           at scbus3 target 0 lun 0 (da1,pass2)
    ```

</br>

- List all disk with partition info

    Maybe you need to install it first: `sudo pkg install lsblk`

    ```bash
    lsblk
    ```

</br>

- List all USB info (with interface speed)

    ```bash
    sudo usbconfig
    ```

    If you need `USB` auto mount, check [here](https://www.freebsd.org/doc/handbook/usb-disks.html)

</br>

- How to mount `Ext2/3/4` format partition

    You need to load the `ext2fs` module before you can mount the partition.

    ```bash
    # Load the `ext2fs` module
    sudo kldload ext2fs

    # Mount ext4 partition, for example, /dev/da1p3
    sudo mount -t ext2fs /dev/da1p3 /mnt

    # Umount
    sudo umount /mnt
    ```

</br>

- List all PCI devices

    - List all PCI device into a file, then you can search all hardware info on your computer:

        ```bash
        pciconf -lv > ~/hardware_info.log
        ```

    - Only list network NIC info

        ```bash
        pciconf -lv | grep network -B4
        ```

    - Only list display card (GPU) info

        ```bash
        pciconf -lv | grep VGA -B4
        ```
