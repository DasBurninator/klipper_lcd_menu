# Klipper LCD Menu

A custom menu system for LCD displays on klipper such as a 12864LCD screen.
Intended to extend the functionality beyond the default klipper LCD menu provides, while being printer agnostic.
Layout is organized into what I would consider a more logical workflow.

## InstalL

```
mkdir -p $HOME/printer_data/config/menu && git clone https://github.com/DasBurninator/klipper_lcd_menu $HOME/printer_data/config/lcd_menu
```

Add the following to `printer.cfg`:

`[include ./lcd_menu/lcd_menu.cfg]`

## Updates

### Manual Update

```
cd $HOME/printer_data/config/
git pull
```

### Moonraker Update Manager

Updates require that Moonraker is run in debug mode for unofficial repos. See the Moonraker documentation below:
[Enabling debug mode in Moonraker](https://moonraker.readthedocs.io/en/latest/installation/#the-environment-file)

Once Moonraker is running in debug mode the follow can be added to the `moonraker.conf file`

```
[update_manager client klipper_lcd_menu]
type: git_repo
channel: dev
primary_branch: main
path: ~/printer_data/config/lcd_menu
origin: https://github.com/DasBurninator/klipper_lcd_menu
managed_services: klipper
```

## Menu Layout

+ Prep (Disabled When Printing)
  + Prep ABS
  + Prep PLA
  + Z Tilt > Park
  + QGL > Park
  + Park
  + Park Rear
+ Print (Enabled During Printing)
  + Resume printing
  + Pause printing (Enabled During Printing)
  + Cancel printing (Enabled During Printing)
+ Tune (Enabled During Printing)
  + Offset Z:00.00
  + Flow: 000%
  + Speed: 000%
  + Fan speed: 000%
  + Retraction
  + Pressure Advance
  + Machine Limits
+ Control (Disabled When Printing)
  + Homing
    + Home All
    + Home Z
    + Home X/Y
    + Z Tilt
    + Quad Gantry Lvl
    + Bed Mesh
  + Move
    + Move 10mm
      + Move X:000.0
      + Move Y:000.0
      + Move Z:000.0
      + Move E:+000.0
    + Move 1mm
      + Move X:000.0
      + Move Y:000.0
      + Move Z:000.0
      + Move E:+000.0
    + Move 0.1mm
      + Move X:000.0
      + Move Y:000.0
      + Move Z:000.0
      + Move E:+000.0
  + Steppers off
  + Fan: OFF
  + Fan speed: 000%
  + KlickyProbe
    + Attach Probe
    + Dock Probe
+ Temperature
  + Ex0:000 (0000)
  + Ex1:000 (0000)
  + Bed:000 (0000)
  + Preheat PLA
    + Preheat all
    + Preheat hotend
    + Preheat hotbed
  + Preheat ABS
    + Preheat all
    + Preheat hotend
    + Preheat hotbed
  + Cooldown
    + Cooldown all
    + Cooldown hotend
    + Cooldown hotbed
+ Filament
  + Ex0:000 (0000)
  + Load Filament
  + Unload Filament
  + Purge Filament
  + Feed: 000.0
+ Setup
  + Save config
  + Restart
    + Restart host
    + Restart FW
+ Calibration (Disabled When Printing)
  + PID Tune
    + PID Tune ABS (tunes both bed and extruder for ABS temps)
    + PID Tune PLA (tunes both bed and extruder for PLA temps)
    + Ex0 PID
    + Bed PID
    + Save Config
+ Network
  + mDNS
  + Eth IP
  + Wifi SSID
  + Wifi IP

## Changelog

### Feb 9th 2023

+ Initial set of commits and debugging
+ Added network_status plugin menu options (conditional that plugin is enabled)
+ firmware_retraction and pressure_advance tuning menus now conditional of those options being enabled.
+ Completely reorganized the Control Menu
  + Added Homing menu and moved Home/Z-tilt/QGL/etc into this menu
  + Added Move menu and moved Move 0.1mm/1mm/10mm menus under this
  + Disabled Lighting Controls