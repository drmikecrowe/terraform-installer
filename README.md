# Terraform Installer - Automated Terraform Installation

## Automatically Download, Extract and Install Latest or Specific Version

[![](https://img.shields.io/github/release/robertpeteuil/terraform-installer.svg?colorB=2067b8)](https://github.com/robertpeteuil/terraform-installer)
[![](https://img.shields.io/badge/language-bash-89e051.svg?style=flat-square)](https://github.com/robertpeteuil/terraform-installer)
[![](https://img.shields.io/github/license/robertpeteuil/terraform-installer.svg?colorB=2067b8)](https://github.com/robertpeteuil/terraform-installer)

---

The **terraform-install** script automates the process of downloading and installing Terraform.  This provides an ideal method for installation on new hosts, installing updates and even downgrading if necessary.  This script detects or determines the OS and CPU-Architecture.

Options:

- install specific version: `-i VERSION`
- automatically `sudo` install to /usr/local/bin: `-a`
  - prevents user prompt asking for install destination
  - user must enter sudo password unless NOPASSWD is enabled
  - uncomment line 12 to make this the default behavior (`sudoInstall=true`)

### Installation with this Installer

Download the installer and make executable

``` shell
curl -LO https://raw.github.com/robertpeteuil/terraform-installer/master/terraform-install.sh
chmod +x terraform-install.sh
```

Run the installer

``` shell
./terraform-install.sh
```

Optional Parameters

``` shell
# -i = Install specific version
./terraform-install.sh -i 0.11.1

# -a = Automatic sudo install to /usr/local/bin/
./terraform-install.sh -a
```

### Terraform's Official Installation Process

- visit website download page
- locate version for OS/CPU and download
- find and extract binary from downloaded zip file
- copy binary to a directory on the PATH

### System Requirements

- System with Bash Shell (Linux, macOS, Windows Subsystem for Linux)
- `curl`
- `unzip` - terraform downloads in zip format

### Script Process Details

- Determines Version to Download and Install
  - Uses Version specified by `-i VERSION` parameter (if specified)
  - Otherwise determines Latest Version
    - Uses GitHub API to retrieve latest version number
- Calculates Download URL based on Version, OS and CPU-Architecture
- Verifies URL Validity before Downloading in Case:
  - VERSION incorrectly specified with `-i`
  - Download URL Format Changed on terraform Website
- Determines Install Destination
  - Performed before Download/Install Process in case User selects `abort`
- Installation Process
  - Download, Extract, Install, Cleanup and Display Results

#### CPU Architecture Detection

CPU architecture is detected for each OS accordingly:

- Linux / Windows (WSL since this is a Bash script)
  - detected with `lscpu` or by inspecting `/proc/cpuinfo`
- macOS - uses Default Arch `amd64` as it's the only version available on macOS
- Default Value - `amd64`

### License

Apache 2.0 License - Copyright (c) 2018    Robert Peteuil
