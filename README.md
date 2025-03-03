# Superlithe: Forked from the GTNH 1.7.10 Example Forge Mod

A lightweight mod template for Minecraft 1.7.10 with RFGradle that's keeping it simple.

## Credit

Many thanks to [SinTh0r4s](https://github.com/SinTh0r4s), [TheElan](https://github.com/TheElan), [basdxz](https://github.com/basdxz), and all other contributors to the [original template](https://github.com/GTNewHorizons/ExampleMod1.7.10).

### Motivation

Superlithe attempts to provide a dead-simple build system for both new and experienced modders. Currently, it doesn't do that.

### Help! I'm stuck!

This project is *highly experimental*, and commits may brick things temporarily. For the time being, this template should not be used in serious projects. New mods should first consider using the [GTNH template](https://github.com/GTNewHorizons/ExampleMod1.7.10), which is very stable in comparison.

### Getting started

Creating mod from scratch:
1. If you know how, clone this repository. Those interested in a simplified workflow might prefer using the `Code > Download Zip` drop-down on the Github website.
2. Change the LICENSE file to your preferred software license (ignore this step if you're okay with using the MIT license). If you're unfamiliar with FOSS software licensing, scan [this article](https://en.wikipedia.org/wiki/Open-source_license) for an introduction.
3. Initializing your folder as a git repository is highly encouraged. If you have git installed, enter this at the command line: `git init; git commit --message "Initial Commit"`. If you're interested in sharing your mod's code through Github, see [this guide](https://docs.github.com/en/get-started/git-basics/managing-remote-repositories). 
4. Replace placeholder values in gradle.properties.
5. Rename the directories `/src/main/java/com/myname/mymodid/` to align with your `modGroup` property in gradle.properties. For example, if your `modGroup` is `com.johndoe.grassblocks-improved`, your source code should be under `/src/main/java/com/johndoe/grassblocks-improved/`.
6. If you're interested in using Scala in your mod, put Scala source files under `/src/main/scala/...`.
7. Rename classes to your liking (`*.java` files are all classes).
8. Run `./gradlew build`.
9. Check out the rest sections of this file.
10. When sharing your work publicly, remember to comply with the [Minecraft EULA](https://www.minecraft.net/en-us/eula). In a nutshell: selling your mod is verboten (all the more reason to share the source code for free!), and you should try to avoid using decompiled code by Mojang.
 
## Migration 

Migration from other Forge workspaces is not a current design priority. If you are interested in migration/porting to Superlithe, you are better suited porting to the [GTNH workspace](https://github.com/GTNewHorizons/ExampleMod1.7.10) and then Frankenstein-ing together your own bespoke build system with parts of this repository.

### Features

#### Unique to Superlithe
 - *crickets*
 
#### From GTNH
 - Optional API artifact (.jar)
 - Optional version replacement in Java files
 - Optional shadowing of dependencies
 - Simplified setup of Mixin and example
 - Scala support (add sources under `src/main/scala/` instead of `src/main/java/`)
 - Optional named developer account for consistent player progression during testing
 - Boilerplate forge mod as starting point
 - Improved warnings for pitfalls
 - Git Tags integration for versioning
 - [Jitpack](https://jitpack.io) CI
 - GitHub CI:
   - Releasing your artifacts on new tags pushed. Push git tag named after version (e.g. 1.0.0) which will trigger a release of artifacts with according names.
   - Running smoke test for server startup. On any server crash occurring workflow will fail and print the crash log.

### Goals
- [ ] Explanatory documentation inside most files for hackers and those new to Gradle
- [ ] Simplified/documented Gradle commands
- [ ] Overhauled `gradle.properties`
  - [ ] Distinguished required/non-required fields
  - [ ] GTNH-specific integration made more workflow-agnostic
- [ ] Stability improvements
  - [ ] Warnings when authors require compatibility-breaking mods
- [ ] Superlithe-specific contributions to the [legacy modding wiki](https://legacymoddingmc.github.io/wiki/).

### Files
 - [`gradle.properties`](https://github.com/GTNewHorizons/ExampleMod1.7.10/blob/main/gradle.properties): The core configuration file. It includes
 - [`dependencies.gradle[.kts]`](https://github.com/GTNewHorizons/ExampleMod1.7.10/blob/main/dependencies.gradle): Add your mod's dependencies in this file. This is separate from the main build script, so you may replace the [`build.gradle`](https://github.com/SinTh0r4s/ExampleMod1.7.10/blob/main/build.gradle) if an update is available.
 - [`repositories.gradle[.kts]`](https://github.com/GTNewHorizons/ExampleMod1.7.10/blob/main/repositories.gradle): Add your dependencies' repositories. This is separate from the main build script, so you may replace the [`build.gradle`](https://github.com/SinTh0r4s/ExampleMod1.7.10/blob/main/build.gradle) if an update is available.
 - [`jitpack.yml`](https://github.com/GTNewHorizons/ExampleMod1.7.10/blob/main/jitpack.yml): Ensures that your mod is available as import over [Jitpack](https://jitpack.io).

### Forge's Access Transformers

You may activate Forge's Access Transformers by defining a configuration file in `gradle.properties`.

Check out the [`example-access-transformers`](https://github.com/GTNewHorizons/ExampleMod1.7.10/tree/example-access-transformers) branch for a working example!

__Warning:__ Access Transformers are bugged and will deny you any sources for the decompiled minecraft! Your development environment will still work, but you might face some inconveniences. For example, IntelliJ will not permit searches in dependencies without attached sources.

### Mixins

Mixins are usually used to modify vanilla or mod/library in runtime without having to change source code. For example, redirect a call, change visibility or make class implement your interface. It's an advanced topic and most mods don't need to do that.

You can activate Mixin in 'gradle.properties'. In that case a mixin configuration (usually named `mixins.mymodid.json`) will be generated automatically, and you only have to write the mixins itself. Dependencies are handled as well.
Take a look at the examples in [Hodgepodge](https://github.com/GTNewHorizons/Hodgepodge/) and [Angelica](https://github.com/GTNewHorizons/Angelica/pull/8).

### Advanced

If your project requires custom Gradle commands you may add a `addon.gradle[.kts]` to your project. It will be added automatically to the build script. Although we recommend against it, it is sometimes required. When in doubt, feel free to ask us about it. You may break future updates of this build system!
If you need access to properties modified later in the buildscript, you can also use a `addon.late.gradle[.kts]`.
For local tweaks that you don't want to commit to Git, like adding extra JVM arguments for testing, use `addon[.late].local.gradle[.kts]`.

