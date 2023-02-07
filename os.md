# Multiple Operating Systems Installation



## Dual-Booting Setting

### Adjust the order of the boot

```sh
cd /etc/grub.d
# Swap the order of windows and ubuntu(Priority promotion)
sudo mv 30_os-prober 06__os-prober
# Hide ubuntu's advanced options
sudo chmod -x 20_memtest86+
```

### Adjust the default boot

```sh
sudo vim /etc/default/grub
# Modify existing ones directly, and add a line if not
GRUB_DEFAULT=saved # or just change the order=> GRUB_DEFAULT=0
GRUB_SAVEDEFAULT=true
# and then Update grub configuration
sudo update-grub
```



## Note

- installed in a single hard drive or more?

There may be some differences between the two approaches.

