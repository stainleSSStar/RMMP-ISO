# RMMP-ISO

ISO releases for [RMMP](https://github.com/stainleSSStar/RMMP) - a minimal Arch
Linux distribution with Trinity Desktop on XLibre that boots on BIOS and UEFI.

The distribution **source** lives in the private repository
[stainleSSStar/RMMP](https://github.com/stainleSSStar/RMMP). This repository
holds the **built images**, because GitHub Actions artifacts are size limited
(~500 MB) while release assets are not, and this way the ISOs are downloadable
without authentication.

## Downloading a release

Every release contains the ISO split into 450 MiB parts plus `SHA256SUMS`:

```sh
# download the assets of a release, then reassemble
cat rmmp-*.part* > rmmp.iso
sha256sum -c SHA256SUMS

# write it to a USB stick
sudo dd if=rmmp.iso of=/dev/sdX bs=4M status=progress oflag=sync
```

`/dev/sdX` is the whole disk, not a partition.

## Building a new ISO

The build runs here, in this repository, because of the artifact size limit:

```sh
gh workflow run build-iso.yml --repo stainleSSStar/RMMP-ISO
```

It needs the secret `RMMP_SOURCE_TOKEN` (a personal access token with the
`repo` scope that can read the private source repository) to check out the
profile. A weekly build runs automatically as a prerelease, and pushing a
`v*` tag in the source repository triggers one as well.

Full build documentation, including how to build locally on an Arch machine:
<https://github.com/stainleSSStar/RMMP/blob/main/docs/BUILD.md>
