# Install **`i3`** Window Manager

A window manager (**`WM`**) is system software that controls the placement and appearance of windows
within a windowing system in a graphical user interface (GUI). It can be part of a desktop environment 
(**`DE`**) or be used standalone.

We will install a **`Tiling`** window manager which calls **`i3`**.

- How to install

    ```bash
    sudo pkg install i3 i3-gaps i3status i3lock dmenu
    ```

    Then we need on more comopnent from **`AUR`**`:
    ```bash
    yay -Sy i3exit
    ```
    
| Component | Description|
| --------- | -----------
| `i3-gaps` | Provides a grap between different tiling windows. |
| `i3-wm`   | The core component. |
| `i3block` | Define blocks for your i3bar status line. |
| `i3lock`  | mproved screenlocker based upon XCB and PAM.|
| `i3status`| Generates status bar to use with i3bar, dzen2 or xmobar. |
| `i3exit`  | A easy to do `shutdown`, `reboot`, `lock` in i3 environment. |


</br>

- Let `startx` auto run `i3`

   `vim ~/.xinitrc` with the following settings:

    ```bash
    /usr/local/bin/i3
    ```

    `chmod +x ~/.xinitrc`


    Re-login again, then `startx` :)

</br>

- How to run some scripts or programms when **`i3`** reload?

    Add the setting below to your `~/.config/i3/config`

    ```bash
    # Run the command without delay
    exec_always YOUR_COMMAND_HERE

    # Sleep 1 second then run the command
    exec_always sleep 1; YOUR_COMMAND_HERE
    ```
