<p align="center">
  <img src="Freddie_Calibration_Logo.jpg" width="100%" alt="Freddie Calibration Companion tool" />
</p>

# Freddie Calibration Assistant

An independent, offline-capable calibration journal for Primera Freddie that can
also read FreddieView's log and edit its settings file.
Open `index.html` or visit the GitHub Pages site. No build step or dependencies.

## What it does

- **Run journal with one next step.** Record each calibration or icing trial
  and get one prioritized recommendation. Batch history stays in browser local
  storage; export JSON backups regularly.
- **Reads the FreddieView log** (`C:\ProgramData\PTI\FreddieVision\FreddieVision.log`).
  For each day you get calibration readings plotted against flood pressure, cookies iced,
  icing used per cookie, the settings in effect for each cookie, setting changes,
  factory resets, and machine/camera faults with what to do about them.
- **Edits FreddieView's settings** (`Persistence\visionsettingsWorkingCopy.json`):
  flood pressure, outline pressure, relative icing amount and distance from edge.
  Only those numbers change; every other byte of the file is left as-is. Each save
  comes with a command that backs up the current file to `FreddieVision\CalibratorBackups`
  first, and **Download previous version** gives back the file from before your last save.
- **Smarter pressure steps.** FreddieView says "too thin, decrease pressure" when a
  reading is above its pass window (0.19–0.29" by default, read from `settings.json`)
  and "too thick, increase" below it. The companion brackets between the highest
  pressure that read too thick and the lowest that read too thin and suggests the midpoint.
- **Reliability check.** If readings contradict each other (too thick at a higher
  pressure than one that read too thin, or readings over 1"), it stops recommending
  more calibration and suggests trial & error instead.
- **Trial & error mode.** Skip calibration: ice one cookie, record what you see
  (runs over edge, gaps, spiral lines, pooling, thin or bleeding outline…) and the
  companion changes one setting per cookie.

## Using it on the Freddie PC

The app has three tabs: **1 Setup**, **2 Calibrate**, **3 Log insights**.

1. Open the site on the Windows PC that runs FreddieView.
2. On **Setup**, click **Choose…** next to each file. The file's full path is copied for
   you; in the Open window click **File name**, press Ctrl+V, then Enter (this works even
   though `C:\ProgramData` is hidden).
   - Settings file: `C:\ProgramData\PTI\FreddieVision\Persistence\visionsettingsWorkingCopy.json` (needed to change settings)
   - Log: `C:\ProgramData\PTI\FreddieVision\FreddieVision.log`
   - Optional: `Persistence\FrostingCal.Bipart.json`, `Persistence\settings.json`
3. **Close FreddieView before saving settings.** Saving downloads the updated
   `visionsettingsWorkingCopy.json` and shows a one-line PowerShell command that backs up
   the current file to `FreddieVision\CalibratorBackups` and copies the new one into place.
   Reopen FreddieView; it reads the file at start-up.

Why a download instead of saving in place: browsers block web pages from writing anywhere
under `C:\ProgramData` (Chromium's File System Access blocklist), so the companion never
writes there itself.

Editing FreddieView's files is not supported by Primera. Keep the backups, and use
Download previous version or FreddieView's Restore Defaults if anything looks wrong. This app does not talk
to Freddie. Disconnect power before maintenance.

## Credits

Created by Ed Wolf ([github.com/digitalducktape](https://github.com/digitalducktape)) for
the kitchen at City Gal Bakes. See what Freddie is icing at [CityGalBakes.com](https://citygalbakes.com).

## GitHub Pages

In repository Settings → Pages, choose Deploy from a branch, `main`, `/ (root)`.
The root `index.html` is the application. No uploaded manuals or private batch
records are included in this repository.

## Use The Tool
The tool can be accessed here:
https://digitalducktape.github.io/Freddie-Calibrator/
