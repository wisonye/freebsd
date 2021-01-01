# Fix vim

In `Extra config after first boot` chapter, you've already installed `vim-tiny`, but that's the 
mini version which doesn't have full features (especially the `clipboard` feature). So you can 
install the full version to replace that:

```bash
sudo pkg install vim
```

</br>

If you want to use `coc` plugin, then you need to install `node` and `npm` as well. I highly recommend
you install the `12 LTS` version which can make `coc` more stable:

```bash
sudo pkg install nod12 npm-node12
```

</br>

Also, maybe you need:

```bash
sudo pkg install fzf ripgrep
```
