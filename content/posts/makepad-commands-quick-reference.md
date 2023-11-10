+++
title="Makepad Commands Quick Reference"
date=2023-11-09
+++

Yesterday I wrote a post detailing specific instructions on how to build and run Makepad apps on IOS and Android devices. This post is a quick reference that lists most the commands, including sample commands for specific  apps in the [Project Robius](https://github.com/project-robius) repo.

For more detailed descriptions, please see:
[Makepad Build Commands](https://edwardtan.com/posts/makepad-build-commands/)

## Cargo Tools Installations

These are commands that need to be run at least once initially to setup Makepad development environments. They should also be run once in a while or when there are updates to the cargo_makepad script. I personally run them about once a week.

```bash
rustup update
rustup install nightly
rustup toolchain install nightly

cd ~/projects/makepad
cargo install --path ./tools/cargo_makepad
cargo makepad android toolchain-install
cargo makepad apple ios toolchain-install
```

## Android

The following should be run inside each of the sample app directories.

Command for installing the app onto an IOS Simulator.

```bash
cargo makepad android run -p makepad_wechat --release

cargo makepad android run -p makepad_taobao --release

cargo makepad android run -p makepad_widgets_sample --release

cargo makepad android run -p todo_makepad --release
```

## IOS Simulator

The following should be run inside each of the sample app directories.

Command for installing the app onto an IOS Simulator.

```bash
cargo makepad apple ios --org=rs.robius --app=taobao run-sim -p makepad_taobao --release

cargo makepad apple ios --org=rs.robius --app=wechat run-sim -p makepad_wechat --release

cargo makepad apple ios --org=rs.robius --app=WidgetsSample run-sim -p makepad_widgets_sample --release

cargo makepad apple ios --org=rs.robius --app=todo run-sim -p todo_makepad --release
```

## IOS Device

The following should be run inside each of the sample app directories.

Command for installing the app onto a physical IOS device:

```bash
cargo makepad apple ios --org-id=ORGIDVALUE --org=rs.robius --app=wechat run-device -p makepad_wechat --release

cargo makepad apple ios --org-id=ORGIDVALUE --org=rs.robius --app=taobao run-device -p makepad_taobao --release

cargo makepad apple ios --org-id=ORGIDVALUE --org=rs.robius --app=WidgetsSample run-device -p makepad_widgets_sample --release

cargo makepad apple ios --org-id=ORGIDVALUE --org=rs.robius --app=todo run-device -p todo_makepad --release
```

## Cargo Check Builds

Command to check that the compilation passes for all Makepad supported platforms:
(Will use 100% CPU and cause hang machine, only try on high-end systems)

```bash
cargo makepad check install-toolchain
cargo makepad check all
```
