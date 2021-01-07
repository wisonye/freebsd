# X can't start

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

