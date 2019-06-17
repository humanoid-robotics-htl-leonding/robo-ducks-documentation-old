# Max Research #

## What does .cppstyle do ##

It's a configuration file for some kind of cpp-formatter which isn't integrated into CLion so it doesn't affect us in any way. (We can use CLion integrated clang-format with .clang-format)

## toggleFullVisionFake ##

Changes a configuration file for HULK-architecture:
${BASEDIR}/home/configuration/location/default/tuhh_autoload.json

```js
{
  "moduleSetup" : "default", //{default, fullVisionFake, replay, oldWalking}
  "sharedObjects" : [
    {
      "sharedObject" : "Motion",
      "loglevel" : "info"
    },
    {
      "sharedObject" : "Brain",
      "loglevel" : "info"
    }
  ]
}
```

```js
{
  "moduleSetup" : "fullVisionFake", //{default, fullVisionFake, replay, oldWalking}
  "sharedObjects" : [
    {
      "sharedObject" : "Motion",
      "loglevel" : "info"
    },
    {
      "sharedObject" : "Brain",
      "loglevel" : "info"
    }
  ]
}
```

It basically tells the Hulks wether or not they should enable all vision functionality

## toolchain ##

* init  
    Initially creates a symlink from ~/naotoolchain/ to the {CodeRelease_Toolchain_Repo} (according to toolchain_type and toolchain_version)
* docker  
    Resets or creates docker-stuff for the HULKsCodeRelease
* list  
    Lists the current version of all toolchain_types
* select
    Creates a symlink from ~/naotoolchain/ to the {CodeRelease_Toolchain_Repo} (according to toolchain_type and toolchain_version)
* update
    Creates a symlink from ~/naotoolchain/ to the {CodeRelease_Toolchain_Repo} (according to toolchain_type and toolchain_version) (would also try to download the toolchains if the server still existed)

## upload ##

* Compiles the code with the toolchain
* Downloads logfiles from Nao
* Stops all processes related to the Hulks
* Restarts NaoQi
* Uploads file Target
* Restarts all processes previosly killed

## moduleSetup ##

Edits a config file for deployment to set which tuuhNao Modules to load (So it is basically useless)

## hardwareStatus ##

Updates a private HULKs Repo where information about the hardware of the NAOs is kept (SerialNum,....) (Useless)