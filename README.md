# SUN ROCK 1.0 RC
**ADVANCED STEAMVR INPUT SUPPORT FOR UE4.21**

REQUIRED: Update to OpenVR over Stock UE4.21 engine. Use included script to upgrade (no engine recompile necessary).

Run the "RUN_ME_ONCE-UpdateOpenVR.bat" script in a command line or Powershell. This script can be found in

{RepositoryLocation}/SunRock/Plugins/KnucklesLiveLink

## Overview:
Includes a Livelink Plugin for SteamVR's new Knuckles Streaming Hand Skeletal Data System and extends UE's SteamVR Controller to support the new Knuckles Controllers including autogeneration of Controller Binding files.

v1.0 adds direct controller support for Finger Curls and Splays.

For a "plugin only" project for use as a submodule in your projects, use this repo:
https://github.com/1runeberg/KnucklesLiveLink

## Preview Video:

[![v1.0 RC CHANGES](http://img.youtube.com/vi/4NLeZIMcyZw/0.jpg)](http://www.youtube.com/watch?v=4NLeZIMcyZw "Version 1.0 RC Changes")

[![KNUCKLES UE4 PLUGIN](http://img.youtube.com/vi/OBLxaObZBaY/0.jpg)](http://www.youtube.com/watch?v=OBLxaObZBaY "Knuckles UE4 Plugin Overview")

**Release Notes**
1.0 RC Release Candidate.
    + Adds support to read finger Curls and Splays direct from the controller (Knuckles)
    + Access to latest OpenVR API 1.2.10 using stock UE4 (not Engine compile necessary)
    + Demo: Gesture Recognition
    + Demo: Standard UE4 Hand skeletal mesh animation
    + Utility: Script that searches user's PC for a stock UE4 Engine, checks if latest OpenVR (1.2.10) is installed, if not, adds all necesary files to upgrade Engine's OpenVR to latest

0.5b Beta release. Open sourced under MIT License
     + Reimplement SteamVRController as KnucklesVRController
     + Auto-Generate SteamVRInput Bindings File from UE Action & Axis Mappings
     + Added Knuckles Runtime Component
     + Fixed Haptics
     + Refactored Code for Public Release
        - Retire Input Component in favor of new KnucklesVRController
        - Removed Knuckles to UE Skeletal Animation mapping 

0.2a Customisation of Skeletal Animation Feed during runtime, stability improvements
0.1a Initial early release

**SPECIAL NOTE ON RELEASE: From 0.5 beta onwards, during first Editor start, bindings and action manifest will be autogenerated. If during this initial session your bindings do not work, restart BOTH SteamVR and UE Editor, see section IV of instructions below for more details.**

## INSTRUCTIONS
**I. The Knuckles Livelink Plugin contain the following core modules:** <br />
    * Knuckles Livelink - For livelink feed of SteamVR hand skeletal animation<br />
    * Knuckles Livelink Runtime - For establishing Livelink Feed during runtime<br />
    * KnucklesVRController BP Library - For static functions related to SteamVRInput (e.g. Triggering Haptics)<br />
    * KnucklesVRController - Reimplemented SteamVRController from UE4.21 to support Knuckles and automated new SteamVR Input Bindings generation.<br />
    
**IMPORTANT:** 
1. If CVar vr.SteamVR.EnableVRInput = 1, KnucklesVRController will defer back to the original SteamVRController from the Engine.
2. You MUST use Action and Axis Mappings in your project (see Section IV of the Instructions below)<br /><br />

**II. Dependencies:** <br />
    * SteamVR Plugin<br />
    * Knuckles Livelink Plugin<br /><br />

**III. Livelink:** <br />
    Livelink can be used either in-Editor for testing Knuckles Hardware and/or Finger mocap recordings. 
    More information about how to use Livelink Plugins are documented here:<br />
    https://docs.unrealengine.com/en-us/Engine/Animation/Live-Link-Plugin<br /><br />

With the Livelink Runtime component, you can also use the Skeletal Hand Animation Feed from SteamVR during Runtime and for packaged projects.<br /><br />

**IV. Auto-Generation of SteamVRInput Bindings:** <br />
    The SteamVRController if active will auto-generate:<br />
        {ProjectDir}\Saved\Config\steamvr_actions.json (action manifest, Editor & Packaged)<br />
        {ProjectDir}\Config\SteamVRBindings\\{ControllerType}.json (bindings file, Editor only)<br /><br />
    
If the bindings files already exists, they won't be overwritten. To regenerate new ones delete any existing binsind and action manifest files and restart the Engine.<br /><br />

An Engine and SteamVR Restart is recommended everytime these files are changed.<br /><br />

{ControllerType}.json files are auto-generated if they don't exist with bindings from your project's Input Mappings (Settings > Project Settings > Engine > Input). Both Key & Axis Mappings are supported.<br /><br />

Autogeneration is based on best guess from the UE Mapping to what's an appropriate equivalent for a SteamVR Input binding. You can fine tune these bindings in SteamVR (Devices > Controller Input Binding) and publish as normal.<br /><br />

**V. Packaging/Publishing your Project:** <br />
1. After packaging your project as normal, copy:<br />
    from {Your UE Project Folder}\Plugins\KnucklesLiveLink to {Build Directory}\\..\\{Project Name} directory where your project's executable is. Don't forget to delete the Intermediate Folder.<br /><br />

    So should look something like this:
    E:/BUILDS/WindowsNoEditor/SunRock/KnucklesLiveLink

2. Also copy your Input Bindings:<br />
   from {Your UE Project Folder}\Config\SteamVRBindings to {Build Directory}\\..\\{Project Name}\Config\SteamVRBindings<br /><br />

    So should look something like this:
    E:/BUILDS/WindowsNoEditor/SunRock/Config/SteamVRBindings

The action manifest (steamvr_actions.json) will be autogenerated during runtime so there is no need to copy this file across your packaged project.<br />

3. Copy the old version of OpenVR (v1.0.16) from your stock engine to your project build. For example:

    From: E:/Program Files/Epic Games/UE_4.21/Engine/Binaries/ThirdParty/OpenVR

    To: E:/BUILDS/WindowsNoEditor/Engine/Binaries/ThirdParty/OpenVR

    The contents of the above directory MUST include BOTH of these:
    OpenVRv1_0_16
    OpenVRv1_2_10
   

**NOTE: To reset Action Manifest for UE4Editor to defaults:**

1. Go to "Program Files (x86)\Steam\config\steamvr.settings"
2. In there, will have a section called "system.generated.ue4editor.exe"
3. Delete this section to restore defaults 

Courtesy of: https://steamcommunity.com/id/lamboman007
Forum Post: https://steamcommunity.com/app/633750/discussions/0/1730963192554016903/

## Demo Project Requirements

1. Unreal Engine 4.21
2. Knuckles Hardware (EV2 or EV3)
3. SteamVR Beta
4. Steam Running and User Logged-In
5. Knuckles Livelink & Input System Plugin (binary included in this repo)
6. Pre-release 3.0.6 alpha version of RunebergVR Plugin (binary included and enabled in this repo)
7. Livelink Engine Plugin from Epic (included in 4.21, enabled in this repo)
8. SteamVR Engine Plugin (included in 4.21, enabled by default)
