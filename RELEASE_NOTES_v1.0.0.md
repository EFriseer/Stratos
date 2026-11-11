# Stratos 1.0.0

First public release. Live atmosphere, lighting, colour, weather, graphics and AutoLOD control for **Microsoft Flight Simulator 2024 (Steam)**. Every change applies while you fly: no sim restart, no reloading a flight, nothing installed into the sim's folder. Made by [EFriseer](https://efriseer-games.org).

> **Tested only on the author's own PC and configuration.** It may not work for you, may look different, or may break after a sim update. Use it at your own risk (see `LICENSE.txt`).

## Downloads

| File | Use it if |
|---|---|
| **Stratos_1.0.0_x64-setup.zip** (recommended) | You want a normal install. Extract it and run `Stratos_1.0.0_x64-setup.exe`. It installs for your Windows account only (no administrator rights), adds a Start menu shortcut and an entry in Windows Apps, and an uninstaller that asks whether to keep your presets and screenshots. |
| **Stratos_1.0.0_portable.zip** | You want no installation. Extract the whole folder anywhere you can write to (for example `D:\Stratos`, not Program Files and not the sim's folder) and run `Stratos.exe`. Keep `Stratos.exe`, `stratos_core.dll`, `stratos-map.json` and `SimConnect.dll` together. Presets, screenshots and logs are created in the same folder. Delete the folder to remove it. |

Both are the same program and behave the same in the sim. Both keep a small settings file in your Windows user profile.

**Windows may show "Windows protected your PC".** The files are not signed with a paid certificate. Choose "More info", then "Run anyway". Only do this if you downloaded the files from this page.

## Requirements

- Windows 10 or 11, 64-bit
- Microsoft Flight Simulator 2024, Steam version, on DirectX 12
- If the sim runs as administrator, run Stratos as administrator too
- Stratos needs no ReShade and works alongside ReShade, the Steam overlay, RTSS and similar tools

## How it works

Stratos is two parts. The **app** is the window you use. **Stratos Core** is a small library the app loads into the running sim, which does the work: the post-processing pass, the atmosphere and weather values, the frame counter. Everything Stratos needs sits next to the app. When you close Stratos, or go back to a menu in the sim, the Core lets go of everything it changed and the sim is exactly as it was.

**Connecting.** Start Stratos and the sim in any order. Stratos waits until you are really flying (not in a menu, the world map or the hangar) and the flight has settled for about ten seconds, then loads the Core. The lights in the title bar show where it is: **Sim** (the sim is running), **Core** (Stratos Core is loaded; hover for details) and **Active Sky** (detected). A ring means "on its way", a lit light means connected, hollow means off, and amber means attention (hover for why). *Settings, Debug, Attach to the sim now* connects right away.

**Hold B** (or the "Hold to compare" button under the sky strip) to see the untouched sim while you hold it.

## The tabs

### Post Processing
The final image: exposure, contrast, highlights, shadows and midtones; warmth, tint, saturation and vibrance; split toning with a separate colour and strength for shadows and highlights; sharpen, local contrast and vignette. Works with every weather mode.

### Atmosphere
Engine-level sky values: Rayleigh and Mie scattering, sun halo tightness, atmosphere depth and falloff, particle distribution and scattering intensity, ozone absorption, and per-channel colour for the sky, the haze and the scene. Also sun intensity, sun colour temperature, auto-exposure bias and cirrus coverage and altitude.

### Weather and Time
- **Time:** a sun path chart with blue hour, sunrise, morning gold, solar noon, evening gold, sunset and dusk times. Set the date and time of day directly, or go back to live.
- **Live weather** stays the sim's own (or Active Sky's). Stratos changes the look on top of it.
- **Stratos preset** makes Stratos hold the weather: three cloud layers (base, top, density, coverage, spread), up to four wind layers with gusts, sea-level temperature and pressure, precipitation, lightning and snow depth. To use it, open the sim's weather panel once and choose any preset other than Live weather. Stratos then takes over, and follows along when you pick another preset in the sim. You can copy the current live weather into your own values with one click.

