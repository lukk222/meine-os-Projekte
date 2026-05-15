# GDI Screamer & Visualizer (Safe Version)

Hi! This is the harmless version of my GDI project. I have specifically rewritten the code to ensure it is absolutely safe. Unlike the other version, this one does NOT overwrite the MBR, and there are NO write operations to `sector0` or other critical files. It is purely a visual and auditory experiment.

The project was cross-compiled for Windows on a Mac using MacPorts.


## ⚠️ Epilepsy / Photosensitivity Warning
⚠️ Caution: This program generates rapidly flashing visual effects, intense colors, and chaotic screen animations using the Windows GDI API.

These effects may trigger seizures,
dizziness, or discomfort in individuals with photosensitive epilepsy or other visual sensitivities.
Please do NOT run this program under any circumstances if you:

-> suffer from photosensitive epilepsy
-> are sensitive to flashing lights or rapidly changing patterns
-> experience dizziness, nausea, or headaches in response to intense visual effects


If you choose to test the program regardless:

-> Run it only within a virtual machine (e.g., using VirtualBox or VMware Workstation).
-> Terminate the program immediately if you begin to feel unwell.
-> Do not use it in a dark room, and avoid using maximum screen brightness.

This project is intended solely for demonstration and experimentation purposes within the fields of graphics and systems programming.


## What does the program do?
When you launch the EXE, everything runs in the background (without an unsightly CMD window):
Using the GDI API, the screen is filled with wild shapes and circles until nothing is recognizable anymore.

As mentioned: As soon as you hard-reboot the VM or kill the process, everything returns to normal. No permanent damage.

## How was it built?
The code runs without the C standard library (`-nostdlib`) to keep the EXE size small and to utilize a custom entry point. The icon and sound are embedded directly within the file (except for the sound—the sound file is named "Aufnahme.wav" and must be located in the same folder as the program).

If you would like to build this yourself on a Mac, here are the commands:

1. **Package resources:**
```bash
/opt/local/bin/i686-w64-mingw32-windres ressourcen.rc ressourcen.o
```

2. **Compile (Universal 32-bit Windows):**
```bash
/opt/local/bin/i686-w64-mingw32-g++ -static -nostdlib -msse2 -mwindows -o programm.exe code.cpp ressourcen.o -lkernel32 -luser32 -lgdi32 -ladvapi32 -lwinmm -Wl,-e,_WinMainCRTStartup -Wl,--disable-stdcall-fixup -Wl,--subsystem,windows
```

Have fun testing it in your VM!
