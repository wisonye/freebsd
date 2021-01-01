# Fix GPU driver issue

Before install `X`, you better to fix the GPU issue first:


The easy way to solve GPU driver issue:

```bash
cd /usr/ports/graphics/drm-kmod
sudo make install clean
```

</br>

After compilation done, you should be able to the tips like below:

```bash
For amdgpu and radeonkms. there have been reports of issues when using UEFI
firmware boot. You might need to disable the console by adding
hw.syscons.disable=1 to /boot/loader.conf. Please note that this will
disable the console until the graphic driver is loaded.

For amdgpu: kld_list="amdgpu"
For Intel: kld_list="/boot/modules/i915kms.ko"
For radeonkms: kld_list="/boot/modules/radeonkms.ko"
```

First, `sudo vim /etc/rc.conf` and add the following settings:

```bash
# Load AMD GPU module
kld_list="amdgpu"
```

Second, `sudo vim /boot/loader.conf` and add the following settings:

```bash
# Disable the console until GPU driver is loaded.
hw.syscons.disable=1
```

Finally, add users into the `video` group:

```bash
sudo pw groupmod video -m root
sudo pw groupmod video -m YOUR_UESR_NAME_HERE
```

Reboot.

</br>

Pay attention:

_From now on, the reboot UI will look like freeze at some point, as the console be disabled before the GPU driver is loaded._

