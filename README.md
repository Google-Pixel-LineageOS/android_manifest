# Google Pixel | Build Instructions with Manifest
<br/>

Set up Linux environment
```
curl https://raw.githubusercontent.com/Google-Pixel-LineageOS/android_manifest/lineage-19.1/Scripts/environment.sh > environment.sh
sh environment.sh
```
<br/>

Initialize repo:
```
mkdir -p ~/android/lineage
cd ~/android/lineage
repo init -u https://github.com/Google-Pixel-LineageOS/android_manifest.git -b lineage-19.1
```
<br/>


Download latest manifest:
```
mkdir -p .repo/local_manifests
curl https://raw.githubusercontent.com/Google-Pixel-LineageOS/android_manifest/lineage-19.1/Manifests/manifest.xml > .repo/local_manifests/manifest.xml
curl https://raw.githubusercontent.com/Google-Pixel-LineageOS/android_manifest/lineage-19.1/Manifests/gapps.xml > .repo/local_manifests/gapps.xml
```
<br/>

Sync repo:
```
repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags
source build/envsetup.sh
```
<br/>

Patches:

```ADB```
```
patch -d  packages/modules/adb/ -p1 < .repo/manifests/patches/adb.patch
```

```MicroG```
```
patch -d frameworks/base/ -p1 < .repo/manifests/patches/0023-Add-support-for-app-signature-spoofing.patch
```

```Legacy```
```
patch -d art -p1 < .repo/manifests/patches/art.patch
patch -d external/perfetto -p1 < .repo/manifests/patches/perfetto.patch
patch -d system/bpf -p1 < .repo/manifests/patches/bpf.patch
patch -d system/netd -p1 < .repo/manifests/patches/netd.patch
patch -d frameworks/native -p1 < ".repo/manifests/patches/0001-SurfaceFlinger-Don't-cleanup-resources-from-previous-frame.patch"
patch -d vendor/lineage -p1 < .repo/manifests/patches/0001-Restore-libbfqio-for-non-BPF-devices.patch

```

``` Monet```
```
patch -d frameworks/base -p1 < .repo/manifests/patches/0013-SystemUI-Always-refresh-power-menu-on-UI-mode-change.patch
patch -d frameworks/base -p1 < .repo/manifests/patches/0021-monet-Fix-overly-low-chroma-for-tones-below-90.patch
patch -d frameworks/base -p1 < .repo/manifests/patches/0006-Keyguard-Never-switch-to-large-clock.patch
patch -d packages/apps/Trebuchet -p1 < .repo/manifests/patches/0001-launcher-Add-support-for-themed-icons.patch
```

```Hacks ```
```
patch -d frameworks/base -p1 < .repo/manifests/patches/0001-Hack-Ignore-SensorPrivacyService-Security-Exception.patch
patch -d frameworks/base -p1 < .repo/manifests/patches/0002-Bring-Back-XML-Format-UTF-8-TWRP.patch
patch -d frameworks/base -p1 < .repo/manifests/patches/0001-Fix-Brightness-Slider-12.patch
patch -d frameworks/native -p1 < .repo/manifests/patches/0001-keystore2-fallback-mCallingSid-to-getpidcon.patch
patch -d frameworks/base -p1 < .repo/manifests/patches/0002-Disable-vendor-mismatch-warning.patch
patch -d frameworks/base -p1 < .repo/manifests/patches/0012-core-Remove-old-app-target-SDK-dialog.patch
```

```GMS ```
```
patch -d vendor/partner_gms -p1 < .repo/manifests/patches/0001-Minimal-GMS-For-J5-Devices.patch
```
<br/>

<br/>

Build:

```sailfish```

```
brunch sailfish #for OG Pixel
```
<br/>

```marlin ```

```
brunch marlin #for OG Pixel XL
```
<br/>
