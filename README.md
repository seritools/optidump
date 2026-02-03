# Patched Optiarc firmwares for archival (redump etc.)

These firmwares unlock scrambled reading for the entire range from LBA -135 to leadout. That's it.

## Supported drives

Firmwares are based on the latest Liggy/Dee's
([archive](https://web.archive.org/web/20181002183703/http://liggydee.cdfreaks.com/page/en/),
[github](https://github.com/Liggy/binflash)) firmware releases with Riplock removed, set to RPC1,
and bitsetting enabled.

| Model           | Patch V. | Based on                    | Notes     | Reported Vendor/Name       | Rep. FW Version | Rep. Vendor String     |
|-----------------|----------|-----------------------------|-----------|----------------------------|-----------------|------------------------|
| ND-3520A (PATA) | SE01     | 3.07 (3.07bt_rpc1 LiggyDee) | [^pregap] | `_NEC    DVD_RW ND-3520AW` | `3.07`          | `seri-01 BT-LIGGY`     |
| AD-7173A (PATA) | SE01     | 1.04 (1.04bt_rpc1 LiggyDee) | [^dma]    | `Optiarc DVD RW AD-7173A ` | `1-04`          | `seri-01    BT-LIGGY`  |
| AD-7290H (SATA) | SE02     | 1h44 (1h44_rpc1 LiggyDee)   | [^serial] | `hp      DVD RW AD-7290H5` | `SE02`          | `Feb17'12\[serial]`    |

[^dma]: Drive has a bug where firmware updates don't work if DMA is enabled. Use PIO mode to update
    firmware.

[^pregap]: Drive struggles with the first supported pregap sectors (negative LBA) on some discs,
    needs multiple retries.

[^serial]: The drive injects its serial into the vendor string, so I instead modified the firmware
    version.

## Download and patching

Downloads: <https://archive.org/details/optidump-fw>

Use [binflash](https://github.com/Liggy/binflash) to flash.

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
