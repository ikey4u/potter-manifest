# LineageOS for Security Research

Customize the Android OS for security research for fun and profit :)

# Initialize Repository

You have several ways to initialize your local repository, choose one from below list:

- Initialize from Google and Github

    For people who could access Google directly, you can use the following method

        repo init -u https://github.com/ikey4u/android.git -b android-7.1.2_r36

    which equals

        repo init -u https://github.com/ikey4u/android.git -b android-7.1.2_r36 default.xml

- Initialize from mirror

    If you are in China, you may use this method to speed up your download.

        repo init -u https://github.com/ikey4u/android.git -b android-7.1.2_r36 -m tsinghua.xml

- Initialize from local server
    
    If you have mirrored AOSP and Lineage onto your local server, you may need
    some more steps to make this work.

    Firstly, clone this repository into your own Github, change ip address in local.xml
    to your local server, and push it, then use the following command:

        repo init -u https://github.com/<your github user name>/android.git -b android-7.1.2_r36 -m local.xml

Notice that every time you use `repo init` command, it will auto update itself
using the default source (Google), if you cannot access google, you may export
an environment `REPO_URL` or pass `--repo-url` to repo commands. For example,
you  may set it to `https://mirrors.tuna.tsinghua.edu.cn/git/git-repo/ ` if you
are in china.

# Sync source codes

When you have initialized your repository, its time to sync the codes into your
working directory. To sync up, using the following script(you could save it as sync.sh)

    #!/bin/bash
    echo "======start repo sync======"
    repo sync
    while [ $? == 1 ]; do
    echo "======sync failed, re-sync again======"
    sleep 3
    repo sync
    done

# Build

Please see the [LineageOS Wiki](https://wiki.lineageos.org/) for building instructions.
