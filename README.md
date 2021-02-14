# Creating a miner with NUC8i7HxK RX Vega M

## Windows
Just works with SW such as nanominer, as the device is recognized as OpenCL compute immediately

### HNK / Vega M GL
HNK/GL Gfx = 3MH/s average on ETH @ 45W
- This tends to work with ETH even though less than 4GB is available on the card, for what I assume is memory architecture detail in the Win driver or HW. It will most likely stop working in the future as DAG increases
TODO - RVN, etc

### HVK / Vega M GH
TODO

## Ubuntu

### HVK / Vega M GH
ETH mining does not work natively as in Windows. Using zombie mode, the terrible 140H/s rate at 60W should never be used
RVN = 7.3MH/s average @ 60W (60-75C temps : Should enable aggresive fan modes in BIOS)

Tuning power settings doesn't seem to be supported via AMD/rocm drivers

**DO NOT INSTALL amdgpu-pro drivers**

*Only compatible with Kernel 5.4.0-xx*

Install rocm [https://github.com/RadeonOpenCompute/ROCm] with the opencl/rocminfo packages (don't need dkms)

**Fix missing dependency for rocm4.0** [https://github.com/RadeonOpenCompute/ROCm/issues/1324]

sudo apt install libtinfo5

Add lines to /etc/ld.so.conf.d/hsa-rocr-dev.conf

>
 /opt/rocm-4.0.0/hsa/lib
 /opt/rocm-4.0.0/lib
 /opt/rocm-4.0.0/opencl/lib
>
run ldconfig to get new link paths

- add user to video group
- add user to render group

Device should be available in rocminfo and clinfo
