# pkg

    Using `pkg` for binary package management


- Install `pkg`

   If you don't have `pkg` in some cases, then you can install it via `port`:

   ```bash
   # Switch `root`
   cd /usr/ports/ports-mgmt/pkg
   make
   make install clean
   ```

</br>

- Update package

    By default, `pkg` uses the closest mirror automatic, the config file located at
    **`/etc/pkg/FreeBSD.conf`**

    Update the repo metadata:

    ```bash
    pkg update -f

    # The package management tool is not yet installed on your system.
    # Do you want to fetch and install it now? [y/N]: y
    ```

    For the first time you run `pkg` (before you install `sudo`), you need to change to
    `root` user for doing that.

</br>

- Common usage

    ```bash
    # `PACKAGE_NAME` below can be just the name or with the version!!!

    # Search package by name
    pkg search PACKAGE_NAME

    # Install package by name
    pkg install PACKAGE_NAME

    # Query package info by name
    pkg info PACKAGE_NAME

    # Remove package by name
    pkg delete PACKAGE_NAME
    ```

</br>

- Upgrade all install packages

    ```bash
    pkg upgrade
    ```

</br>

- Clean

    ```bash
    # Auto remove unused packages
    pkg autoremove

    # Clean the entire cache which located at `/var/cache/pkg` by default
    pkg clean -a
    ```

</br>

