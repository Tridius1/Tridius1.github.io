---
layout: page
title: "Grebe Hardware Volume Mixer"
subtitle: "A solution to allow use Windows voume mixer while fullscreen applications are open, using arduino hardware."
date: 2026-06-30
thumbnail: "/assets/images/grebe_thumbnail.jpg"
github_link: "https://github.com/Tridius1/Grebe"
---



### The Challenge
While open source software for using arduino hardware to interface with the Windows volume mixer already exists (notably [deej](https://github.com/omriharel/deej)), it is limited by the use of hardware sliders which are necessarily limited in number and cannot react to the Windows audio mixer being adjusted manually. This project instead uses rotary encoders in conjunction with a small screen to allow greater flexibility, dynamic reactions, and provides real time information to the user.

### Process
As the sole developer, I engineered Grebe from the ground up, dividing the project into two distinct domains: a lightweight background Windows daemon and the embedded microcontroller firmware.

* **Hardware & Firmware:** I designed the physical interface using an ESP32 DEVKIT V1, EC11 rotary encoders, and a DIYables LCD. The firmware, written in C++, is responsible for debouncing the physical inputs, updating the local UI, and establishing a fast, reliable serial connection to the host PC.

* **Systems Programming (Daemon):** I built the Windows daemon in Rust to ensure memory safety, speed, and portability. The daemon hooks into the Windows Core Audio API (WASAPI) to intercept and inject volume commands. It is responsible for listening to both user inputs, forwarded by the hardware, and Windows audio events to maintain the state of the mixer and inform the hardware so that state can be displayed. 

* **Resilience & UX:** A major focus of the process was bulletproofing the user experience. I implemented a named system Mutex to handle single-instance locking, preventing overlapping audio hooks if the user accidentally launched the app twice. Additionally, I engineered a robust reconnection loop that allows the Rust daemon to gracefully handle broken serial pipes and hotplugging of the hardware.

* **Tech Stack:** Rust (Windows API, Serial I/O), C++ (Embedded/ESP32), Hardware Prototyping

* **Duration:** 4 weeks

### The Result
The final outcome is a highly portable, zero-configuration hardware volume mixer. The project was successfully shipped as a v1.0.0 release containing pre-compiled binaries for both the .exe Windows daemon and the .bin ESP32 firmware, allowing end-users to flash their hardware and run the software without needing to install language toolchains or compile from source.

Grebe runs silently in the background, consuming minimal system resources while providing instantaneous, tactile control over the Windows audio environment.


#### License

* **Source Code:** The software logic of this project is licensed under the [MIT License](https://mit-license.org/).
* **Project Thumbnail:** The file `/assets/images/grebe_thumbnail.jpg` is a derivative work based on "[Great Crested Grebe (Podiceps cristatus)](https://www.flickr.com/photos/rainbirder/4722390714/)" by Steve Garvie, used under [CC BY-SA 2.0](https://creativecommons.org). This modified version is licensed under the [Creative Commons Attribution-ShareAlike 2.0 Generic (CC BY-SA 2.0)](https://creativecommons.org) license by [Tristan Swanson/Tridius1].
