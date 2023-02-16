# amdvbflash

AMD vBIOS flash utility for Linux.

---

This tool can be used to flash or dump the AMD graphics card vBIOS.
Before AMD acquired the company ATI this tool was also known as `atiflash`.

## Usage

Before flashing a new vBIOS you should dump your vBIOS first.
For this you need the adapter number of your card.
The following command will display information of all AMD adapters in the system.

```sh
sudo ./amdvbflash -i
```

If you have only one card installed the adapter number will probably be `0`.
Next we will do a backup of our vBIOS. Where `0` is the adapter number and `<file>` the name of your backup.

```sh
sudo ./amdvbflash -s 0 <file>
```

Now we can flash the new vBIOS to our card.
The following commands will write the vBIOS image in file `<file>` to flash ROM in adapter `0`. Notice that the `-f` option is not supported in external versions.

```sh
sudo ./amdvbflash -f -p 0 <file>
```

You must reboot your system now.

## Help

This will show you all possible commands and options that are available.

```sh
sudo ./amdvbflash -h
```

## Known Issues

* Incorrect dGPU Behavior

The AMDVBFlash tool, used for flashing the VBIOS image to dGPU, does not communicate with the ROM Controller specifically when the driver is present. This is because the driver, as part of its runtime power management feature, puts the dGPU to a sleep state.

As a workaround, users can run `amdgpu.runpm=0`, which temporarily disables the runtime power management feature from the driver and dynamically changes some power control-related sysfs files.

