Packages for various operating systems
======================================

Making a new release:
---------------------

Release dependency: I use `github-release` to automatically upload packages to github.
You can obtain it with:

```sh
go install github.com/github-release/github-release@latest
```

You will need it on both the Windows and Linux system. OSX too if I jpackage this
for it.

Releases can be created in a mostly automatic way. With a working Java toolchain
including jpackage installed:

0. Set a `GITHUB_TOKEN` in the environment containing an API key.
1. Update `CHANGES.md`
2. Update the version number(`GITHUB_TAG`) and version title(`GITHUB_NAME`) in `config.sh`
3. On a Linux machine, run `./release.sh`
4. On a Windows machine, run `./windows-release.sh`
5. On whatever machine you check in code with, run `./packages.sh`

Windows
-------

All Windows packages require building on a Windows machine. In order to build
them, check out i2p.firefox in an adjacent directory and `source` i2p.firefox/config.sh
to set the path to the Java toolchain you want to use.

run: `ant jar` before any of these scripts.

run: `windows-release.sh` only *after* release.sh on a Linux machine.

### MSI

Requires the Wixl toolset.

#### Status: Works. Maintained.

run: `./windows.sh`

#### EXE

No special requirements.

#### Status: Works. Maintained.

run: `./windows-exe.sh`

### Portable(.zip)

No special requirements.

#### Status: Works. Maintained.

run: `./windows-portable.sh`

Linux
-----

All Linux packages require building on a Linux machines. Debian packages must
be built on Debian, Fedora packages must be built on Fedora. Some leeway for
derivative distros. Portable can be b build anywhere with a jpackage. Have
Java tools in your `PATH`.

### Debian

Make sure you have a recent Java and jpackage.

#### Status: Works. Maintained.

run: `ant debian`

### Fedora

I'm a Debian user and don't have a Fedora machine set up right now.  Therefore,
I build Fedora packages in a container.

Fedora doesn't have a jpackage in their repositories as far as I can tell so I use
Adoptium's third-party repository to supply the JDK I use to build the fedora
package.

#### Status: Unknown. Maintained.

run: `ant fedora`

### Portable(.zip)

Details are platform dependent. Same build-deps as everything else.

#### Status: Works. Maintained.

run: `ant jpackage`

Docker
------

```sh
docker build -t eyedeekay/i2p.plugins.firefox .
```

```sh
xhost + local:docker
docker run -it --rm \
        --net=host \
        -e DISPLAY=unix$(DISPLAY) \
        -v /tmp/.X11-unix:/tmp/.X11-unix \
        eyedeekay/i2p.plugins.firefox
```

OSX
---

### TODO