# change wallpaper

```bash
sudo pkg install feh
````

Download wallpaper you like and then `vim ~/.config/i3/config` with the following setting:

```js
exec_always feh --bg--file YOUR_WALLPAPER_FULL_PATH_FILE_NAME
```

Restart `i3` then you should be able to see the new wallpaper.
