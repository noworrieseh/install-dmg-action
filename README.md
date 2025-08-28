# Install DMG Action

This action mounts a DMG file and runs an installer. Only supported on macOS as it uses the hdiutil command. It can also be used to just

## Inputs

| Name      | Description                              | Required | Default |
| --------- | ---------------------------------------- | -------- | ------- |
| dmg       | The DMG file to mount. `none` means skip | false    | `none`  |
| installer | Installer to run. `none` means skip      | false    | `none`  |
| detach    | Detach Volume                            | false    | `true`  |

## Outputs

| Name      | Description                 |
| --------- | --------------------------- |
| directory | Directory of mounted volume |

## Example

Downloads a release DMG from another repo, mounts the DMG, and runs the installer in the image.

```
jobs:
  build:
    runs-on: macos-14
    env:
       MACFUSE_VERSION: 4.8.2

    steps:
    - name: Checkout code
      uses: actions/checkout@v5

    - name: Download macFUSE
      uses: dsaltares/fetch-gh-release-asset@master
      with:
        repo: macfuse/macfuse
        version: tags/macfuse-${{ env.MACFUSE_VERSION }}
        file: macfuse-${{ env.MACFUSE_VERSION }}.dmg
        target: macfuse.dmg

    - name: Install macFUSE
      uses: noworrieseh/install-dmg-action@v1
      with:
        dmg: macfuse.dmg
        installer: "Install macFUSE.pkg"

```
