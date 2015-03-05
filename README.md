# Monkey + Yocto Project

This repository is a fork of the official recipes to build Monkey on [Yocto Project](https://www.yoctoproject.org/).

I only created a minimal yocto layer and moved the recipes from the official repository into it so I don't have to move stuff around as suggested but instead just add this repository in conf/bblayers.conf.


## Getting Started

The following instructions assumes that your are building [Yocto](https://www.yoctoproject.org/) images from scratch using the [Poky](https://www.yoctoproject.org/tools-resources/projects/poky) tool, the first step is to get a copy of the [Monkey-Yocto](https://github.com/monkey/monkey-yocto) repository in your local computer:

```Shell
$ git clone https://github.com/monkey/monkey-yocto
```

then reference the __monkey-yocto/monkey__ directory in your build directory's __conf/bblayers.conf__ file:

```
BBLAYERS ?= " \
  ~/git/poky/meta \
  ~/git/poky/meta-yocto \
  ~/git/poky/meta-yocto-bsp \
  ~/git/monkey-yocto/meta-monkey \
  "
```

> make sure you are using the right Poky path

Once there, go into the __build/__ directory and make a test building Monkey:

```Shell
$ cd poky/build/
$ bitbake monkey
```

If it built fine, you should see an output similar to this:

```
Build Configuration:
BB_VERSION        = "1.22.0"
BUILD_SYS         = "x86_64-linux"
NATIVELSBSTRING   = "Ubuntu-14.04"
TARGET_SYS        = "i586-poky-linux"
MACHINE           = "qemux86"
DISTRO            = "poky"
DISTRO_VERSION    = "1.6"
TUNE_FEATURES     = "m32 i586"
TARGET_FPU        = ""
meta
meta-yocto
meta-yocto-bsp    = "monkey-daisy:98ad3cb2c0f5975a0df4cebc06775aaae657700d"

NOTE: Preparing runqueue
NOTE: Executing SetScene Tasks
NOTE: Executing RunQueue Tasks
NOTE: Tasks Summary: Attempted 391 tasks of which 391 didn't need to be rerun and all succeeded.
```

## Add Monkey to your Yocto Image

As any other extra package for your Image, the Build system needs to be aware that you want to include Monkey. For that purpose edit your __build/conf/local.conf__ configuration file and add the following line at bottom:

```
IMAGE_INSTALL_append = " monkey"
```

That line tells the Build system to include __monkey__ package when creating the final image. If for some reason the variable already exists, just append the __monkey__ package name at the end, e.g:

```
IMAGE_INSTALL_append = " package1 package2 monkey"
```

The next time you build your image, Monkey will be packaged into it.
