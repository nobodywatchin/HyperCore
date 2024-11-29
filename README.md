# HyperCore &nbsp; [![bluebuild build badge](https://github.com/nobodywatchin/hypercore/actions/workflows/build.yml/badge.svg)](https://github.com/nobodywatchin/hypercore/actions/workflows/build.yml)

HyperCore is a purpose-built operating system for cloud-native, hyper-converged environments. It seamlessly integrates virtualization, redundant storage, and container orchestration into a unified platform.

Built on top of uCore, HyperCore incorporates Kubernetes for container management, leverages the Xen hypervisor for virtualization, and utilizes Ceph for robust, distributed storage management.

By combining these technologies, HyperCore delivers a hyper-converged server cluster within a lightweight, headless operating system, optimized for performance and simplicity.

## Installation

> **Warning**  
> [This is an experimental feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable), try at your own discretion.

To rebase an existing atomic Fedora (coreOS, Silverblue, Kinoite) installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/nobodywatchin/hypercore:latest
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Then rebase to the signed image, like so:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/nobodywatchin/hypercore:latest
  ```
- Reboot again to complete the installation
  ```
  systemctl reboot
  ```

The `latest` tag will automatically point to the latest build. That build will still always use the Fedora version specified in `recipe.yml`, so you won't get accidentally updated to the next major version.

## ISO

If build on Fedora Atomic, you can generate an offline ISO with the instructions available [here](https://blue-build.org/learn/universal-blue/#fresh-install-from-an-iso). These ISOs cannot unfortunately be distributed on GitHub for free due to large sizes, so for public projects something else has to be used for hosting.

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/nobodywatchin/hypercore
```
