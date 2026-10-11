# OnePlus Ace 5 / OnePlus 13R (giulia / giuliac) AERA Device Tree

Device tree for building AERA Recovery (LVGL interface) for OnePlus Ace 5 (PKG110) and OnePlus 13R (CPH2645 / CPH2647 / CPH2691).

## Device Specifications

| Feature | Specification |
| :--- | :--- |
| **SoC** | Qualcomm Snapdragon 8 Gen 3 (SM8650 / pineapple) |
| **CPU** | Octa-core (1x3.3 GHz Cortex-X4 & 5x3.2 GHz Cortex-A720 & 2x2.3 GHz Cortex-A520) |
| **GPU** | Adreno 750 |
| **Display** | 6.78-inch 1.5K AMOLED, 2780 x 1264 pixels, 120Hz LTPO |
| **OS** | ColorOS 15 (Android 15) |
| **Device Codename** | `giuliac` (China Ace 5 / PKG110), `giulia` (Global 13R) |

## Features & Bring-Up Targets

- [x] LVGL Native Touch UI (1.5K 2780x1264 display profile, 120Hz refresh)
- [x] Dynamic model detection via `libinit` (`ro.boot.prjname` 23851 -> Ace 5 PKG110)
- [x] Android 15/16 FBE v2 File-based encryption with Wrappedkey support
- [x] OPLUS Dynamic Partitions (Super partition, `my_product`, `my_heytap`, etc.)
- [x] Fastbootd & USB ADB / MTP / OTG
- [x] Hardware accelerated Adreno 750 rendering
- [x] Qualcomm PAL/AGM audio integration
- [x] AIDL Haptics and RichTap motor support
- [x] Wi-Fi networking and ADB over Wi-Fi
- [x] KernelSU, KernelSU-Next, and APatch root support

## How to Build

### 1. Sync AERA Recovery Source

```bash
mkdir -p ~/android/AERA_16.0
cd ~/android/AERA_16.0
repo init -u https://github.com/AERA-Recovery/android_manifest -b aera-16.0
repo sync -c -j$(nproc --all)
```

### 2. Place Device Tree

```bash
git clone <this_repo_url> device/oneplus/giulia
```

### 3. Build Recovery Image

```bash
cd ~/android/AERA_16.0
source build/envsetup.sh
lunch twrp_giulia-eng
mka recoveryimage
```
