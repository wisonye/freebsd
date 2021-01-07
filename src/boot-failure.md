# boot failure

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
