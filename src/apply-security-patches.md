# Applying Security Patches

```bash
# Only fetch the patches and list it, it won't apply update.
freebsd-update fetch

# After you review (if needed), then run this command to update.
freebsd-update install
```

If the update applies any kernel patches, the system will need a reboot in order
to boot into the patched kernel. If the patch was applied to any running binaries,
the affected applications should be restarted so that the patched version of the 
binary is used.

So how to check whether need to reboot or not:

```bash
freebsd-version -k
# 12.2-RELEASE-p1

uname -r
# 12.2-RELEASE
```

If the result is different (e.g the above case), then you need to reboot.

</br>

If anything wrong after update, you can rollback easy like below:

```bash
freebsd-update rollback
```
