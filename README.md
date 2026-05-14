# GDI Screamer & Visualizer (Safe Version)

Hi! Das hier ist die harmlose Version meines GDI-Projekts. Ich habe den Code extra so umgeschrieben, dass er absolut sicher ist. Im Gegensatz zu der anderen Version wird hier KEIN MBR überschrieben und es gibt KEINE Schreibzugriffe auf `PhysicalDrive0`. Es ist ein reines visuelles und akustisches Experiment.

Das Projekt wurde auf einem Mac via MacPorts für Windows cross-kompiliert.

## Was macht das Programm?
Wenn du die EXE startest, läuft alles im Hintergrund ab (ohne hässliche CMD-Box):
1. Die eingebettete `Aufnahme.wav` ballert in einer Endlosschleife los.
2. Über die GDI-API wird der Bildschirm mit wilden Formen und Kreisen vollgezeichnet, bis man nichts mehr erkennt.

Wie gesagt: Sobald du die VM hart neustartest oder den Prozess killst, ist alles wieder komplett normal. Keine bleibenden Schäden.

## Wie wurde es gebaut?
Der Code läuft ohne C-Standardbibliothek (`-nostdlib`), damit die EXE klein bleibt und der eigene Einstiegspunkt genutzt wird. Icon und Sound stecken direkt in der Datei.

Falls du es selbst auf dem Mac nachbauen willst, hier sind die Befehle:

1. **Ressourcen verpacken:**
   ```bash
   /opt/local/bin/i686-w64-mingw32-windres ressourcen.rc ressourcen.o
   ```

2. **Kompilieren (Universelles 32-Bit Windows):**
   ```bash
   /opt/local/bin/i686-w64-mingw32-g++ -static -nostdlib -msse2 -mwindows -o programm.exe code.cpp ressourcen.o -lkernel32 -luser32 -lgdi32 -ladvapi32 -lwinmm -Wl,-e,_WinMainCRTStartup -Wl,--disable-stdcall-fixup -Wl,--subsystem,windows
   ```

Viel Spaß beim Testen in der VM!
