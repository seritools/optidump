# Patched Optiarc firmwares for archival (redump etc.)

These firmwares unlock scrambled reading for the entire range from LBA -135 to leadout. That's it.

## Supported drives

Firmwares are based on the latest Liggy/Dee's
([archive](https://web.archive.org/web/20181002183703/http://liggydee.cdfreaks.com/page/en/),
[github](https://github.com/Liggy/binflash)) firmware releases with Riplock removed, set to RPC1,
and bitsetting enabled.

NOTE: For some models, there are multiple revisions (e.g. AD-5280S 1.01/1.G8/1.Z8). These are not
necessarily compatible with each other, and will fail to flash. Please flash with `-v` to see full
log output, and create an issue with that output if you run into issues.

| Model           | Patch V. | FW (Liggy/Dee name) | Notes     | Reported Vendor/Name       | Rep. FW Ver | Rep. Vendor String     | Verified by        |
|-----------------|----------|---------------------|-----------|----------------------------|-------------|------------------------|--------------------|
| ND-3520A (PATA) | SE01     | 3.07 (307bt_rpc1)   | [^pregap] | `_NEC    DVD_RW ND-3520AW` | `3.07`      | `seri-01 BT-LIGGY`     | @seritools         |
| ND-4551A (PATA) | SE01     | 1.09 (109bt_rpc1)   |           | `_NEC    DVD_RW ND-4551A ` | `1-09`      | `seri-01 BT-LIGGY`     | @madsl             |
| AD-5200A (PATA) | SE01     | 1.09 (109bt_rpc1)   | [^5200a]  | `Optiarc DVD RW AD-5200A ` | `1.09`      | `seri-01    BT-LIGGY`  | SpikerZ            |
| AD-5280S (SATA) | SE01     | 1.01 (101bt_rpc1)   |           | `Optiarc DVD RW AD-5280S ` | `1.01`      | `seri-01    BT-LIGGY`  | SpikerZ            |
| AD-7173A (PATA) | SE01     | 1.04 (104bt_rpc1)   | [^dma]    | `Optiarc DVD RW AD-7173A ` | `1-04`      | `seri-v1    BT-LIGGY`  | @seritools         |
| AD-7241S (SATA) | SE01     | 1.61 (161bt_rpc1)   | [^dru875] | `SONY    DVD RW DRU-875S ` | `1.61`      | `seri-01    BT-LIGGY`  | @APOLLONS          |
| AD-7250H (SATA) | SE01     | 1.D3 (1d3bt_rpc1)   |           | `Optiarc DVD RW AD-7250H ` | `1.D3`      | `seri-01    BT-LIGGY`  | @NBA2K1            |
| AD-7290H (SATA) | SE02     | 1h44 (1h44_rpc1)    | [^serial] | `hp      DVD RW AD-7290H5` | `SE02`      | `Feb17'12\[serial]`    | Morlit, @seritools |
| AD-7590A (PATA) | SE01     | 1.V1 (1v1bt_rpc1)   |           | `Optiarc DVD RW AD-7590A ` | `1.V1`      | `seri-01    BT-LIGGY`  | @MarvinOl          |

[^dma]: Drive has a bug where firmware updates don't work if DMA is enabled. Use PIO mode to update
    firmware.
[^pregap]: Drive struggles with the first supported pregap sectors (negative LBA) on some discs,
    needs multiple retries.
[^serial]: The drive injects its serial into the vendor string, so I instead modified the firmware
    version.
[^dru875]: also known as Sony DRU-875S
[^5200a]: Has a weird double firmware file. I only patched the "second" half. Please raise an issue
    if you don't see the `seri-01` in the vendor string after flashing.

## Patched but currently unverified drives

| Model           | Patch V. | FW (Liggy/Dee name) | Notes      | Reported Vendor/Name       | Rep. FW Ver | Rep. Vendor String     | Verified by  |
|-----------------|----------|---------------------|------------|----------------------------|-------------|------------------------|--------------|
| AD-5170A (PATA) | SE01     | 1.H1 (1h1bt_rpc1)   | [^dma]     | `Optiarc DVD RW AD-5170A ` | `1.H1`      | `seri-01    BT-LIGGY`  | -            |
| AD-5170A (PATA) | SE01     | 1.Gq (1gqbt_rpc1)   | Duplicator | `Optiarc DVD RW AD-5170A ` | `1.Gq`      | `seri-01`              | -            |
| AD-5280S (SATA) | SE01     | 1.Z8 (1z8_rpc1)     | 1.Z ver    | `Optiarc DVD RW AD-5280S ` | `1.Z8`      | `seri-01`              | -            |

These firmwares were patched but couldn't be tested yet. If you've got one of these drives, please
contact me to try it out and let me know how it goes!

## Download and patching

Downloads: <https://archive.org/details/optidump-fw>

Use [binflash](https://github.com/Liggy/binflash) to flash. Please always use the `-v` flag.

## More drives

Generally, all NEC/Optiarc drives based on the V850ES platform (MC-10xxx and µPD chipset) supported
by Liggy/Dee's binflash tool should be patchable.

If you have a drive that is not listed here, feel free to create an issue and I'll see what I can
do.

## Supported discs

Thank you Morlit for testing the more cursed discs (on AD-7290H).

Lots of discs work fine (CD, CD-DA, CD-i, CD-XA, CD-Extra).

The drives currently fail or struggle with:

- DPM reading (via Morlit and me, both Alcohol 120% and Daemon Tools fail)
- Weirdly mastered discs (via Morlit: <http://redump.org/disc/79065/>)
- Hexalock protected discs (via Morlit)
- Codelok/Copylock protected discs (via Morlit and me)
- Reading CD-Text over 0x800 (2048) bytes in length. Will return the correct length, but zeroed out
  after 0x800. (via @MarvinOl on AD-7590A; might be disc-specific)
