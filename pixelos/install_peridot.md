# Before you start

- Download the ROM zip and the **`addons`** folder from the download link. The `addons` folder is in the same location as the ROM zip.

> [!NOTE]
> The `addons` folder contains many images, but you only need the ones listed in this guide. You can ignore `vbmeta` and `super_empty`.

## Clean install (coming from another ROM)

### Step 1: Flash the required images

Reboot your device to **fastboot** mode, connect it to your PC, and run:

```bash
fastboot flash boot boot.img
fastboot flash init_boot init_boot.img
fastboot flash vendor_boot vendor_boot.img
fastboot flash dtbo dtbo.img
fastboot flash recovery recovery.img
```

> [!TIP]
> Use the actual file names from the `addons` folder (for example `boot-peridot-20261107-1914.img`), or rename the files first.

### Step 2: Boot into recovery

```bash
fastboot reboot recovery
```

### Step 3: Sideload the ROM

1. In recovery, go to **Apply update → Apply from ADB**.
2. On your PC, run:

```bash
adb sideload path/to/ROM.zip
```

> [!NOTE]
> The progress may stop at around **45–47%** and appear stuck. This is normal. It's a display quirk, and it means the transfer is complete.

> [!NOTE]
> The device firmware is already bundled with the ROM, so you **don't** need to flash a separate firmware package.

### Step 4: Format data and reboot

1. When the sideload finishes, a prompt will ask whether you want to reboot to install additional files. Choose **No**.
   - Choose **Yes** only if you couldn't format data, so the recovery restarts and you can try again.
2. Go back to the main recovery menu and select **Format data / Factory reset**.
3. Once it's done, select **Reboot system now**.

> [!TIP]
> If formatting fails or isn't available after the sideload, reboot back to recovery and try again.

The first boot may take a few minutes.

## Updating (dirty flash)

For future updates, you don't need to flash the images or format anything:

1. Boot into recovery.
2. Go to **Apply update → Apply from ADB**.
3. Run `adb sideload path/to/ROM.zip`.
4. When it finishes, choose **No** at the prompt and reboot.
