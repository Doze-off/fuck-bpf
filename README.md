# Fuck-BPF aka Android 16 QPR2 BPF Reverts to support <= 4.19 kernels

## Overview

This repository contains patches to revert "Bpf Requirements" in AOSP to enable legacy kernels devices (<=  4.19) boot Android 16 QPR2.

## Background

With the release of Android 16 QPR2, Google introduced strict BPF requirements that prevent booting on kernels older than version 5.4. This change rendered numerous devices unable to run Android 16 QPR2, particularly affecting:

- Devices with kernel 4.19 and older kver.

Also, Many devices in the market lack publicly available kernel sources, making it impossible to backport BPF support or upgrade to newer/latest upstream, other than this, sometimes it's infeasible to upstream kernel source due to certain factors (like some oplus devices). The mandatory BPF requirements in Android 16 QPR2 created a hard compatibility barrier, causing boot failures & splash loop on these devices.

## Solution

This repository provides source-level reverts/patches that reverse the BPF requirements, allowing Android 16 QPR2 to boot on devices without full BPF support. The patches implement fallback mechanisms and remove hard dependencies on BPF functionality.

## Usage

### Use Auto Patch Script
1. Clone this repo in root of your source tree
2. Run command:
```
./fuck-bpf/apply.sh --mb
```

### Manual Application
Patches can be applied manually to specific components:

```bash
cd /path/to/android/source/component
git am /path/to/this/repo/component/*.patch
```

### Prerequisites

- You have Android 16 QPR2 tree with proper blob patches
- Basic knowledge of Git & Android build system
- Common sense :D


## Contributing

Contributions are welcome. When submitting patches:

1. Follow the existing patch naming convention (0001-description.patch)
2. Ensure patches apply cleanly with `git am`
3. Test on target hardware before submitting
4. Include clear commit messages explaining the change

## Credits

* Patches in this repository are derived from work by multiple contributors, all credits goes to the original author of patches.
* This repository is curated & maintained by [Aryan Sinha](https://github.com/techyminati)

## License
This repo is licensed under Apache License 2.0

## Disclaimer

These patches modify core Android system components. Use at your own risk. Thoroughly test on target hardware before deploying to release. 
