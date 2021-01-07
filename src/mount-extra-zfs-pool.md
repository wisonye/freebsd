# Mount extra zfs pool

For example, you make the wrong configuration to your **`FreeBSD`** (`ZFS`) 
accidentally, maybe you delete the entire /boot folder which not possible 
to reboot and fix in that case. 

So, you need another **`FreeBSD`** to boot and accept your original `ZFS`
pool to fix it.

1. Boot into the **`FreeBSD`** live CD/USB

</br>

2. Run this command to get the name of your `zpool`

    If your **`FreeBSD`** is installed in another USB, then plug it in right now.

    ```bash
    # It prints the possible importable zpool name
    # For example, `zroot`
    zpool import
    ```

</br>

3. Create a temporary mount folder for the `zpool` you want to mount into

    ```bash
    mkdir -p /tmp/zroot
    ```

</br>

4. Import your **`FreeBSD`** original `zpool` and mount to that folder

    ```bash
    # For example, your zpool name is `zroot`
    zpool import -fR /tmp/zroot zroot
    ```

5. Create another mount folder for any `zfs Data set` you want to mount and fix:

    For example, you want to mount the `/` (system root folder in your **`FreeBSD`**),
    then it should located in `zroot/ROOT/default`

    ```bash
    mkdir /tmp/my-root

    mount -t zfs zroot/ROOT/default /tmp/my-root
    ```

    So go to `/tmp/my-root` to fix your problem, or maybe copy the missing files from 
    anothe `zfs snapshot hidden folder`, etc.

</br>

6. Export the `zpool` after you done

    ```bash
    umount /tmp/my-root

    zpool export zroot
    ```

    Then reboot and try:)
