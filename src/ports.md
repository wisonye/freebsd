# port

The **`Ports`** Collection is a set of Makefiles, patches, and description files. 
Each set of these files is used to compile and install an individual application
on FreeBSD, and is called a **`port`**.

By default, the Ports Collection itself is stored as a subdirectory of **`/usr/ports`**.

When using `port` to install, you can change any default compile option to fit your
requirement.

- Port folder description
    
    For example:

    ```bash
    ll /usr/ports/x11-drivers/xf86-video-intel/
    total 28
    drwxr-xr-x   3 root  wheel  -  512 Oct 23 13:06 ./
    drwxr-xr-x  46 root  wheel  - 1536 Oct 23 13:06 ../
    -rw-r--r--   1 root  wheel  - 1519 Oct 23 13:06 Makefile
    -rw-r--r--   1 root  wheel  -  292 Oct 23 13:06 distinfo
    drwxr-xr-x   2 root  wheel  -  512 Oct 23 13:06 files/
    -rw-r--r--   1 root  wheel  -  567 Oct 23 13:06 pkg-descr
    -rw-r--r--   1 root  wheel  -  240 Oct 23 13:06 pkg-plist
    ```

    - **`Makefile`**: contains statements that specify how the application should be compiled
    and where its components should be installed.

    - **`distinfo`**: contains the names and checksums of the files that must be downloaded
    to build the port.

    - **`files/`**: this directory contains any patches needed for the program to compile and
    install on FreeBSD. This directory may also contain other files used to build the port.

    - **`pkg-descr`**: provides a more detailed description of the program.

    - **`pkg-plist`**: a list of all the files that will be installed by the port. It also tells
    the ports system which files to remove upon deinstallation.

</br>

- Install and remove

    When you install via `port`, you need root premission.

    ```bash
    # Go inside the folder you want to install, for example:
    cd /usr/ports/x11-drivers/xf86-video-intel/
    
    # Compile, install and clean the temp files
    make install clean
    ```

    How to remove installed ports:

    ```bash
    # Go inside the folder you want to install, for example:
    cd /usr/ports/x11-drivers/xf86-video-intel/

    # Remove
    make deinstall
    ```

</br>

- About the disk space

    After installing a few packages via `port`, you will see that
    the `/usr/ports/distfiles` folder hold a lot of space. But DO
    NOT run `rm -rf /usr/ports/distfiles/*`, that will make another
    module which installed via `port` not working anymore!!!

    The correct way to claim back the space is following `portsclean`
    or `portmaster` to do that.

    For more details, visit [here](https://www.freebsd.org/doc/en_US.ISO8859-1/books/handbook/ports-using.html)

