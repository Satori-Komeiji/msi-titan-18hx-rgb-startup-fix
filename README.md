# MSI Titan 18 HX RGB Startup Fix
Driver-based fix for MSI Titan 18 HX Dragon Edition Norse Myth: keyboard RGB not lighting at boot / lock screen (or staying off until SteelSeries loads).

## MSI Titan 18 HX Dragon Edition Norse Myth (A2XWJG-429CA)
### Fix: Keyboard RGB OFF until Windows/SteelSeries loads + Brightness “Offset” behavior

**Author:** Lily (original discovery + fix)  
**Model tested:** MSI Titan 18 HX Dragon Edition Norse Myth **A2XWJG-429CA**  
**OS:** Windows 11 Pro  
**Date:** 2025-12-15

### Symptoms
- Keyboard RGB/backlight stayed **completely off** during boot / BIOS / Windows lock screen.
- Keyboard RGB only turned on **after** logging into Windows (when SteelSeries GG finished loading).
- Touchpad RGB stayed on throughout boot, but keyboard did not.
- Fn brightness steps appeared **out of sync / offset** between touchpad and keyboard (cycling but not aligned).

### What DIDN’T fix it (for me)
- Reinstalling RGB apps / toggling RGB control settings alone
- EC reset alone
- BIOS-only changes alone

### The fix that worked
> Note: This is confirmed on A2XWJG-429CA. It may also help other MSI Titan 18 HX / A2XW variants with similar symptoms, but results may vary by BIOS/EC and driver versions.

Reinstalling these drivers from MSI’s support page for the exact model:

1) **Intel HID Event Filter driver**
- Version: **2.2.2.12**
- Release date: **2025-02-12**
- File size: **0.10 MB**
- SHA-256: `72e83d108f72c77393d6fdc64785975ae75c3451784547ffce5bbd8e48d569a2`

2) **Intel Serial IO driver**
- Version: **30.100.2419.23**
- Release date: **2025-05-09**
- File size: **2.96 MB**
- SHA-256: `953353ad796454e3e7a2e20766b43523cd9459825bd90562c1ae9e7ff97af322`

After reinstalling those drivers:
- Keyboard RGB began lighting **at startup** alongside the touchpad again
- The “RGB dead until login” behavior stopped
- Brightness behavior returned to normal / usable

### Steps (exact)
1. Download the drivers from MSI for **A2XWJG-429CA**
2. Install **Intel HID Event Filter**
3. Reboot
4. Install **Intel Serial IO**
5. Reboot
6. Confirm keyboard RGB lights during boot / at lock screen

### Notes / Theory (why this makes sense)
This appears to be an HID / event pipeline initialization issue: keyboard lighting behavior seems tied to chipset/HID event handling (not only RGB apps). Fixing Serial IO + HID Event Filter restores proper device initialization timing.

### Safety / best practice
- Create a **System Restore Point** before experimenting further.
- If newer versions exist, try the latest first. If that doesn’t work, these known-good versions are confirmed to fix the issue on A2XWJG-429CA.
- I’m not redistributing any MSI/Intel files here. Download drivers only from official MSI sources.

**Keywords:** MSI Titan 18 HX, Norse Myth, A2XWJG, keyboard RGB, SteelSeries GG, Intel Serial IO, HID Event Filter, backlight off at boot
