
# tinytex-rpm

Packages [TinyTeX](https://yihui.name/tinytex/) as an RPM, including custom packages, and uploads it to a Nexus server.

This repo isn't actively maintained. It's not a project but rather a template for anyone who faces a similar challenge.

## Why this project exists

TinyTeX does not provide an installable RPM or similar. Instead, the author provides an
[installation script](https://yihui.name/gh/tinytex/tools/install-unx.sh)) that requires internet access to download
other files and dependencies. As this might not work in a corporate environment with restricted internet access, the installation script [has been adapted](./ci/build-tinytex.sh) to require only access to one CTAN repository.

## How to update

Since the TinyTeX build will always download the newest TinyTeX files and dependencies available, no files need to be
changed to update to a newer version (unless the installation procedure changed). Two builds of the same
revision might result in different results.

To build a new version of TinyTeX:

1. If needed, update [`tinytex-packages.txt`](./ci/tinytex-packages.txt) to add/remove a custom package
1. Commit your changes, if any
1. Tag the new (or existing) commit with the desired version number, e.g. `0.14`. You may want to use [TinyTeX's current version](https://github.com/yihui/tinytex/releases).
1. Push the new tag and let your Jenkins build it

## How to install

    wget https://nexus.example.com/repository/.../tinytex.rpm
    rpm -U tinytex.rpm

## Configuring access to the CTAN repository

Allow the CI system to access the CTAN repository by updating `/usr/lib64/microsoft-r/3.3/lib64/R/etc/Renviron` to contain:

    http_proxy=http://<user>:<password>@proxy.example.com:8080
    https_proxy=http://<user>:<password>@proxy.example.com:8080
    ftp_proxy=http://<user>:<password>@proxy.example.com:8080
