+++
title="Makepad Build Commands"
date=2023-11-08

[taxonomies]
# categories = [" Post"]
# tags = ["post", "makepad"]
+++

Makepad is a cross-platform UI framework written in Rust.
It is in active development, but is already usable to build quick prototypes and simple (or even complicated UI) applications.

One of the key features of the Makepad is its ability to simply, and quickly, build and run applications on multiple platforms, including MacOS, Windows, Linux, Android, iOS, and WebAssembly.

Here are the current/latest instructions on how to build and run Makepad applications.

## Assumptions

We will assume the following:
Name of application: `New_App`

It should be changed to any one of the existing example apps in the [*project-robius*](https://github.com/project-robius) repository.

## Build & Run Instructions

Follow step 1 commands below for initial setup of the Makepad build and run environment.
After step 2, you may choose any one or more of the platforms you're interested in building for.

## 1. Setup Makepad

Replace `projects` with your own directory name.

```
cd ~/projects
```

### Clone the Makepad repository

```
git clone https://github.com/makepad/makepad.git
```

or

```
git clone git@github.com:makepad/makepad.git
```

### Change to latest 'rik' branch (Optional)

```
git branch rik
```

### Install makepad subcommand for cargo

```
cd ~/projects/makepad
cargo install --path ./tools/cargo_makepad
```

### Install platform toolchains

```
rustup toolchain install nightly
```

## 2. Get Project

### Clone the `New_App` repo

```
git clone https://github.com/project-robius/New_App.git
```

or

```
git clone git@github.com:project-robius/New_App.git
```

## 3. Android Build

### Install Android toolchain (First time)

```
cargo makepad android install-toolchain
```

### Install app on Android device or Android emulator

Open either the Android emulator or connect to a real Android device
use `adb` command to make sure there's a single device connected properly, then install and run as below:

```
~/projects/New_App
cargo makepad android run -p New_App --release
```

The application will be installed and launch on either the emulator or device.

## 4. iOS Setup & Install

### Install IOS toolchain (First time)

```
xcode-select --install
cargo makepad apple ios install-toolchain
```

### Install app on Apple devivce or iOS simulator

### iOS Setup

For iOS, the process is slightly more complicated. The steps involved are:

1. Enable your iPhone's Developer Mode, please see instructions here: [Enable Developer Mode](https://www.delasign.com/blog/how-to-turn-on-developer-mode-on-an-iphone/)
1. Setup an Apple Developer account
1. Setup an empty skeleton project in XCode
    1. File -> New -> Project to create a new "App"
    1. Set the Product Name as **`NewApp`**  (used in --org later)
    1. Set the Organization Identifier to a value of your choice, for this example we will use **`rs.robius`**. (used in --app later)
    1. Setup the Project Signing & Capabilities to select the proper team account
1. In XCode, Build/Run this project to install and run the app on the simulator and device
1. Once the simulator and device has the "skeleton" app installed and running properly, then it is ready for Makepad to install its application.

### Makepad Install

We will run the `cargo makepad apple ios` command, similar to Android build above, but there are some 2 to 4 additional parameters that need to be filled in:

**`--org`**

First few parts of the organization identifier (which makes up the Bundle Identifier). Usually in the form of **com.somecompany** or **org.someorg**
This is the same value used to setup the initial skeleton app above. For this example:
> `rs.robius`

**`--app`**

The name of the application or the project. This is the same as the Product Name used to setup the initial skeleton app above. In this case:
> `NewApp`

**`--org-id`** (real-device only)

This is the <string> value of the ApplicationIdentifierPrefix <key> in the `**.mobileprovision` file located in the `~/Library/MobileDevice/Provisioning Profiles` directory.
It should be a 10 digit alphanumeric value.

**`--ios-version`** (OPTIONAL)

defaults to 17. Set it to 16 or other values if the device is not running iOS 17.

### Example

For this example, we have the Bundle Identifier of **`rs.robius.NewApp`**

### Install app on IOS simulator

```
cd ~/projects/New_App
cargo makepad apple ios --org=rs.robius --app=NewApp run-sim -p New_App --release
```

### Install app on IOS device

```
cd ~/projects/New_App
cargo makepad apple ios --ios-version=16 --org-id=<ORGIDVALUE> --org=rs.robius --app=NewApp run-device -p New_App --release
```

The application will be installed and launch on either the emulator or device.

## 5. WASM Build

*Coming Soon*

## 6. MacOS / PC

Although it is a mobile app, Makepad cross-platform means you may run it on desktops if you wish.

```
cd ~/projects/New_App
cargo run
```
