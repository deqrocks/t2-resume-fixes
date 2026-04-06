# Apple T2 Resume Fixes

This tree currently carries two relevant Apple T2 resume-related patches:

- `patches/0001-thunderbolt-add-device-links-for-integrated-Apple-T2-NHI.patch`
  Companion Thunderbolt fix. This adds the missing device links for
  integrated Apple T2 Thunderbolt NHIs and removes the warning
  `device links to tunneled native ports are missing!`.
- `patches/0002-PCI-portdrv-use-INTx-for-Apple-T2-Thunderbolt-root-port-services.patch`
  Actual SMP resume fix. This forces PCIe port services on Apple T2
  Thunderbolt root ports (`TRP*`) to use INTx instead of MSI/MSI-X.

## Current State

- The older PCI quirk that tried to keep the ports in D0 was dropped.
- The slow `smpboot` behavior after S3 resume was reproduced on
  MacBookAir9,1 and fixed by the `pcieport` INTx patch.
- Remaining post-resume latency appears to be separate and sits in
  later device/userspace resume, especially `apple-bce`/`aaudio` and
  likely `brcmfmac`.

## Relevant Commits

- `c9a88b70e` `thunderbolt: add device links for integrated Apple T2 NHI`
- `a388d392d` `PCI/portdrv: use INTx for Apple T2 Thunderbolt root port services`

## Exported Patches

The `patches/` directory is intentionally limited to the two current
patches above so they can be shared and tested independently or sent
upstream.
