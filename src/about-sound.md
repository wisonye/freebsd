# About sound

By default, your sound card should work automatic after installed `xorg`.
You can run the command below to print the sound card status:

```bash
cat /dev/sndstat

# Installed devices:
# pcm0: <Cirrus Logic CS4206 (Internal Analog 3.1/2.0)> (play/rec) default
# pcm1: <Cirrus Logic CS4206 (Analog Headphones)> (play)
# pcm2: <Cirrus Logic CS4206 (Digital)> (play)
# No devices installed from userspace.
```

If it doesn't work for you, then you should follow this 
[Handbook tutorial](https://www.freebsd.org/doc/en_US.ISO8859-1/books/handbook/sound-setup.html)
to load the extra driver.


### How to control volume

- Install the packages below:

    ```bash
    sudo pkg install alsa-utils
    sudo pkg install pulseaudio
    ```

    From now on, you can run `alsamixer` to change your volum in terminal. 
    (Press `ESC` to exit `alsamixer`)

</br>

- For using `volume_up` and `volume_down` key to control volume:

    Add the settings below in `i3` configuration file:

    ```bash
    # ===========================================================================
    # Audio and volume control
    # ===========================================================================
    # Use pactl to adjust volume in PulseAudio.
    set $refresh_i3status killall -SIGUSR1 i3status
    bindcode 96 exec --no-startup-id pactl set-sink-volume @DEFAULT_SINK@ +5% && $refresh_i3status
    bindcode 95 exec --no-startup-id pactl set-sink-volume @DEFAULT_SINK@ -5% && $refresh_i3status
    bindcode 76 exec --no-startup-id pactl set-sink-mute @DEFAULT_SINK@ toggle && $refresh_i3status
    ```

    Restart `i3` to take effect.
    
</br>

- Troubleshooting

    In my peronsal case, the command `pactl set-sink-mute @DEFAULT_SINK@ toggle`
    doesn't work for me. Then I use `mixer vol mute` to mute, but when I run
    `mixer vol unmute`, it doesn't work, I have to press `volume_up` button many
    times to bring back the volume.

