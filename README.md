# Blank Slate ZMK Firmware

This repo contains the firmware for the Blank Slate PCB.

For full build guide for the Blank Slate, see https://docs.lpgala.xyz/docs/blank-slate-build-guide/overview/

# Install

After committing the changes click the "Actions" link along the top to see the list of GitHub Actions builds. Find the new build in the listing, and click on the description.

From there, near the bottom of the screen will be download labeled "firmware", that you should click to download.

Once downloaded, unzip the downloaded file, and you will have a file, named lpgalaxy_blank_slate-zmk.uf2.

Connect your Blank Slate to your computer using a USB cable, and double tap the reset button through the small hole on the bottom of the case. The blue LED should flash, slowing down once detected and connected to your computer.

A new USB "drive" should appear on your connected computer, with a name of "Blank Slate". Copy and paste the lpgalaxy_blank_slate-zmk.uf2 images to the new USB drive, and Blank Slate should complete flashing the new image and instantly restart into it.

# Soft Off Support

Blank Slate includes support for a ZMK feature this is still [in a PR](https://github.com/zmkfirmware/zmk/pull/1942). By default, this repository builds against that feature branch to ensure that works properly.

Should you desire to track ZMK `main` (or some other branch of ZMK), simply edit the `config/west.yml` file and replace the contents with:

```
manifest:
  remotes:
    - name: petejohanson
      url-base: https://github.com/petejohanson
  projects:
    - name: zmk
      remote: zmkfirmware
      revision: main
      import: app/west.yml
    - name: blank-slate-zmk-module
      remote: petejohanson
      revision: main
  self:
    path: config
```

And then comment out the line in `config/lpgalaxy_blank_slate.conf`:

```
# CONFIG_ZMK_PM_SOFT_OFF=y
```
