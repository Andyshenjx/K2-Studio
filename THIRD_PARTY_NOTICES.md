# Third-party notices

K2 Studio's WITRN protocol adaptation and PD field decoding reference the following open-source projects by **JohnScotttt / JohnScott**.

## WITRN_HID_API

- Source: https://github.com/JohnScotttt/WITRN_HID_API
- Reference file: `witrnhid/core.py`, version 1.1.5.
- Reference blob: `ed20674cd7f6b43975b2ffbbf30deed0a972b101`.
- Copyright (c) 2025 JohnScotttt.
- License: **LGPL-3.0-or-later**, as specified in upstream `pyproject.toml`.
- Adaptation: USB VID/PID, 64-byte HID framing, general-report field offsets, SOP codes, PD payload length convention. The Python HID transport and metadata class are replaced with native Swift models and IOKit input callbacks.

## USB_PD_Parser_API_Py

- Source: https://github.com/JohnScotttt/USB_PD_Parser_API_Py
- Reference file: `usbpdparser/core.py`, version 1.1.6.
- Reference blob: `516298a93541b9e6fffd41fcf7a28e4d1d712e96`.
- Copyright (c) 2025 JohnScotttt.
- License: **LGPL-3.0-or-later**.
- Adaptation: PD message type names and bit layouts for common PDO/RDO, PPS, SPR AVS, EPR AVS and extended headers. The Swift decoder implements its own bounded, per-SOP/per-sender/per-type chunk state, validates available lengths, and keeps raw reports when decoding is incomplete.
- K2 Studio does not reproduce the complete upstream parser. It does not include the upstream vendor database, Python runtime, Windows GUI, fonts, images, or executable releases.

## witrn_pd_sniffer

- Source: https://github.com/JohnScotttt/witrn_pd_sniffer
- Read as an architectural reference. Its GUI, fonts, icons, file importers and code are not incorporated into K2 Studio.

## WITRN application icon

- Source: WITRN PC V1.0.4, `WITRN.exe` icon resource, distributed through https://www.witrn.com/?p=873 and https://forum.avhzy.com/forum.php?mod=viewthread&tid=603.
- The original 48 × 48 pixel orange-and-white W icon is preserved as `Design/AppIcon/WITRNOriginal48.png`. The white W is reconstructed as editable vector geometry in `Configuration/K2AppIcon.icon/Assets/WITRNMark.svg`; this is an adaptation of the original mark, not an official high-resolution source file.
- `Configuration/K2AppIcon.icon` contains the vector foreground and orange background as separate Icon Composer layers. The Xcode App target uses Apple's native icon asset pipeline for its contour and appearances. `Sources/K2Studio/Resources/WITRNIcon.png` is a 1024 × 1024 Icon Composer render used in the sidebar. `LegacyAppIcon.icns` is an explicit App bundle fallback and is also used by package executables, rendered from these same layers with legacy macOS outer spacing.
- Used for the application icon and sidebar logo at the user's request. WITRN branding remains the property of its respective owner and is not covered by this project's LGPL license.

## License files

`LICENSE` contains the unmodified GNU Lesser General Public License version 3.
`COPYING` contains the unmodified GNU General Public License version 3, which is incorporated by the LGPL.
A separate source snapshot with the editable Swift source and build files is provided as a Release attachment. This publication did not rebuild the supplied App to verify exact correspondence. K2 Studio is provided under LGPL-3.0-or-later.

K2 Studio is an independent third-party project and is not an official WITRN application.
