# Install X implementation

The **`X`** Window System (**`X11`**, or simply **`X`**) is a windowing system for bitmap displays, 
common on Unix-like operating systems. It provides the basic framework for a GUI environment:

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

    If you don't know the name, then just type `sudo pkg instal xf86-video-` and press `tab`
    key, it will list all possible missing part.

</br>

Now, let's install `X` window implementation in the next chapter.

<hr>

After you installed `Xorg` and you can start the `X` by running `startx`.

But if you saw something like below:

```bash
Fatal server error:
(EE) no screens found(EE)
(EE)
Please consult the The X.Org Foundation support
            at http://wiki.x.org
 for help.
(EE) Please also check the log file at "/var/log/Xorg.0.log" for additional information.
(EE)
(EE) Server terminated withe error (1). Closing log file.
xinit: giving up
xinit: unable to connect to X server: Connection refused
xinit: server error
```

That means you got a wrong configuration or missing driver, plz check the `/var/log/Xorg.0.log`
to figure out what the error there.

By default, manual configuration is usually not necessary. Please do not manually create configuration
files unless **autoconfiguration** does not work.
For my case, I'm using `FreeBSD` in `2019 iMac 5K` which with an `AMD Radeon Pro 570X` GPU, so I first 
tried to apply the following setting based on the official handbook about [`Xorg Configuration`](https://www.freebsd.org/doc/handbook/x-config.html)
section:

`vim /usr/local/etc/X11/xorg.conf.d/driver-radeon.conf`

```bash
Section "Device"
    Identifier "Card0"
    Driver     "radeon"
EndSection
```

After that, reboot and `startx`, still not work, then I checked the `/var/log/Xorg.0.log` and I found
this:

```bash
(II) LoadModule: "radeon"
(WW) Warning, couldn't open module radeon
(EE) Failed to load module "radeon" (module does not exist, 0)
(EE) No driver available.
(EE)
Fatal server error
```

So, that's very clear, I didn't install the correct **`GPU`** driver!!! How to fix it?

```bash
sudo pkg install xf86-video-admgpu drm-kmod
```

**Then the boot process is halt!!!!**

**Then the boot process is halt!!!!**

- Exit the boot menu

    In the boot menu UI, just press any arrow key (or another key NOT match the default shortcut) to exit
    the menu, then you got the `Ok` prompt. You can press `?` to see supported command.

    As boot process ONLY halt after adding the below setting to `/etc/rc.conf`:

    ```bash
    kld_list="/boot/modules/amdgpu.ko"
    ```

    So the first try should be disable that module, how to do that?

    ```bash
    set module_blacklist="/boot/modules/amdgpu.ko"
    ```

    Show it to confirm

    ```bash
    show module_blacklist
    ```
    
    Reboot, then press `7` for the option, and press `5` to turn on the `Verbose`, and then press `Enter` to boot.

**Then the boot process is halt!!!!**

Full version package list:

```bash
	appres: 1.0.5
	bitmap: 1.0.9
	dejavu: 2.37_1
	encodings: 1.0.5,1
	evdev-proto: 5.8
	expat: 2.2.8
	font-adobe-100dpi: 1.0.3_4
	font-adobe-75dpi: 1.0.3_4
	font-adobe-utopia-100dpi: 1.0.4_4
	font-adobe-utopia-75dpi: 1.0.4_4
	font-adobe-utopia-type1: 1.0.4_4
	font-alias: 1.0.4
	font-arabic-misc: 1.0.3_4
	font-bh-100dpi: 1.0.3_4
	font-bh-75dpi: 1.0.3_4
	font-bh-lucidatypewriter-100dpi: 1.0.3_4
	font-bh-lucidatypewriter-75dpi: 1.0.3_4
	font-bh-ttf: 1.0.3_4
	font-bh-type1: 1.0.3_4
	font-bitstream-100dpi: 1.0.3_4
	font-bitstream-75dpi: 1.0.3_4
	font-bitstream-type1: 1.0.3_4
	font-cronyx-cyrillic: 1.0.3_4
	font-cursor-misc: 1.0.3_4
	font-daewoo-misc: 1.0.3_4
	font-dec-misc: 1.0.3_4
	font-ibm-type1: 1.0.3_4
	font-isas-misc: 1.0.3_4
	font-jis-misc: 1.0.3_4
	font-micro-misc: 1.0.3_4
	font-misc-cyrillic: 1.0.3_4
	font-misc-ethiopic: 1.0.4
	font-misc-meltho: 1.0.3_4
	font-misc-misc: 1.1.2_4
	font-mutt-misc: 1.0.3_4
	font-schumacher-misc: 1.1.2_4
	font-screen-cyrillic: 1.0.4_4
	font-sony-misc: 1.0.3_4
	font-sun-misc: 1.0.3_4
	font-winitzki-cyrillic: 1.0.3_4
	font-xfree86-type1: 1.0.4_4
	fontconfig: 2.13.92_2,1
	freetype2: 2.10.4
	glib: 2.66.0_2,1
	iceauth: 1.0.8_2
	libFS: 1.0.8
	libICE: 1.0.10,1
	libSM: 1.2.3,1
	libX11: 1.6.12,1
	libXScrnSaver: 1.2.3_2
	libXau: 1.0.9
	libXaw: 1.0.13_3,2
	libXcomposite: 0.4.5,1
	libXcursor: 1.2.0
	libXdamage: 1.1.5
	libXdmcp: 1.1.3
	libXext: 1.3.4,1
	libXfixes: 5.0.3_2
	libXfont: 1.5.4_2,2
	libXfont2: 2.0.4
	libXft: 2.3.3
	libXi: 1.7.10,1
	libXinerama: 1.1.4_2,1
	libXmu: 1.1.3,1
	libXpm: 3.5.13
	libXrandr: 1.5.2
	libXrender: 0.9.10_2
	libXres: 1.2.0_2
	libXt: 1.2.0,1
	libXtst: 1.2.3_2
	libXv: 1.0.11_2,1
	libXvMC: 1.0.12
	libXxf86dga: 1.1.5
	libXxf86vm: 1.1.4_3
	libdmx: 1.1.4_2
	libdrm: 2.4.102,1
	libedit: 3.1.20191231,1
	libepoll-shim: 0.0.20200602
	libepoxy: 1.5.4
	libevdev: 1.9.1.20200928
	libffi: 3.3_1
	libfontenc: 1.1.4
	libgudev: 234
	libiconv: 1.16
	libinput: 1.16.1
	libmtdev: 1.1.6
	libpciaccess: 0.16
	libpthread-stubs: 0.4
	libudev-devd: 0.4.2_1
	libunwind: 20200331_1
	libwacom: 1.5
	libxcb: 1.14_1
	libxkbfile: 1.1.0
	libxml2: 2.9.10_1
	libxshmfence: 1.3
	llvm80: 8.0.1_4
	mesa-dri: 19.0.8_9
	mesa-libs: 19.0.8_3
	mkfontscale: 1.2.1
	pciids: 20200819
	pcre: 8.44
	perl5: 5.32.0
	pixman: 0.40.0_1
	png: 1.6.37
	py37-evdev: 1.3.0
	py37-pyudev: 0.22.0
	py37-setuptools: 44.0.0
	py37-six: 1.15.0
	python37: 3.7.9
	readline: 8.0.4
	sessreg: 1.1.2
	setxkbmap: 1.3.2
	smproxy: 1.0.6
	twm: 1.0.11
	wayland: 1.18.0_4
	x11perf: 1.6.1
	xauth: 1.1
	xbacklight: 1.2.3
	xbitmaps: 1.1.2
	xcalc: 1.1.0
	xcb-util: 0.4.0_2,1
	xcb-util-wm: 0.4.1_3
	xclock: 1.0.9
	xcmsdb: 1.0.5
	xconsole: 1.0.7_1
	xcursor-themes: 1.0.6
	xcursorgen: 1.0.7
	xdpyinfo: 1.3.2_3
	xdriinfo: 1.0.6_3
	xev: 1.2.4
	xf86-input-keyboard: 1.9.0_4
	xf86-input-libinput: 0.30.0_1
	xf86-input-mouse: 1.9.3_3
	xf86-video-scfb: 0.0.5_2
	xf86-video-vesa: 2.5.0
	xf86dga: 1.0.3_1
	xgamma: 1.0.6
	xgc: 1.0.5
	xhost: 1.0.8
	xinit: 1.4.1,1
	xinput: 1.6.3
	xkbcomp: 1.4.3
	xkbevd: 1.1.4
	xkbutils: 1.0.4_2
	xkeyboard-config: 2.30
	xkill: 1.0.5
	xlsatoms: 1.1.3
	xlsclients: 1.1.4
	xmessage: 1.0.5
	xmodmap: 1.0.10
	xorg: 7.7_3
	xorg-apps: 7.7_4
	xorg-docs: 1.7.1,1
	xorg-drivers: 7.7_6
	xorg-fonts: 7.7_1
	xorg-fonts-100dpi: 7.7
	xorg-fonts-75dpi: 7.7
	xorg-fonts-cyrillic: 7.7
	xorg-fonts-miscbitmaps: 7.7
	xorg-fonts-truetype: 7.7_1
	xorg-fonts-type1: 7.7
	xorg-libraries: 7.7_4
	xorg-server: 1.20.9_1,1
	xorgproto: 2020.1
	xpr: 1.0.5
	xprop: 1.2.4
	xrandr: 1.5.1
	xrdb: 1.2.0
	xrefresh: 1.0.6
	xset: 1.2.4_3
	xsetroot: 1.1.2
	xterm: 360
	xtrans: 1.4.0
	xvinfo: 1.1.4
	xwd: 1.0.7
	xwininfo: 1.1.5
	xwud: 1.0.5
```
