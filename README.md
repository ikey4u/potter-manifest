# LineageOS for Security Research

Sync url is set to [Tsinghua LineageOS Mirror](https://mirror.tuna.tsinghua.edu.cn/help/lineageOS/).

## Getting Started

To initialize your local repository, use a command like this:

    repo init -u https://github.com/ikey4u/android.git -b android-7.1.2_r36

Then to sync up, using the following script(you could save it as sync.sh)

    #!/bin/bash
    echo "======start repo sync======"
    repo sync
    while [ $? == 1 ]; do
    echo "======sync failed, re-sync again======"
    sleep 3
    repo sync
    done

## Build

Please see the [LineageOS Wiki](https://wiki.lineageos.org/) for building instructions.
