Odin patch
==========

Adapted from the original patch here:

https://github.com/lalithsuresh/odin-driver-patches

Instructions
------------

Download your kernel sources (Ubuntu Trusty 14.04 kernel 3.13.0-39-generic)

```
  $: git clone git://kernel.ubuntu.com/ubuntu/linux.git
  $: git clone --reference linux git://kernel.ubuntu.com/ubuntu/ubuntu-trusty.git
```

Inspect the tags and find your current kernel version

```
  $: git tag -l Ubuntu-*
  $: git checkout -b my_kernel Ubuntu-3.13.0-39
```

Configure the kernel - i.e. Select the debugfs option for ath driver

```
  $: make menuconfig
  $: make -j5 (recommended at first)
```

NOTE: 5 = 1 + num_cores

After the whole kernel was compiled we can patch the debug.c file in path_kernel_src/drivers/net/wireless/ath/ath9k/

```
  $: patch < path_to_ath_patch/patch.patch
  $: make modules_prepare
  $: make modules SUBDIRS=drivers/net/wireless/ath
```

If it was built successfully:

$ rmmod ath9k_htc
$ rmmod ath9k_common
$ rmmod ath9k_hw
$ rmmod ath

$ insmod ath
$ insmod ath9k_hw
$ insmod ath9k_common
$ insmod ath9k_htc

Check info about a module

```
  $: modinfo MODULE
```