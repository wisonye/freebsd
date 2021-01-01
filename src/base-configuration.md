# Base configuration

After the installation and reboot, `sshd` should run in background if you choosed to install it.
Then you're able to `ssh` in and finish the configuration below. If you don't install `sshd`, then
just login as `root` before you install `sudo`.

- About `vi: No terminal database found`

    If you `ssh` into your `virtualbox` FreeBSD and saw the error about when running `vi` command,
    that's because your current shell is different with the FreeBSD default one. Run this to fix:

    ```bash
    export TERM=xterm
    ```

    Then, exit and `ssh` in again.

</br>

- Install `sudo`

    ```bash
    # Switch to `root`
    su

    # Update package repo metadata
    pgk update -f

    # Install `sudo`
    pkg install sudo

    # Run `visudo`
    visudo

    # Enable the below line:
    # %wheel ALL=(ALL) ALL
    #
    # Save and exit.
    ```

</br>

- Customize `ds` (Disk Space) script

    Because you're using `auto  ZFS partition` and it will generate separated `dataset` for you. So,
    if you run `df -Th`, you will get similar result like below:

    ```bash
    Filesystem          Type    Size    Used    Avail   Capacity    Mounted on
    zroot/ROOT/default  zfs     26G     1.1G    25G     4%          /
    devfs               devfs   1.0K    1.0K    0B      100%        /dev
    zroot/var/log       zfs     25G     164K    25G     0%          /var/log
    zroot/var/crash     zfs     25G     96K     25G     0%          /var/crash
    zroot/var/tmp       zfs     25G     96K     25G     0%          /var/tmp
    zroot               zfs     25G     96K     25G     0%          /zroot
    zroot/usr/src       zfs     25G     727M    25G     0%          /usr/src
    zroot/tmp           zfs     25G     96K     25G     0%          /tmp
    zroot/usr/ports     zfs     25G     692M    25G     0%          /usr/ports
    zroot/var/audit     zfs     25G     96K     25G     0%          /var/audit
    zroot/usr/home      zfs     25G     132K    25G     0%          /usr/home
    zroot/var/mail      zfs     25G     96K     25G     0%          /var/mail
    ```

    It's easy to figure `How much space already used and how much available`. So you can add the customized
    script to do that.

    ```bash
    mkdir ~/scripts
    ```

    `vim ~/scripts/ds.sh` with the following content:

    ```bash
    #!/bin/sh
    zfs list | grep "/zroot" -B1
    ```

    `chmod +x ~/scripts/ds.sh` and add `~/scripts` to your shell path.
