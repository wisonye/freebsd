# Troubleshooting

- `X` can't start

    After you installed `Xorg` and you can start the `X` by 
    running `startx`.

    But if you saw something like below:

    ```bash
    Fatal server error:
    (EE) no screens found(EE)
    (EE)
    Please consult the The X.Org Foundation support
                at http://wiki.x.org
     for help.
    (EE) Please also check the log file at "/var/log/Xorg.0.log" 
    for additional information.
    (EE)
    (EE) Server terminated withe error (1). Closing log file.
    xinit: giving up
    xinit: unable to connect to X server: Connection refused
    xinit: server error
    ```

    That means you got a wrong configuration or missing driver,
    plz check the `/var/log/Xorg.0.log` to figure out what the error there.

</br>

- Boot fail or freeze

    If you put the wrong module in `/etc/rc.conf`, sometimes 
    it can't boot or the boot process is freezing, no any
    response when pressing any key.

    If that happens, you can follow the steps below to solve
    it out:

    In the boot menu UI, just press any arrow key (or another
    key NOT match the default shortcut) to exit the menu, then 
    you got the `Ok` prompt. You can press `?` to see supported
    command.

    So the first try should be disable the module you doubt,
    how to do that?

    ```bash
    # For example, the `/boot/modules/amdgpu.ko` is the possible
    # wrong module you add to `/etc/rc.conf`.
    # The setting below can avoid to load that module.
    set module_blacklist="/boot/modules/amdgpu.ko"
    ```

    Show it to confirm

    ```bash
    show module_blacklist
    ```
    
    Then reboot.

    In the boot menu UI, press `7` for the option, and press `5`
    to turn on the `Verbose`, and then press `Enter` to boot.

    If you can login, then fix the wrong configuration and reboot.

