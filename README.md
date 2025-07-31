# Chrultrablue (working title) &nbsp; [![bluebuild build badge](https://github.com/cablespaghetti/chrultrablue/actions/workflows/build.yml/badge.svg)](https://github.com/cablespaghetti/chrultrablue/actions/workflows/build.yml)

Yet another attempt at trying to build a Universal Blue image targeted at my collection of shit end of life Chromebooks. This one is based on the hyprland image from https://github.com/wayblueorg/wayblue. Please do not use it, it is likely I will lose interest in maintaining it!

## Installation

> [!WARNING]  
> [This is an experimental feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable), try at your own discretion.

To rebase an existing atomic Fedora installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/cablespaghetti/chrultrablue:latest
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Then rebase to the signed image, like so:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/cablespaghetti/chrultrablue:latest
  ```
- Reboot again to complete the installation
  ```
  systemctl reboot
  ```

The `latest` tag will automatically point to the latest build. As this is pulling from the latest tag of the wayblue image you will get upgraded to the latest Fedora without any warning. I apologise for nothing.

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/cablespaghetti/chrultrablue
```
