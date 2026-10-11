# avb/ — official vbmeta for the recovery partition

`recovery-vbmeta.bin` is the AVB vbmeta blob taken **from this device's own
retail recovery partition**. It is the OEM-signed vbmeta that the OnePlus
Ace 5 (PKG110 / giulia) bootloader expects for `recovery`, and it is what
`tools/transplant_avb.py` puts back into a locally built `recovery.img`, whose
own vbmeta is signed with the AOSP test key.

Provenance (no third-party files, no vendor blobs from the internet):

| item | value |
| --- | --- |
| source of the image | the phone's own OTA payload, extracted to `D:\ace5\extracted\recovery.img` |
| source image size | 104857600 bytes (100 MB partition) |
| source image vbmeta | offset 36290560, size 2240 |
| extraction tool | `D:\ace5\tools\avb_parse.py --extract` |
| this file | 2240 bytes |
| header | `AVB0`, vbmeta version 1.0 |
| algorithm | `SHA256_RSA4096`, auth block 576 B, aux block 1408 B (256+576+1408 = 2240) |
| sha256 | `250c5dea25f268e970a1310cf5aebb23d0ae7bae52d64de4a2e4c82a28c12497` |

Verification performed locally before committing: running
`tools/transplant_avb.py avb/recovery-vbmeta.bin <stock recovery.img> out.img`
reproduces the stock image **byte for byte**
(sha256 `773618278b2fc6f8d89465e2b3d80c008c377d94904717a1d469a9c336b8b0ee`),
so the footer arithmetic in the tool matches how the vendor ships the
partition.

Reference points for the layout:

* stock `recovery.img`: `original_image_size` 36290560, `vbmeta_size` 2240,
  signed (`SHA256_RSA4096`).
* the community TWRP image this phone already accepted
  (`TWRP-OnePlus-Ace5-SM86xx.img`): `original_image_size` 63242240,
  `vbmeta_size` 832, **algorithm `NONE`** — i.e. that image carries an
  unsigned vbmeta, which suggests the bootloader is not enforcing a vendor
  signature on this partition (worth remembering as a fallback: if the
  transplanted image is rejected, flash the raw AOSP-signed build instead).
