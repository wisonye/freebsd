# Fix rust

When you install `rust` in **`FreeBSD`**, you will see the error below:

```bash
error: error: 'sysinfo not supported on this platform'
```

But it seems doesn't broken, `rustc` still work. The side-effect 
I found is that: When using `cargo watch`, it needs a few seconds delay
to detect the file change!!!


### About `rust-analyzer`

There is no release executable for **`FreeBSD`**, so you have to
compile it by yourself:

```bash
git clone https://github.com/rust-analyzer/rust-analyzer.git
cd rust-analyzer/
cargo xtask install --server
```

If you use `Coc`, make sure you change the settings below to `:CocConfig`:

```bash
"rust-analyzer.serverPath": "/home/YOUE_USERNAME_HERE/rust-analyzer",
```

Pay attention that: 

`rust-analyzer.serverPath` only accept the full path setting,
so if you put `$HOME/.cargo/bin/rust-analyzer` there, it won't work!!!

</br>

Also, maybe you should disable the auto update. Otherwise, the `coc-rust-analyzer`kk
will keep asking you every time you open `.rs` file:

```bash
"coc.preferences.extensionUpdateCheck": "never",
```

</br>
