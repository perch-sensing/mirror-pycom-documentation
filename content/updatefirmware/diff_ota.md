---
title: "Differential OTA Update"
aliases:
    - updatefirmwate/diff_ota.html
    - updatefirmwate/diff_ota.md
    - chapter/updatefirmwate/diff_ota

---

Differential update allows you to update your device using a differential update file (patch file) instead of a complete new binary. This can save a considerable amount of space and bandwidth while downloading the new firmware. The exact size of the patch file depends on the differences  between the source and the target versions and it will usually be quite small when upgrading to a successive version.

> Note: You can only perform the differential updates if your current firmware version supports this feature. The target can be any version above `1.20`. You can check whether this feature is enabled in your firmware or not by calling `pycom.diff_update_enabled()` function.

## Generating a Differential Update File

The differential update files can be generated by using our `DiffCreator` tool which uses `bsdiff`.
In order to generate the differential update file, you will need the following tools and files:

* [DiffCreator](/gitbook/assets/DiffCreator.tar.gz)
* Old firmware version binary
* New firmware version binary

> Note: The binary files used for this are the *.bin* files generated after the firmware is built. If you have downloaded the firmware as a compressed archive, you can decompress it to find the *.bin* file.

1. Download the `DiffCreator` tool using the above link.
2. After extracting the contents of the `DiffCreator` archive, navigate to the directory with the terminal and type `make` to build the utility. 
3. After building you can run the following command in the terminal to generate the patch file:

```
./diff_creator source.bin target.bin patch.bin
```

* `source.bin` is the current binary of your device, 
* `target.bin` is the target binary
* `patch.bin` is the name of the patch file that you want to be generated.


> Note: replace the `.bin` filenames with the actual filenames.

This will create the *patch.bin* file which can be used to upgrade your firmware instead of *target.bin* file.


## Using the Differential Update File

To apply the differential update, use any of the methds described [here](../ota) by using your generated differential update file (e.g. patch.bin) as the new firmware binary.

The following message will be displayed on REPL when a differential update file is detected by the device:

```
Differential Update Image detected. Restart the device to apply the patch.
```

After this, the device must be restarted so that the patch can be applied. After restart, you should see the following messages in REPL:

```
Patching the binary...
Patching SUCCESSFUL.
```

After patching is done, the device will restart again automatically and this time the updated firmware will be loaded.

