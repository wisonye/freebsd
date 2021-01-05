# Install X implementation

The **`X`** Window System (**`X11`**, or simply **`X`**) is a 
windowing system for bitmap displays, common on Unix-like 
operating systems. It provides the basic framework for a GUI 
environment:

- Drawing
- Moving windows
- Interact with mouse and keyboard


It's `Client, Server` architecture.

</br>

- Install `Xorg`

    You can  install a `X` implementation via either `pkg` or `port`:


    - Full version of `Xorg` which around **`1GB`**:

        ```bash
        sudo pkg install xorg
        ```

        Or

        ```bash
        cd /usr/ports/x11/xorg
        make install clean
        ```

    </br>

    - Minimal version of `Xorg`:

        ```bash
        sudo pkg install xorg-minimal
        ```

        Or

        ```bash
        cd /usr/ports/x11/xorg-minimal
        make install clean
        ```

    </br>

- Install GPU related X11 driver

    ```bash
    # For AMD GPU
    sudo pkg install xf86-video-amdgpu
    
    # For Intel GPU
    sudo pkg install xf86-video-intel
    ```

    If you don't know the name, then just type 
    `sudo pkg instal xf86-video-` and press `tab`
    key, it will list all possible missing part.

</br>

- Install and enable `dbus` and `hald`

    ```bash
    sudo pkg install dbus hal
    ```

    `sudo vim /etc/rc.conf` with the following settings:

    ```bash
    # DBus and hardware abstraction layer
    dbus_enable="YES"
    hald_enable="YES"
    ```

    Reboot.
