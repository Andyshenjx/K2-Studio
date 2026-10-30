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

## WITRN K2 firmware protocol and container adaptation

- Source: https://github.com/lliooly/witrn-k2-mac
- Pinned reference commit: `15df558eb761a75de92e45daec0e4dd2e2af3277`.
- Reference files: `k2up/firmware.py`, `k2up/protocol.py`, `k2up/updater.py`, `k2up/backup.py`, `k2up/transport.py`, and `k2up/data/firmware_decode.bin`.
- Copyright (c) 2026 WITRN K2 Updater RE contributors.
- Original code and documentation license: **MIT**. The full upstream notice is retained in `Sources/K2Studio/Resources/WITRNFirmware-MIT.txt` and copied into both Xcode and SwiftPM app resources.
- Adaptation: K2 container validation / recovery wrapping, model bytes, application and backup ranges, frame checksums, command layout, identity probing, two-pass backup, erase / write / readback / commit ordering. The Python runtime and HIDAPI library are not included. The transport is implemented with native IOKit, a bounded input queue, and a worker-owned run loop. Swift code also verifies the complete erase span, checks the selected interface and identity again before erasing, and adds app-level mutual exclusion and close protection.
- The 256-byte substitution table embedded in `FirmwareImage.swift` is vendor-derived protocol data reproduced from the reference project's `firmware_decode.bin` (Git blob `e9f5cb8bf772703fce1a34a39a9a35df4216eb70`). Upstream states it was reconstructed through analysis of vendor software and makes no ownership claim over vendor material. Project licenses do not grant rights to vendor software, firmware, trademarks, or other third-party material.
- No vendor firmware, vendor executable, reference screenshots, or DFU illustrations are redistributed with this feature. Users supply their own local firmware. The reference project's single-device results are not hardware validation of K2 Studio's native implementation.

## Official WITRN K2Picture resource interoperability

- Primary sources: [official K2Picture 1.1 page](https://www.witrn.com/?p=2615), [official dial resources](https://www.witrn.com/?p=2639), and [official K2 manual](https://www.witrn.com/?p=2105).
- The user supplied the official K2Picture 1.1 distribution. Static inspection of its metadata and resource methods established the BMP dimensions, RGB565 packing, 400-byte `.pic` structure, 17 editable element mappings, font identifiers, resource addresses and command conventions. Hashes and method identifiers are recorded in `Documentation/K2PICTURE.md`.
- The resource importer, byte-preserving layout editor and transaction code are written in Swift. They share the existing native DFU transport and protocol described above; that adaptation retains its original attribution and MIT notice. No third-party community appearance implementation was incorporated. The layout preview uses fixed example readings and substitute system fonts; its starter layout is authored for K2 Studio and is not a factory device screen.
- The later editor expansion follows the feature scope in the user-referenced [维简 Mac documentation](https://github.com/lliooly/witrn-k2-mac/blob/15df558eb761a75de92e45daec0e4dd2e2af3277/docs/macos-app.md): image fitting, project persistence and undo/redo. These editor additions are independently implemented with SwiftUI, ImageIO and Core Graphics. K2 Studio's `.k2studioproject` is its own format and does not claim interoperability with the other application's `.k2project`; `.pic` and BMP remain the common resource interchange formats.
- K2Picture executables, assemblies, HID libraries, fonts and dial assets are not bundled or redistributed. Users provide their own images and parameter files. Project licensing does not grant rights to vendor software, firmware, trademarks or dial artwork.
- No compilation, runtime or hardware verification was performed for this addition.

## License files

`LICENSE` contains the unmodified GNU Lesser General Public License version 3.
`COPYING` contains the unmodified GNU General Public License version 3, which is incorporated by the LGPL.
The complete editable Swift source and build files are provided in the source ZIP attached to each release. K2 Studio is provided under LGPL-3.0-or-later.

K2 Studio is an independent third-party project and is not an official WITRN application.
