# Make your boot faster

By default, you need to wait for around **10** second before select the default boot option.

But we can change it in `/boot/loader.conf`.

`sudo vim /boot/loader.conf` to change some settings to reduce the timeout

```bash
# Loader settings
autoboot_delay="1"
```

Save and exit. 

Also, you can know more about the loader option in `/boot/defaults/loader.conf`.
But make sure DO NOT change in `/boot/defaults/loader.conf` directly, copy the
settings you wants and override them in `/boot/loader.conf`.

For example, you can change the loader logo with the setting below:

```bash
loader_logo="beastie"
```

Now, reboot to take effect.

</br>

