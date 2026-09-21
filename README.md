# Trove updates

Public update feed for Trove boxes, the custom LibreELEC image built around
the Trove Kodi skin. It holds release files only. The sources are private.

| Path | What reads it |
|---|---|
| `updates.json` | The settings add-on on each box, every 6 hours. One entry per `LIBREELEC_ARCH` (`Generic.x86_64`, `RPi5.aarch64`) with `version`, `file`, `url`, `size` and `sha256`. A box downloads the `.tar` when `version` is newer than its own `VERSION` in `/etc/os-release`, checks the sha256, and applies it on the next reboot |
| Releases (`1.0.0`, ...) | One release per image version: the `.tar` update file and the `.img.gz` for flashing |
| `addons/` | A Kodi add-on repository (`addons.xml`, `.md5`, zips plus `.sha256`), read by `repository.trove`. Newer `skin.trove` and `screensaver.trove` versions reach boxes here between images |
| `repository.trove/` | Source of the repository add-on. The image ships it as a system add-on |

Everything here is written by `tools/publish-image.py` and
`tools/publish-addons.py` in the private TroveOS repo. Don't edit the files by hand.

## Versions

- **Image:** `MAJOR.MINOR.PATCH`, e.g. `1.0.0`. It's `VERSION` in
  `/etc/os-release`. `VERSION_ID` stays at the LibreELEC base (`12.2`).
- **Skin and screensaver:** their own `MAJOR.MINOR.PATCH` from `addon.xml`,
  independent of the image. Each image ships a skin release tag, and newer
  ones arrive through `repository.trove`.
