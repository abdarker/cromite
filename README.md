<a href="https://github.com/uazo/cromite/releases/latest">
  <img src="https://img.shields.io/github/v/release/uazo/cromite" alt="current Cromite release" title="current Cromite release" />
</a>
<br>

[![Build Cromite](https://github.com/uazo/cromite/actions/workflows/build_cromite.yaml/badge.svg)](https://github.com/uazo/cromite/actions/workflows/build_cromite.yaml)

# Cromite (a Bromite fork) - Take back your browser

<a href="https://www.cromite.org">
  <img title="Cromite - take back your browser!" src="https://www.cromite.org/app_icon.png" width="96" alt="Bromite" />
</a>
<br>

Cromite is a [Chromium](https://www.chromium.org/Home) fork based on [Bromite](https://github.com/bromite/bromite) with built-in support for ad blocking and an eye for privacy.

Cromite is available for Android arm64-v8a, arm32-v7a and x86_64, Nougat and above (Minimum v8.0, API level 26), Windows and Linux 64bit.

# Goals

Cromite's goal is to
- limit the features built into the browser that can be used as a platform for tracking users' habits, and, if it is not technically possible, disable them and leave it up to the user to choose whether to re-enable them
- limit the close integration between the browser and its manufacturer
- not let the excellent research work done by csagan5 with Bromite be lost

In addition, Cromite would like to promote greater integration with other non-profit, open source browsers, encouraging closer collaboration with others, and attempt to integrate them directly into Chromium once they have reached an appropriate level of maturity.

# Privacy limitations

Cromite's privacy features, including anti-fingerprinting mitigations (which are not comprehensive), **are not to be considered useful for journalists and people living in countries with freedom limitations**, please look at [Tor Browser](https://www.torproject.org/download/) in such cases.
Please note that this project is not free of bugs and that changing the behaviour of a browser can be risky and not without problems.

# Docs
- [Privacy Policy](https://github.com/uazo/cromite/blob/master/docs/PRIVACY_POLICY.md)
- [Features](https://github.com/uazo/cromite/blob/master/docs/FEATURES.md)
- [How to build](https://github.com/uazo/cromite/blob/master/docs/HOW_TO_BUILD.md)
- [Patch list](https://github.com/uazo/cromite/blob/master/docs/PATCHES.md)

# Releases

All built versions are available as [releases](https://github.com/uazo/cromite/releases).

Cromite is currently built for ARM64, x86 (Android SDK version 23+) and Windows x64.

You will automatically receive notifications about new updates (and be able to install them) via the auto updater functionality (enabled by default), see [related wiki page](https://github.com/bromite/bromite/wiki/AutomaticUpdates).

### F-droid

Official F-droid repo url:
https://www.cromite.org/fdroid/repo/?fingerprint=49F37E74DEE483DCA2B991334FB5A0200787430D0B5F9A783DD5F13695E9517B

### Auto-update setup for windows

1. Download https://github.com/henrypp/chrlauncher/releases
2. Create a `chrlauncher.ini`

```
[chrlauncher]

# Custom Chromium update URL (string):
ChromiumUpdateUrl=https://github.com/uazo/cromite/releases/latest/download/updateurl.txt

# Command line for Chromium (string):
# note --user-data-dir= works better if path is absolute
# See here: http://peter.sh/experiments/chromium-command-line-switches/
ChromiumCommandLine=--user-data-dir="C:\Users\<my user>\AppData\Local\Cromite\User Data" --no-default-browser-check

# to enable full logging in c:\temp\log.txt (daily rotate, no automatic deletion)
# ChromiumCommandLine=--enable-logging --v=0 --log-file=C:\temp\log.txt --user-data-dir=".\User Data" --no-default-browser-check

# Chromium executable file name (string):
ChromiumBinary=chrome.exe

# Chromium binaries directory (string):
# Relative (to chrlauncher directory) or full path (env. variables supported).
ChromiumDirectory=.\bin
```
To prevent deletion by Microsoft Defender each time the browser is updated, check the `user-data-dir` folder by modifying it accordingly.

### Enable network process sandbox in windows
I don't include any setups because I don't like the experience of not knowing what they do, so you must manually run this command on first installation:
```
cd <where_is_the_exe>
icacls . /grant "*S-1-15-2-2:(OI)(CI)(RX)"
```
see https://github.com/uazo/bromite-buildtools/issues/51

### Enable AppContainer for renderer process in windows
you can activate the 'RendererAppContainer' flag from the command line with
```
  --enable-features=RendererAppContainer
```

### Making Cromite work in Ubuntu 24.04 and its derivatives (kubuntu, etc)
This happens because, starting with Ubuntu 24.04, Apparmor
restricts the use of unprivileged user namespaces. To fix this, you have several options:
#### 1. Creating an apparmor profile for cromite
Create `/etc/apparmor.d/chrome`, and write:
```
abi <abi/4.0>,
include <tunables/global>

profile cromite /home/user/cromite/chrome-lin/chrome flags=(unconfined) {
  userns,

  include if exists <local/chrome>
}
```
replacing the cromite binary path with where you have placed cromite.

Now, run `sudo apparmor_parser -r /etc/apparmor.d/cromite` to apply the changes.
#### 2. Disabling the restriction until next reboot
`sudo sysctl -w kernel.apparmor_restrict_unprivileged_userns=0`
#### 3. Disabling the restriction permanently
Add `kernel.apparmor_restrict_unprivileged_userns=0` to the file `/etc/sysctl.d/60-apparmor-namespace.conf`.  Create the file if not exists.
### Auto-update setup for linux
working in progress in https://github.com/uazo/cromite/issues/771

# Contributing

Please submit issues following the issue template; beware that GitHub does not display the templates from mobile.

Patches are welcome and accepted if they match the project goals.

If you want to help me, [here](https://github.com/uazo/cromite/blob/master/docs/HELP_ME_PLEASE.md) is the list of things I would need.

For any usage or development discussion please use GitHub Discussions: https://github.com/uazo/cromite/discussions

# Credits

* [Chromium project](https://www.chromium.org/Home) and developers
* [Bromite](https://github.com/bromite/bromite)
  * [Iridium project](https://github.com/iridium-browser) for some patches
  * [ungoogled-chromium](https://github.com/Eloston/ungoogled-chromium) for some patches
  * [ungoogled-chromium-android](https://github.com/ungoogled-software/ungoogled-chromium-android) for some patches
  * [GrapheneOS](https://github.com/GrapheneOS) for some security patches
  * [Inox patchset](https://github.com/gcarq/inox-patchset) for some patches (via ungoogled-chromium)
  * [Brave Browser](https://github.com/brave/brave-core) for some patches

thanks to [austinhuang0131](https://github.com/austinhuang0131) for the svg icon

# License

Cromite is published under [GNU GPL v3](./LICENSE).
The patches published as part of the Bromite project are released under GNU GPL v3 only.
Cromite specific patches are under the GNU GPL-2+ licence.
Each individual patch contains specific information on the licence used.
