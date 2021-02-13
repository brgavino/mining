# mining

Creating a miner with NUC8i7HxK

Win10 - Just works with SW such as nanominer
HNK/GL Gfx = 3MH/s average

Ubuntu
DO NOT INSTALL amdgpu-pro drivers
Install rocm opencl/rocminfo

Fix missing dependency for rocm4.0
sudo apt install libtinfo5

Add lines to /etc/ld.so.conf.d/hsa-rocr-dev.conf

/opt/rocm-4.0.0/hsa/lib
/opt/rocm-4.0.0/lib
/opt/rocm-4.0.0/opencl/lib

run ldconfig

- add user to video group
- add user to render group
