# Compress feature

Each `dataset` has a compression property, which defaults to off. This 
property can be set to one of a number of compression algorithms. This 
will cause all new data that is written to the `dataset` to be compressed.

Enable compression can reduce the space used, increase the read and write 
throughput, as because fewer blocks are read or written!!!

[Here](https://www.freebsd.org/doc/handbook/zfs-term.html#zfs-term-compression)
is the supported compress algorithms. As you can see, the new `LZ4` can 
often compress at over `500 MB/s`, and decompress at over `1.5 GB/s` (per single CPU core).

If you selected `ZFS` via the installation process, `compress=lz4` is enabled
by default.

Example:

```bash
# Create non-compressed and compressed dataset
sudo zfs create -o mountpoint=/usr/home/$USER/test zroot/test
sudo zfs create -o mountpoint=/usr/home/$USER/test-compressed -o compress=lz4 zroot/test-compressed

sudo chown $USER:$USER ~/test
sudo chown $USER:$USER ~/test-compressed
```

So, let's check the compress attribute for both datasets:

```bash
zfs get compress zroot/test-compressed
# NAME                   PROPERTY     VALUE           SOURCE
# zroot/test-compressed  compression  lz4             local

zfs get compress zroot/test
# NAME        PROPERTY     VALUE           SOURCE
# zroot/test  compression  lz4             inherited from zroot
```

</br>

The command below is used to query `How much space you're save`:

```bash
zfs get used,compressratio,compression,logicalused zroot/ROOT/default

# NAME                PROPERTY       VALUE           SOURCE
# zroot/ROOT/default  used           2.95G           -
# zroot/ROOT/default  compressratio  1.98x           -
# zroot/ROOT/default  compression    lz4             inherited from zroot
# zroot/ROOT/default  logicalused    5.45G
```
As you can see, the `zroot/ROOT/default` dataset saved almost half disk 
space by using the lz4, super nice:)
