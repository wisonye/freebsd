# About screen brightness

After you install `xorg`, the `backlight` util should be installed. So, you
can run `backlight +` to increase the screen brightness, and run `backlight -`
to decrease the screen brightness.

Also, you can set the keybinding in `i3` like below:

```bash
# ===========================================================================
# Screen brightness control
# ===========================================================================
bindcode 67 exec --no-startup-id backlight -
bindcode 68 exec --no-startup-id backlight +
```

But make sure change `67` and `68` to your keyboard key code, you can run `xev`
to print out the key code if you don't sure about that.

