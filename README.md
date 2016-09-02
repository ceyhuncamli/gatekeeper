# Gatekeeper

## How to Set Up

### Install and Configure Dependencies

Install the following software dependencies:

    $ sudo apt-get update
    $ sudo apt-get -y -q install git clang doxygen hugepages build-essential linux-headers-`uname -r`

To use DPDK, make sure you have all of the environmental requirements: <http://dpdk.org/doc/guides/linux_gsg/sys_reqs.html#running-dpdk-applications>.

Note that DPDK requires the use of hugepages; instructions for mounting hugepages are available in the link above.

Once the software dependencies have been installed and the hugepages have been configured, you are ready to build `gatekeeper`.

### Obtain Source

Upon cloning the `gatekeeper` repository, change directory to the `dpdk` submodule and initialize it:

    $ cd dpdk
    $ git submodule init
    $ git submodule update

(Note: these initialization steps are not needed if you clone the `gatekeeper` repository using `git clone --recursive ...`.)

### Compile

While in the `gatekeeper` directory, run the setup script:

    $ sudo ./setup.sh

This script compiles DPDK and loads the needed kernel modules.

Once DPDK is compiled, `gatekeeper` can be compiled:

    $ make

### Configure Network Adapters

Before `gatekeeper` can be used, the network adapters must be bound to DPDK. For this, you can use the script `dpdk/tools/dpdk-devbind.py`. For example:

    $ sudo dpdk/tools/dpdk-devbind.py --bind=uio_pci_generic enp131s0f0

This command binds the interface `enp131s0f0` to the `uio_pci_generic` driver so that frames can be passed directly to DPDK instead of the kernel.

## How to Run

Once `gatekeeper` is compiled and the environment is configured correctly, run:

    $ sudo ./build/gatekeeper
