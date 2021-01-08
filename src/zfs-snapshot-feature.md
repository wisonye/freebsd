# snapshot feature

A `snapshot` provides a read-only, point-in-time copy of the `dataset`. 

With the `Copy-On-Write (COW)` behavior, snapshots can be created super fast,
as it doesn't need to clone the entire `dataset`.

- Creating snapshots

    Create a snapshot on `zroot` dataset and all its children (what the `-r` flag does).

    Snapshot name is `2021-01-08`

    ```bash
    sudo zfs snapshot -r zroot@2021-01-08
    ```

    For the name of the snapshot, you can name it to any one you wanted, for example:

    ```bash
    # sudo zfs snapshot -r zroot@clean-install
    # sudo zfs snapshot -r zroot@x-and-i3-done
    # sudo zfs snapshot -r zroot@dev-environment-is-ready
    ```

    After creating `zroot@2021-01-08`, you can run the command below to view 
    all snapshots with that name:

    ```bash
    zfs list -t snapshot | grep 2021-01-08

    # zroot@2021-01-08                   0B      -       96K  -
    # zroot/ROOT@2021-01-08              0B      -       96K  -
    # zroot/ROOT/default@2021-01-08    144K      -     2.65G  -
    # zroot/tmp@2021-01-08              80K      -      112K  -
    # zroot/usr@2021-01-08               0B      -       96K  -
    # zroot/usr/home@2021-01-08       16.6M      -     1.70G  -
    # zroot/usr/ports@2021-01-08         0B      -      749M  -
    # zroot/usr/src@2021-01-08           0B      -      688M  -
    # zroot/var@2021-01-08               0B      -       96K  -
    # zroot/var/audit@2021-01-08         0B      -       96K  -
    # zroot/var/crash@2021-01-08         0B      -       96K  -
    # zroot/var/log@2021-01-08          72K      -      388K  -
    # zroot/var/mail@2021-01-08          0B      -      128K  -
    # zroot/var/tmp@2021-01-08           0B      -       96K  -
    ```

</br>

- Compare 2 snapshots

    You can compare any 2 snapshots at any given time, it works like `git diff`.

    If you want to know the entire different, then you should compare the 
    `POOL_NAME/ROOT/default@SNAPSHOT_NAME`, as usually the `POOL_NAME/ROOT/default`
    dataset is mounted to `/`. You compare that dataset snapshot, you will get
    all the `sub dataset` different as the result.

    ```bash
    # For example, `zroot` is the pool name.
    # Compare the particular snapshot with the `latest` snaphot
    sudo zfs diff zroot/ROOT/default@2021-01-08

    # Compare 2 specified snapshots
    sudo zfs diff zroot/ROOT/default@2021-01-08 zroot/ROOT/default@2021-01-08-v2



    # Save the compare result to a file
    sudo zfs diff zroot/ROOT/default@2021-01-08 zroot/ROOT/default@2021-01-08-v2 > ~/temp/snapshot-diff.txt
    ```

    In the result, you will see 4 different symbols like below:

    ```bash
    +	The path or file was added.
    -	The path or file was deleted.
    M	The path or file was modified.
    R	The path or file was renamed.
    ```

</br>

