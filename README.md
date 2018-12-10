# SUN ROCK (0.5 beta)
**UE4 LIVELINK &amp; INPUT SYSTEM PLUGIN FOR STEAMVR KNUCKLES**

Includes a Livelink Plugin for SteamVR's new Knuckles Streaming Hand Skeletal Data System and a hook to the new Action Binding System to UE4's native Event System.

This demo project only works with UE4.21, SteamVR EV2 & EV3 Knuckles Hardware **AND** Steam **MUST** be running.

## Preview Video:

[![KNUCKLES UE4 PLUGIN](http://img.youtube.com/vi/DDu5W_b88N0/0.jpg)](http://www.youtube.com/watch?v=DDu5W_b88N0 "Knuckles UE4 Plugin Overview")


**Release Notes**
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
    
**IMPORTANT: If CVar vr.SteamVR.EnableVRInput = 1, KnucklesVRController will defer back to the original SteamVRController from the Engine.**<br /><br />

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
        <ProjectDir>\Saved\Config\steamvr_actions.json (action manifest, Editor & Packaged)<br />
        <ProjectDir>\Config\SteamVRBindings\<ControllerType>.json (bindings file, Editor only)<br /><br />
    
If the bindings files already exists, they won't be overwritten. To regenerate new ones delete any existing binsind and action manifest files and restart the Engine.<br /><br />

An Engine and SteamVR Restart is recommended everytime these files are changed.<br /><br />

<ControllerType>.json files are auto-generated if they don't exist with bindings from your project's Input Mappings (Settings > Project Settings > Engine > Input). Both Key & Axis Mappings are supported.<br /><br />

Autogeneration is based on best guess from the UE Mapping to what's an appropriate equivalent for a SteamVR Input binding. You can fine tune these bindings in SteamVR (Devices > Controller Input Binding) and publish as normal.<br /><br />

**V. For Packaged Projects:** <br />
After packaging your project as normal, copy:<br />
    from <Your UE Project Folder>\Plugins\KnucklesLiveLink to <Build Directory>\..\<Project Name> directory where your project's executable is. Don't forget to delete the Intermediate Folder.<br /><br />

Also copy your Input Bindings:<br />
   from <Your UE Project Folder>\Config\SteamVRBindings to uild Directory>\..\<Project Name>Config\SteamVRBindings<br /><br />

The action manifest (steamvr_actions.json) will be autogenerated during runtime so there is no need to copy this file across your packaged project.<br />

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
