# WIFI configuration

- Install correct WIFI NIC driver module for `Boardcom` series (e.g. `Apple iMac`, `Apple MBP`)

    ```bash
    cd /usr/ports/net/bwn-firmware-kmod
    sudo make install clean
    ```

    `sudo vim /etc/rc.conf` with the following setting:

    ```bash
    # Load Broadcom BCM43xx SoftMAC IEEE 802.11 wireless network driver
    if_bwn_load="YES"
    ```

</br>

- Another non-supported NIC driver
    
    If you've already tried install your customzied wireless driver, but still can't see in `ifconfig`
    result, then you should try the last step: 
    [`Using Windows® NDIS Drivers`](https://www.freebsd.org/doc/handbook/config-network-setup.html)