- Rollback snapshots

    For rolling back a snapshot is just as easy as typing `zfs rollback snapshotname`. 

    Rolling back to a specified snapshot can be super fast, or take sometimes, it totally
    depends on how many changes are involved. During that time, the dataset always remains
    in a consistent state, much like a database that conforms to ACID principles is performing
    a rollback. This is happening while the dataset is live and accessible without requiring 
    a downtime.

    Once the snapshot has been rolled back, the dataset has the same state as it had 
    when the snapshot was originally taken. All other data in that dataset that was 
    not part of the snapshot is discarded!!!

    Before you roll back to a snapshot, it's always an good idea by taking the current snapshot,
    then you can "go back" (or get back some files) when needed.

    For demonstrate rolling back, let's create some test snapshots for that.

    - Create `test1` to all exists datasets and take a snapshot `2021-01-08-test-v1`

        ```bash
        # Change to `root` for creating test files easier
        su

        # Create `test1` to all datasets
        echo "test1" > /test1
        echo "test1" > /tmp/test1
        echo "test1" > /usr/test1
        echo "test1" > /usr/home/test1
        echo "test1" > /usr/ports/test1
        echo "test1" > /usr/src/test1
        echo "test1" > /var/test1
        echo "test1" > /var/audit/test1
        echo "test1" > /var/crash/test1
        echo "test1" > /var/log/test1
        echo "test1" > /var/mail/test1
        echo "test1" > /var/tmp/test1

        # You can confirm that by running
        ls -lht /test*
        ls -lht /tmp/test*
        ls -lht /usr/home/test*
        ls -lht /usr/ports/test*
        ls -lht /var/test*
        ls -lht /var/audit/test*
        ls -lht /var/crash/test*
        ls -lht /var/log/test*
        ls -lht /var/mail/test*
        ls -lht /var/tmp/test*

        # Create snapshot
        zfs snapshot -r zroot@2021-01-08-test-v1
        ```

    - Create `test2` to all exists datasets and take a snapshot `2021-01-08-test-v2`

        ```bash
        echo "test2" > /test2
        echo "test2" > /tmp/test2
        echo "test2" > /usr/test2
        echo "test2" > /usr/home/test2
        echo "test2" > /usr/ports/test2
        echo "test2" > /usr/src/test2
        echo "test2" > /var/test2
        echo "test2" > /var/audit/test2
        echo "test2" > /var/crash/test2
        echo "test2" > /var/log/test2
        echo "test2" > /var/mail/test2
        echo "test2" > /var/tmp/test2

        # Create snapshot
        zfs snapshot -r zroot@2021-01-08-test-v2
        ```

    - Create `test3` to all exists datasets and take a snapshot `2021-01-08-test-v3`

        ```bash
        echo "test3" > /test3
        echo "test3" > /tmp/test3
        echo "test3" > /usr/test3
        echo "test3" > /usr/home/test3
        echo "test3" > /usr/ports/test3
        echo "test3" > /usr/src/test3
        echo "test3" > /var/test3
        echo "test3" > /var/audit/test3
        echo "test3" > /var/crash/test3
        echo "test3" > /var/log/test3
        echo "test3" > /var/mail/test3
        echo "test3" > /var/tmp/test3

        # Create snapshot
        zfs snapshot -r zroot@2021-01-08-test-v3
        ```
    </br>

    Now, let's list all snapshots you just created:

    ```bash
    zfs list -t snapshot | grep 2021-01-08-test
    ```

    - Create `test4` and roll back to the `zroot@2021-01-08-test-v3`

        ```bash
        echo "test4" > /test4
        echo "test4" > /tmp/test4
        echo "test4" > /usr/test4
        echo "test4" > /usr/home/test4
        echo "test4" > /usr/ports/test4
        echo "test4" > /usr/src/test4
        echo "test4" > /var/test4
        echo "test4" > /var/audit/test4
        echo "test4" > /var/crash/test4
        echo "test4" > /var/log/test4
        echo "test4" > /var/mail/test4
        echo "test4" > /var/tmp/test4
        ```

        Now, all datasets should have the `test4` file in each mounted 
        folder. You can confirm that by running:

        ```bash
        ls -lht /test*
        ls -lht /tmp/test*
        ls -lht /usr/home/test*
        ls -lht /usr/ports/test*
        ls -lht /var/test*
        ls -lht /var/audit/test*
        ls -lht /var/crash/test*
        ls -lht /var/log/test*
        ls -lht /var/mail/test*
        ls -lht /var/tmp/test*

        # Should print out a lot of which `xxx` and `yyy` are the mounted 
        # folder
        /xxx/yyy/test4
        /xxx/yyy/test3
        /xxx/yyy/test2
        /xxx/yyy/test1
        ```

        Let's rollback:

        ```bash
        zfs rollback zroot@2021-01-08-test-v3
        ```
</br>

ll /usr/home/.zfs/snapshot/
total 4
drwxr-xr-x  3 root  wheel     3B Jan  6 08:42 2021-01-08/
drwxr-xr-x  3 root  wheel     4B Jan  8 17:34 2021-01-08-test-v1/
drwxr-xr-x  3 root  wheel     5B Jan  8 17:53 2021-01-08-test-v2/
drwxr-xr-x  3 root  wheel     6B Jan  8 17:58 2021-01-08-test-v3/
drwxr-xr-x  3 root  wheel     3B Jan  6 08:42 2021-01-08-v2/
drwxr-xr-x  3 root  wheel     3B Jan  6 08:42 all_ready/
drwxr-xr-x  3 root  wheel     3B Jan  6 08:42 i3_done/

ll /.zfs/snapshot/
total 60
drwxr-xr-x  19 root  wheel    25B Jan  8 14:22 2021-01-08/
drwxr-xr-x  19 root  wheel    26B Jan  8 17:33 2021-01-08-test-v1/
drwxr-xr-x  19 root  wheel    27B Jan  8 17:53 2021-01-08-test-v2/
drwxr-xr-x  19 root  wheel    28B Jan  8 17:58 2021-01-08-test-v3/
drwxr-xr-x  19 root  wheel    25B Jan  8 16:58 2021-01-08-v2/
drwxr-xr-x  19 root  wheel    25B Jan  6 11:52 all_ready/
drwxr-xr-x  19 root  wheel    25B Jan  6 10:48 i3_done/

</br>

- Delete the older snapshots

    ```bash

    ```
