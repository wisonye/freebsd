# Install **`ligthDM`** as Dislpay Manager

- What is `Dislpay Manager`?

    A display manager, or login manager, is typically a graphical user interface that is displayed at the end of the boot process in place of the default shell.

</br>

- We will install one of the implementation which is called: **LightDM**

    **LightDM** is a cross-desktop **D**isplay **M**anager (also known as a **L**ogin **M**anager). Its key features are:

    - Cross-desktop - supports different desktop technologies.
    - Supports different display technologies (X, Mir, Wayland ...).
    - Lightweight - low memory usage and high performance.
    - Supports guest sessions.
    - Supports remote login (incoming - XDMCP, VNC, outgoing - XDMCP, pluggable).
    - Comprehensive test suite.
    - Low code complexity.

    [Here](https://wiki.archlinux.org/index.php/LightDM) has more detail information.

</br>

- Installation 

    ```bash
    # `lightdm-gtk-greeter` is one of the lightdm greeter which will explain below
    sudo pkg install lightdm lightdm-gtk-greeter
    ```

</br>

- Change the default `greeter`

    A `greeter` just like a graphical login prompt, you can install any one you like.

    By default, all installed `gretter` are located in `/usr/local/share/xgreeters`

    ```bash
    ls -lth /usr/local/share/xgreeters/
    # lightdm-gtk-greeter.desktop
    ```

    `sudo vim /usr/local/etc/lightdm/lightdm.conf` with the following setting to 
    `[Seat:*]` section:


    ```bash
    [Seat:*]
    # ...
    # For example, we just installed this one
    greeter-session=lightdm-gtk-greeter
    # ...

    ```

</br>

- Enable the `lightdm` when booting

    `sudo vim /etc/rc.conf` with the following settings:

    ```bash
    dbus_enable="YES"
    hald_enable="YES"
    lightdm_enable="YES"
    ```

</br>

Now, you're able to install any `DE (Desktop Environment)` or `WM (Window Manager)`.

Let's install `i3` tiling window manager in the next chapter.

</br>
