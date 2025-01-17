#+TITLE: Yocto project examples(builds for Raspberry Pi3B/Pi3B+/Pi4B)
#+DESCRIPTION: Yocto project examples

Examples of [[https://www.yoctoproject.org][Yocto]]

* Installation

** Install OS dependencies

[[https://www.yoctoproject.org/docs/3.0.2/mega-manual/mega-manual.html#required-packages-for-the-build-host][Required Packages for the Build Host]]

** Set environment

[[https://www.yoctoproject.org/docs/3.0.2/mega-manual/mega-manual.html#user-configuration][User Configuration]]

*** For example, my bash configuration:
#+begin_src shell-script
# Build settings
export BITBAKE_COMMON_DIR="$HOME/.bitbake"
export DL_DIR="$BITBAKE_COMMON_DIR/downloads"
export SSTATE_DIR="$BITBAKE_COMMON_DIR/sstate-cache"

# Export name:
export BB_ENV_EXTRAWHITE="$BB_ENV_EXTRAWHITE BITBAKE_COMMON_DIR"
export BB_HASHBASE_WHITELIST="TMPDIR FILE PATH PWD BB_TASKHASH BBPATH DL_DIR \
SSTATE_DIR THISDIR FILESEXTRAPATHS FILE_DIRNAME HOME LOGNAME SHELL TERM \
USER FILESPATH STAGING_DIR_HOST STAGING_DIR_TARGET COREBASE PRSERV_HOST \
PRSERV_DUMPDIR PRSERV_DUMPFILE PRSERV_LOCKDOWN PARALLEL_MAKE \
CCACHE_DIR EXTERNAL_TOOLCHAIN CCACHE CCACHE_DISABLE LICENSE_PATH SDKPKGSUFFIX"
#+end_src

** Install example-yocto

To download 'example-yocto' project and dependencies:

#+begin_src shell-script
# Download example-yocto
git clone https://github.com/yuravg/example-yocto.git
cd example-yocto
# Download Poky and layers
git submodule init
git submodule update --force
#+end_src

* Doc
[[https://www.yoctoproject.org/docs/3.0.2/mega-manual/mega-manual.html][Yocto Project Mega-Manual]]

* Examples

- [[./01_min/README.org][01_min]] - minimal Raspberry Pi3 (RPi3B/RPi3B+) configuration.
- [[./02_uboot/README.org][02_uboot]] - use u-boot RPi3B/RPi3B+
- [[./03_ssh/README.org][03_ssh]] - use sshd RPi3B/RPi3B+
- [[./04_middle/README.org][04_middle]] - RPi3B/RPi3B+, use sshd, systemd, profile
- [[./04_middle_rpi4b/README.org][04_middle_rpi4b]] - RPI4B, use sshd, systemd, profile

TODO: add examples: custom_kernel, remote boot, linaro, wifi, use ssh keys, quemu

** Build example

- [[#install-example-yocto][Install example-yocto]]
- set environment
- set layers
- run building

#+begin_src shell-script
# set environment (from directory: example-yocto)
source poky/oe-init-build-env <example_dir_name>
# set layers (from directory: <example_dir_name>)
make layers
# run building
make base
# or: make minimal
#+end_src

** Add example

- [[#install-example-yocto][Install example-yocto]]
- set environment

#+begin_src shell-script
# set environment (from directory: example-yocto)
source poky/oe-init-build-env <example_dir_name>
#+end_src

* Notes
** Links
- http://git.yoctoproject.org/clean/cgit.cgi/
- https://wiki.yoctoproject.org/wiki/Releases
- http://downloads.yoctoproject.org/releases/yocto/
- https://git.yoctoproject.org/cgit.cgi/meta-raspberrypi/about/
- https://raspinterest.wordpress.com/2016/11/30/yocto-project-on-raspberry-pi-3/
- https://github.com/WebPlatformForEmbedded/meta-wpe/wiki/Raspberry-PI
- https://meta-raspberrypi.readthedocs.io/en/latest
- https://himvis.com/
- https://www.cnx-software.com/2013/07/05/12mb-minimal-image-for-raspberry-pi-using-the-yocto-project/
- https://www.lynxbee.com/category/build-frameworks/yocto-bitbake-openembedded/

*** Creating Your Own General Layer
[[https://www.yoctoproject.org/docs/3.0.2/mega-manual/mega-manual.html#creating-your-own-general-layer][Creating Your Own General Layer]]
#+begin_src shell-script
# create layer
bitbake-layers create-layer <path>/meta-mylayer
#+end_src

*** Devtool

[[https://www.yoctoproject.org/docs/current/sdk-manual/sdk-manual.html#using-devtool-in-your-sdk-workflow][Devtool workflow]]
[[https://www.youtube.com/watch?v=CiD7rB35CRE][Using Devtool to Streamline Your Yocto Project Workflow - Tim Orling, Intel]]

**** Add recipes
***** 'Hello word' from GNU.org
#+begin_src shell-script
devtool create-workspace workspace
devtool add https://ftp.gnu.org/gnu/hello/hello-2.10.tar.gz
#+end_src
