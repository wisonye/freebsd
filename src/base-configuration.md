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

    