### Graphics
The sim's own Graphics menu, from outside the sim: anti-aliasing, DLSS and FSR modes, Reflex, frame generation and generated frames, V-Sync, frame limiter, terrain and objects level of detail, shadows, clouds, volumetrics, reflections, SSAO, traffic, vegetation and more. In a flight, changes go straight into the running sim where the sim allows it and the sim keeps them when it closes. Settings the sim only reads at start-up, and changes made while the sim is in a menu, are written to its file once the sim closes. With the sim closed they are written immediately.

### AutoLOD
Holds your target frame rate by raising and lowering the sim's **Terrain** and **Objects** level of detail while you fly.
- It watches the frame rate (frames shown, or frames rendered, your choice). When it stays under the target for the wait time, it lowers detail by one step. When there is room above the target for the longer wait, it raises detail again. Detail never goes outside the limits you set.
- Separate **target frame rate and limits for the ground, low altitude and high altitude.** The switch between low and high follows your height above the ground and has a small margin so it doesn't flip back and forth.
- **Step size:** fixed, or **dynamic**, where Stratos picks the size of each step (from one point up to your largest step) from how far the frame rate is from the target.
- Waits from 1 second, a pause after every change (adjustable, or off) and a calm period after raising, so it does not oscillate. The first 30 seconds of a flight are always left alone.
- A live readout shows the phase of flight, frame rate against target, the current values next to yours, and the latest changes.
- Your own values come back when you turn AutoLOD off, close Stratos, or close the sim. While it is on, the two level-of-detail sliders on the Graphics tab are held by AutoLOD.
- Set each target a little under your refresh rate or frame limit, otherwise AutoLOD cannot see room to raise detail.

### Overlay (frame counter)
Drawn over the sim's picture: frames shown and rendered per second, frame time, 1% and 0.1% lows, the sim's GPU time and load, which side is holding the frame back, and frame generation. Choose what to show, the font, size, colours, outline, shadow, background and position. HDR screens are supported (the counter's brightness is adjustable). It can be left out of screenshots.

### Presets
Eleven included looks: **Clear alpine**, **Golden hour**, **Misty morning**, **Nordic overcast**, **Realistic**, **Saharan dust**, **Summer haze**, **Thunderstorm front**, **Tropical showers**, **Winter snowfall** and **Default FS24** (everything back to the sim's own values). Save your own, or drop a preset file into the presets folder and it appears at once. Weather in a preset can be exported to the sim's own weather preset list.

### Screenshots
Press **Ctrl+Shift+S** (works inside the sim) or the camera button in the title bar. A clean PNG goes to the `screenshots` folder next to the app, with a small Stratos mark. In *Settings, Screenshots* you can change the key and the folder and turn the mark, the sound, the in-app popup and a Windows notification on or off.

### Settings
Units (feet or metres, temperature and so on), the clock, behaviour, screenshots, a Debug section (attach to the sim, reload the engine map, ask the sim, automatic attach, wait after flight load, draw post processing) and the connection details. Only one Stratos runs at a time.

## If something doesn't work

- Make sure the sim is on DirectX 12.
- Run Stratos as administrator if the sim does.
- After a sim update, Stratos may need an updated `stratos-map.json`. Check this page for a new release.
- Two logs sit next to Stratos: `stratos-app.log` and `stratos-core.log`. Attach both when you ask for help on the [Discord](https://discord.gg/uVhwXbFJGJ) or [open an issue](https://github.com/EFriseer/Stratos/issues), with your GPU, driver version and what you were doing.

## Also on Flightsim.to

Stratos can also be downloaded from **[Flightsim.to](https://flightsim.to/addon/118853/stratos-the-all-in-one-solution)**.

## Support

**Join the Discord for support, questions and ideas: https://discord.gg/uVhwXbFJGJ**

## Removing it

Portable: close Stratos and delete the folder. Installer: Windows Settings, Apps, Stratos, Uninstall.
