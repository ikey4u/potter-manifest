# Get source

Select an entry manifest from three alternatives to initialize `.repo`
repository

- local.xml

    If you have a local mirror of LineageOS and AOSP project, you may be
    interested in this entry.

- default.xml

    Download AOSP from Google and LineageOS related parts from Github.

- tsinghua.xml

    Download AOSP and LineageOS from Tsinghua mirror, good for China users.

Take `local.xml` as an example and assume the source directory is `potter`,
you may do something like below

    mkdir -p potter && cd potter
    repo init -u https://github.com/ikey4u/potter-manifest.git -b android-7.1.2_r36 -m local.xml --repo-url https://mirrors.tuna.tsinghua.edu.cn/git/git-repo/
    repo sync

`repo sync` may take a long time and break if your network is not stable. Try
the follwing script

	#! /bin/zsh

	curdir="$(cd "$(dirname "$0")"; pwd -P)"
	cd "$curdir"

	source $HOME/.zshrc

	echo "[$(date)] Start sync lineage ..."
	pyenv local 2.7.15
	repo sync
	while [[ $? == 1 ]]; do
		echo "[+]  sync lineage failed, try again ..."
		sleep 3
		repo sync
	done

I use zsh as my default shell and pyenv to setup python environment, you may adjust that to fit your situation.

# Build

After you get source, go to your source root directory and execute the following
commands

    source build/envsetup.sh
	lunch lineage_angler-eng

# Modification

- Change of manifest

    Add dktree.xml into  `libs` directory, this file contains device and kernel tree
    project.

    To make this file works along with default, local, and tsinghua
    entry manifests, I add a `dktree` remote tag into this entry manifests.

    dktree remote tag is essentially the same as github tag, lineage will use
    github tag to retrive projects, this change will make the build process a little different,
	see Build section for more details.
