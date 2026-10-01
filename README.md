# Build OrangeFox recovery with GitHub Actions

Builds an OrangeFox recovery from any device tree repository. Fork this, run the
workflow, and the `.img` and `.zip` land in the repository releases.

## Inputs

| Input | Default | Description |
| --- | --- | --- |
| `device_tree_url` | none, required | Device tree repository, for example `https://github.com/anonytry/recovery_sky` |
| `device_tree_branch` | `main` | Branch to clone |
| `manifest_branch` | `16.0` | OrangeFox manifest branch, `16.0` or `12.1` |
| `notification_mode` | `quiet` | Telegram notification group, `quiet` or `loud` |

The device tree URL is an input, so the same builder works for any tree.

## Fixed values

These match the `sky` device and only need editing if you fork this for another
device, in `.github/workflows/Recovery Build.yml`:

| Name | Value |
| --- | --- |
| `SYNC_URL` | `https://gitlab.com/OrangeFox/sync.git` |
| `DEVICE_PATH` | `device/xiaomi/sky` |
| `DEVICE_NAME` | `sky` |
| `MAKEFILE_NAME` | `fox_sky-eng` |
| `BUILD_TARGET` | `recovery` |

## Running a build

Actions -> Recovery Build -> Run workflow, fill in the device tree URL, start.

## Disk space

This is the part most likely to bite. OrangeFox needs a lot of space: the wiki
quotes **45GB** for `fox_12.1` and **85GB** for `fox_14.1`, so `fox_16.0` needs
more again. A stock `ubuntu-24.04` runner does not comfortably hold that. If the
build dies with a disk full error, use a larger runner.

## Notifications

Telegram messages need the `TELEGRAM_BOT_TOKEN` secret set in the repository
settings. Notification failures never fail the build.

## Credits

- OrangeFox Recovery
- TWRP
- The Android Open Source Project