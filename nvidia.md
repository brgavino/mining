# Creating a headless config for nVidia on Ubuntu - eGPU w/ NUC8i7HVK (AMD/Intel gfx)

Install the latest drivers from nVidia, full install
* You may be tempted to not install opengl extensions, but this is necessary for managing clocks using nvidia-settings, even if you don't plan on using the GUI version

**DO NOT CREATE AN XORG.CONF**

*/usr/share/X11/xorg.conf.d files can be used instead of a monolithic xorg.conf*

Add the following to 10-amdgpu.conf

```
Section "Device"
	Identifier "AMDgpu"
	Driver "amdgpu"
	BusID "PCI:1:0:0"
EndSection

Section "Screen"
    Identifier     "amd"
    Device         "AMDgpu"
    Monitor        "Monitor0"
EndSection


Section "Monitor"
    Identifier     "Monitor0"
EndSection
```

*Note that the "OutputClass" will now be the "Driver" section*

Add the following as a 10-nvidia.conf
```
Section "Device"
	Identifier "Nvidiagpu"
	Driver "nvidia"
	BusID  "PCI:12:0:0"	
	Option "Coolbits" "28"
	Option "AllowEmptyInitialConfiguration" "True"
  Option "AllowExternalGpus" "true"
EndSection

Section "Screen"
    Identifier "nv"
    Device "Nvidiagpu"
EndSection

Section "ServerLayout"
    Identifier     "layout"
    Screen      0  "amd" 0 0
    Screen      1  "nv"
EndSection
```

*Change the BusID to match your graphics card bus*
* The Device is created with the appropriate Driver
* A Screen is defined for the Device
* The ServerLayout is defined, with the AMD Device as the primary display, and the nVidia Device as an empty config
** This allows nvidia-settings to be run on a display - otherwise, you get a "no device found error"
** Without this config, you can access the device info in nvidia-smi, but only setting the power level is useful for most cards
