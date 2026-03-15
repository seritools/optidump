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

| Model           | Patch V. | Based on                    | Notes     | Reported Vendor/Name       | Rep. FW Ver | Rep. Vendor String     | Verified by        |
|-----------------|----------|-----------------------------|-----------|----------------------------|-------------|------------------------|--------------------|
| ND-3520A (PATA) | SE01     | 3.07 (307bt_rpc1 LiggyDee)  | [^pregap] | `_NEC    DVD_RW ND-3520AW` | `3.07`      | `seri-01 BT-LIGGY`     | @seritools         |
| ND-4551A (PATA) | SE01     | 1.09 (109bt_rpc1 LiggyDee)  |           | `_NEC    DVD_RW ND-4551A ` | `1-09`      | `seri-01 BT-LIGGY`     | @madsl             |
| AD-5280S (SATA) | SE01     | 1.01 (101bt_rpc1 LiggyDee)  |           | `Optiarc DVD RW AD-5280S ` | `1.01`      | `seri-01    BT-LIGGY`  | SpikerZ            |
| AD-7173A (PATA) | SE01     | 1.04 (104bt_rpc1 LiggyDee)  | [^dma]    | `Optiarc DVD RW AD-7173A ` | `1-04`      | `seri-01    BT-LIGGY`  | @seritools         |
| AD-7250H (SATA) | SE01     | 1.D3 (1d3bt_rpc1 LiggyDee)  |           | `Optiarc DVD RW AD-7250H ` | `1.D3`      | `seri-01    BT-LIGGY`  | @NBA2K1            |
| AD-7290H (SATA) | SE02     | 1h44 (1h44_rpc1 LiggyDee)   | [^serial] | `hp      DVD RW AD-7290H5` | `SE02`      | `Feb17'12\[serial]`    | Morlit, @seritools |
| AD-7590A (PATA) | SE01     | 1.V1 (1v1bt_rpc1 LiggyDee)  |           | `Optiarc DVD RW AD-7590A ` | `1.V1`      | `seri-01    BT-LIGGY`  | @MarvinOl          |

[^dma]: Drive has a bug where firmware updates don't work if DMA is enabled. Use PIO mode to update
    firmware.

[^pregap]: Drive struggles with the first supported pregap sectors (negative LBA) on some discs,
    needs multiple retries.

[^serial]: The drive injects its serial into the vendor string, so I instead modified the firmware
    version.

## Patched but currently unverified drives

| Model           | Patch V. | Based on                    | Notes      | Reported Vendor/Name       | Rep. FW Ver | Rep. Vendor String     | Verified by  |
|-----------------|----------|-----------------------------|------------|----------------------------|-------------|------------------------|--------------|
| AD-5170A (PATA) | SE01     | 1.Gq (1gqbt_rpc1 LiggyDee)  | Duplicator | `Optiarc DVD RW AD-5170A ` | `1.Gq`      | `seri-01`              | -            |
| AD-5280S (SATA) | SE01     | 1.Z8 (1z8_rpc1 LiggyDee)    | 1.Z ver    | `Optiarc DVD RW AD-5280S ` | `1.Z8`      | `seri-01`              | -            |

The AD-5170A is being tested by @superg, but firmwares `1.Gx` are for a different revision,
"AD-5170A for Duplicators". I accidentally patched that one first, so I'm providing it for good
measure, but it is not verified currently. If you've got one, please try it and let me know how it
goes!

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
