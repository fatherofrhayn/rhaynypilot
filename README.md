Table of Contents
=======================

* [Read Before Installing](#-read-before-installing-)
* [Highlight Features](#-highlight-features)
* [Driving Enhancement](#-driving-enhancement)
* [How-Tos](#-How-Tos-)
* [Special Thanks](#-special-thanks)
* [Licensing](#licensing)

---


🚨 Read Before Installing 🚨
---


DONT USE THIS - THIS IS JUST FOR PERSONAL USE - IM 13 YEARS OLD!!

Hi I'm Rhayn. This fork is NOT recommended to be used, I am learning to code with my dad. This for is for Hyundai/Kia/Genesis. This is a fork of Sunny Haibin's fork of [comma.ai's openpilot](https://github.com/commaai/openpilot). By installing this software, you accept all responsibility for anything that might occur while you use it. All contributors to this fork are not liable. <ins>**Use at your own risk.**</ins>

🚗 Highlight Features
---

### Driving Enhancement
* [**Modified Assistive Driving (MAD)**](#modified-assistive-driving-mad) - openpilot Automatic Lane Centering (ALC) and Adaptive Cruise Control (ACC) / Smart Cruise Control (SCC) can be engaged independently of each other
* [**Dynamic Lane Profile (DLP)**](#dynamic-lane-profile-dlp) - Dynamically switch lane profile base on lane recognition confidence
* [**Enhanced Speed Control**](#enhanced-speed-control) - Utilizes data from vision or OpenStreetMap to achieve dynamic speed control without user's intervention
* **No Disengage on Gas** - Allow the gas pedal press to not disengage openpilot. This feature is enabled by default.
* **Quiet Drive 🤫** - Toggle to mute all notification sounds (excluding driver safety warnings)
* **Auto Lane Change Timer** - Set a timer to delay the auto lane change operation when the blinker is used. No nudge on the steering wheel is required to auto lane change if a timer is set
* **Force Car Recognition (FCR)** - Use a selector to force your car to be recognized by openpilot
* **Fix openpilot No Offroad** - Enforce openpilot to go offroad and turns off after shutting down the car. This feature fixes non-official devices running openpilot without comma power
* **Enable ACC+MAD with RES+/SET-** - Engage both ACC and MAD with a single press of RES+ or SET- button

### Visual Enhancement
* **M.A.D. Status Icon** - Dedicated icon to display M.A.D. engagement status
* **Lane Color** - Various lane colors to display real-time Lane Model and M.A.D.S. engagemenet status
* **Developer (Dev) UI** - Display various real-time metrics on screen while driving
  * Click on the "MAX" box on the top left of the openpilot display to toggle different metrics display
* **Stand Still Timer** - Display time spent at a stop with M.A.D.S engaged (i.e., at a stop lights, stop signs, traffic congestions)
* **Braking Status** - Current car speed text turns red when the car is braking by the driver or ACC/SCC

### Operational Enhancement
* **Fast Boot** - openpilot will fast boot by creating a Prebuilt file
* **Disable Onroad Uploads** - Disable uploads completely when onroad. Necessary to avoid high data usage when connected to Wi-Fi hotspot
* **Brightness Control (Global)** - Manually adjusts the global brightness of the screen
* **Driving Screen Off Timer** - Turn off the device screen or reduce brightness to protect the screen after car starts
* **Driving Screen Off Brightness (%)** - When using the Driving Screen Off feature, the brightness is reduced according to the automatic brightness ratio
* **Max Time Offroad** - Device is automatically turned off after a set time when the engine is turned off (off-road) after driving (on-road)

🚗 Driving Enhancement
---

### Modified Assistive Driving (MAD)
The goal of Modified Assistive Driving Safety (MAD) is to enhance the user driving experience with modified behaviors of openpilot engagements. This feature complies with comma.ai's safety rules as accurately as possible with the following changes:
* openpilot Automatic Lane Centering and ACC/SCC can be engaged independently of each other
* Dedicated button to toggle openpilot ALC:
  * `LFA` button: Newer HKG cars
* `SET-` button enables ACC/SCC
* `CANCEL` button only disables ACC/SCC
* `CRUISE (MAIN)` must be `ON` to use MADS and ACC/SCC
* `CRUISE (MAIN)` button disables openpilot completely when `OFF` (strictly enforced in panda safety code)
* `BRAKE pedal` press NOT will pause openpilot Automatic Lane Centering; `BRAKE pedal` release will NOT resume ACC/SCC without an explicit entry
* `GAS pedal` press will NOT disengage openpilot Automatic Lane Centering or ACC/SCC
* `TURN SIGNALS` (`Left` or `Right`) will NOT pause openpilot Automatic Lane Centering if the vehicle speed is below the threshold for openpilot Automatic Lane Change
* Event audible alerts are more relaxed to match manufacturer's stock behavior

### Dynamic Lane Profile (DLP)
Dynamic Lane Profile (DLP) aims to provide the best driving experience with staying within the lane confidently. Dynamic Lane Profile allows openpilot to dynamically switch between lane profiles base on lane recognition confidence level on road.

There are 3 modes to select on the onroad camera screen:
* **Auto Lane**: openpilot dynamically chooses between `Laneline` or `Laneless` model
* **Laneline**: openpilot uses Laneline model only.
* **Laneless**: openpilot uses Laneless model only.

To use Dynamic Lane Profile, do the following:
```
1. openpilot Settings -> Toggles -> Disable use of lanelines -> ON toggle
2. Reboot.
3. Before driving, on the onroad camera screen, toggle between the 3 modes by pressing on the button.
4. Drive. 
```

### Enhanced Speed Control
This fork now allows supported cars to dynamically adjust the longitudinal plan based on the fetched map data. Big thanks to the Move Fast team for the amazing implementation!

**Supported cars:**
* openpilot Longitudinal Control capable
* Stock Longitudinal Control
  * Hyundai/Kia/Genesis

Certain features are only available with an active data connection, via:
* [comma Prime](https://comma.ai/prime) - Intuitive service provided directly by comma, or;
* Personal Hotspot - From your mobile device, or a dedicated hotspot from a cellular carrier.

**Features:**
* Vision-based Turn Control - Use vision path predictions to estimate the appropriate speed to drive through turns ahead - i.e., slowing down for curves
* Map-Data-based Turn Control - Use curvature information from map data to define speed limits to take turns ahead - i.e., slowing down for curves
  * **Note: Require data connection**
* Speed Limit Control - Use speed limit signs information from map data and car interface to automatically adapt cruise speed to road limits
  * **Note: Require data connection**
    * Speed Limit Offset - When Speed Limit Control is enabled, set speed limit slightly higher than the actual speed limit for a more natural drive
      * **Note: Require data connection**
* Hands on Wheel Monitoring - Monitor and alert when driver is not keeping the hands on the steering wheel

**Instruction**

**📗 How to use Custom Longitudinal Control on sunnypilot 📗**

When using Speed Limit Control, Vision or Map based Turn control, you will be setting the "MAX" ACC speed on the openpilot display instead of the one in the dashboard. The car will then set the ACC setting in the dashboard to the targeted speed, but never exceeding the max speed set on the openpilot display. A quick press of the RES+ or SET- buttons will change this speed by 5 MPH or KM/H on the openpilot display, while a long deliberate press (about a 1/2 second press) changes it by 1 MPH or KM/H. DO NOT hold the RES+ or SET- buttons for longer that a 1 second. Either make quick or long deliberate presses only.

**‼ Where to look when setting ACC speed ‼**

Do not look at the dashboard when setting your ACC max speed. Instead, only look at the one on the openpilot display, "MAX". The reason you need to look at the openpilot display is because openpilot will be changing the one in the dashboard. It will be adjusting it as needed, never raising it above the one set on the openpilot display. ONLY look at the MAX speed on the openpilot display when setting the ACC speed instead of the dashboard!

(Courtesy instructions from John, author of jvePilot)

📗 How Tos 📗
---

How-To instructions can be found in [HOW-TOS.md](https://github.com/sunnyhaibin/openpilot/blob/(!)README/HOW-TOS.md).

💰 Donate 💰
---

If you find any of the features useful, feel free to donate to Sunny Haibin and the other contributors below for future feature development.


🏆 Special Thanks
---

* [spektor56](https://github.com/spektor56/openpilot)
* [rav4kumar](https://github.com/rav4kumar/openpilot)
* [mob9221](https://github.com/mob9221/opendbc)
* [briantran33](https://github.com/briantran33/openpilot)
* [Aragon7777](https://github.com/aragon7777/openpilot)
* [sshane](https://github.com/sshane/openpilot-installer-generator)
* [jung](https://github.com/chanhojung/openpilot)
* [dri94](https://github.com/dri94/openpilot)
* [JamesKGithub](https://github.com/JamesKGithub/FrogPilot)
* [twilsonco](https://github.com/twilsonco/openpilot)
* [martinl](https://github.com/martinl/openpilot)
* [multikyd](https://github.com/openpilotkr)
* [Move Fast GmbH](https://github.com/move-fast/openpilot)
* [dragonpilot](https://github.com/dragonpilot-community/dragonpilot)
* [neokii](https://github.com/neokii/openpilot)
* [sunnyhaibin](https://github.com/sunnyhaibin/openpilot)



Licensing
------

openpilot is released under the MIT license. Some parts of the software are released under other licenses as specified.

Any user of this software shall indemnify and hold me and my family, employees, agents, stockholders, affiliates, subcontractors and customers from and against all allegations, claims, actions, suits, demands, damages, liabilities, obligations, losses, settlements, judgments, costs and expenses (including without limitation attorneys’ fees and costs) which arise out of, relate to or result from any use of this software by user.

**THIS IS ALPHA QUALITY SOFTWARE FOR RESEARCH PURPOSES ONLY. THIS IS NOT A PRODUCT.
YOU ARE RESPONSIBLE FOR COMPLYING WITH LOCAL LAWS AND REGULATIONS.
NO WARRANTY EXPRESSED OR IMPLIED.**

---

<img src="https://d1qb2nb5cznatu.cloudfront.net/startups/i/1061157-bc7e9bf3b246ece7322e6ffe653f6af8-medium_jpg.jpg?buster=1458363130" width="75"></img> <img src="https://cdn-images-1.medium.com/max/1600/1*C87EjxGeMPrkTuVRVWVg4w.png" width="225"></img>

[![openpilot tests](https://github.com/commaai/openpilot/workflows/openpilot%20tests/badge.svg?event=push)](https://github.com/commaai/openpilot/actions)
[![Total alerts](https://img.shields.io/lgtm/alerts/g/commaai/openpilot.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/commaai/openpilot/alerts/)
[![Language grade: Python](https://img.shields.io/lgtm/grade/python/g/commaai/openpilot.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/commaai/openpilot/context:python)
[![Language grade: C/C++](https://img.shields.io/lgtm/grade/cpp/g/commaai/openpilot.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/commaai/openpilot/context:cpp)
[![codecov](https://codecov.io/gh/commaai/openpilot/branch/master/graph/badge.svg)](https://codecov.io/gh/commaai/openpilot)
