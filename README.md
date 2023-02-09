# Custom kernel for native docker (cepheus)

### Based on https://gist.github.com/FreddieOliveira/efe850df7ff3951cb62d74bd770dce27#22-kernel

## Custom kernel compilation

To check the necessary features list, first install the [Termux app](https://github.com/termux/termux-app) in your phone.

Next, open Termux and download a script to check your kernel:

```
$ pkg install wget
$ wget https://raw.githubusercontent.com/moby/moby/master/contrib/check-config.sh
$ chmod +x check-config.sh
$ sed -i '1s_.*_#!/data/data/com.termux/files/usr/bin/bash_' check-config.sh
$ sudo ./check-config.sh
```

You can modify kernel configuration with config_modify.sh to make modifications to the defconfig files, but always create a basis and copy the differences manually with according to the modifications not replace the hall file because it won't work.

After run the build.sh file and flash it with TWRP.

### If controllers are missing

Create directories for each of the cgroup resources:

```
sudo mount -t tmpfs cgroup_root /sys/fs/cgroup
```

## Running docker

### Install

```
pkg install root-repo
pkg install docker
```

### Running

In one pane start dockerd:

```
$ sudo dockerd --iptables=false
```

And in others panes you can run the containers:

```
$ sudo docker run hello-world
```

To use this driver give the `--net=host --dns=8.8.8.8` flags when running a container.




