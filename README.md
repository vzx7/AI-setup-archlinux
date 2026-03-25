# AI-setup-archlinux
A manual for setting up an AI environment for development using VS Code.
## OS
```sh
uname -a
Linux archlinux 6.19.9-arch1-1
```
## Hardware
```ini
inxi -CGD
CPU:
  Info: 6-core model: 11th Gen Intel Core i5-11400 bits: 64 type: MT MCP
    cache: L2: 3 MiB
  Speed (MHz): avg: 4295 min/max: 800/4400 cores: 1: 4295 2: 4295 3: 4295
    4: 4295 5: 4295 6: 4295 7: 4295 8: 4295 9: 4295 10: 4295 11: 4295 12: 4295
Graphics:
  Device-1: Intel RocketLake-S GT1 [UHD Graphics 730] driver: i915 v: kernel
  Device-2: Sonix A4tech FHD 1080P PC Camera driver: snd-usb-audio,uvcvideo
    type: USB
  Display: unspecified server: X.Org v: 21.1.21 with: Xwayland v: 24.1.9
    driver: X: loaded: modesetting unloaded: vesa dri: iris gpu: i915
    resolution: 1: 1920x1200~60Hz 2: 1920x1080~60Hz
  API: OpenGL Message: Unable to show GL data. glxinfo is missing.
  Info: Tools: x11: xdriinfo, xdpyinfo, xprop, xrandr
Drives:
  Local Storage: total: 2.06 TiB used: 924.62 GiB (43.8%)
  ID-1: /dev/nvme0n1 vendor: A-Data model: LEGEND 710 size: 476.94 GiB
  ID-2: /dev/sda vendor: Western Digital model: WD5000AAKX-001CA0
    size: 465.76 GiB
  ID-3: /dev/sdb vendor: Apacer model: AS350 256GB size: 238.47 GiB
  ID-4: /dev/sdc vendor: Toshiba model: DT01ACA100 size: 931.51 GiB

```
## Manual

  [Setting up VS code to work with Ollama (LLM)](./MANUAL.md)