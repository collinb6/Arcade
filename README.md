# Arcade Project

A retro arcade setup project using Neo Geo MVS hardware with modern video conversion capabilities.

## Overview

This project involves setting up a Neo Geo Multi Video System (MVS) arcade board with a supergun interface and video converter for use with modern displays.

## Components

### Core Hardware

1. **Neo Geo MVS 1FZ Motherboard**
   - The main arcade board that runs Neo Geo games
   - MVS (Multi Video System) format allows for multiple game cartridges
   - 1FZ model variant

2. **Sigma Raijin Supergun**
   - Interface device that allows arcade PCBs (like the Neo Geo MVS) to be used outside of an arcade cabinet
   - Provides power, video, and control connections
   - Enables home use of arcade hardware
   - **Video Output:** RGB via 8-pin U-DIN connector (labeled "RGB")
   - **Compatibility:** JAMMA standard (compatible with Neo Geo MVS boards)
   - **8-Pin RGB Pinout:** See connection section below for detailed pin assignments

3. **GBS 8200 Video Converter**
   - Converts arcade RGB video signals to VGA output
   - Allows connection to modern monitors and displays
   - Note: Does not accept SCART connections directly

4. **138 in 1 Multi Cart**
   - Multi-game cartridge containing 138 Neo Geo games
   - Requires dipswitch modification for proper operation

5. **NEC MultiSync LCD2690WUXi Monitor**
   - 25.5" professional LCD monitor with H-IPS panel
   - **Native Resolution:** 1920x1200 (16:10 aspect ratio)
   - **Inputs:** DVI-I, DVI-D, and VGA
   - Built-in resolution scaler with customizable screen expansion and aspect ratio options
   - Professional features: ColorComp for backlight uniformity, hardware gamma correction LUT
   - Fast response time suitable for gaming
   - Standard matte anti-glare coating
   - **Reference:** [NEC LCD2690WUXi Review](http://xtknight.50webs.com/lcd26/)

## Connection Setup

### Video Connection Chain

**Setup:** Sigma Raijin (8-pin RGB output) → GBS 8200 (RGB to VGA converter) → NEC LCD2690WUXi (VGA input)

**Monitor:** NEC MultiSync LCD2690WUXi (25.5", 1920x1200 native resolution)

### Sigma Raijin 8-Pin RGB Connector Pinout

The Sigma Raijin supergun has an 8-pin U-DIN connector labeled "RGB" on the back panel. **Important:** This pinout is different from the AV-7 model's 8-pin connector. Use this pinout for the Raijin RGB connector.

**Connector Labeling:**
- **SL** = Sound Left (Audio L)
- **SR** = Sound Right (Audio R)
- **SY** = Sync (Composite Sync / CSYNC)

If you see these labels (SL/SR/SY) on your connector, you've confirmed it's the RGB-capable mini-DIN, not the composite-only one.

**Pin Layout (viewing the male plug from the front, pins toward you, key notch up):**

```
          (key notch)
             ___
          .-'   '-.
         /  6  7  8 \
        |   3  4  5  |
         \    1  2   /
          '-._____.-'
```

**Pin Assignments:**

| Pin | Label | Function | Connects to GBS-8200 |
|-----|-------|----------|---------------------|
| 1 | SL | Audio Left | — (audio amp, not used for video) |
| 2 | GND | Ground | GND |
| 3 | SR | Audio Right | — (audio amp, not used for video) |
| 4 | +5V | +5V (for SCART switching) | — (not used) |
| 5 | G | Green | G (Green) |
| 6 | B | Blue | B (Blue) |
| 7 | R | Red | R (Red) |
| 8 | SY | Sync (CSYNC) | H-SYNC (or SYNC/S) |

**Reference:** [Arcade-Projects Forums](https://www.arcade-projects.com/)

### Direct Connection: Sigma Raijin to GBS-8200

The Sigma Raijin's 8-pin RGB connector already provides everything the GBS-8200 needs: R, G, B, and CSYNC. You can connect directly without needing SCART conversion.

**Wiring Connections Summary:**

```
R (Pin 7)  → R (Red)
G (Pin 5)  → G (Green)
B (Pin 6)  → B (Blue)
SY (Pin 8) → H-SYNC (or SYNC/S)
GND (Pin 2) → GND (Ground)
```

**Important:** Leave V-SYNC empty/unconnected. Don't use +5V (Pin 4).

**Important Notes:**
- **Use CSYNC on HSYNC input:** Connect the composite sync (pin 8) to the GBS-8200's HSYNC input
- **Leave VSYNC unconnected:** Most GBS-8200 units lock better to CSYNC than separate H+V sync
- **Use RGBS input block:** If your GBS-8200 has both a screw terminal RGBS block and a VGA-style RGBHV input, use the RGBS block
- **Pin numbering:** Be aware that some diagrams show the connector from the solder side, which can cause confusion. Pin 8 is sync on the RGB connector.

### Alternative: Using SCART Cable

If you prefer not to solder the 8-pin connector directly, you can:
1. Use a Sigma Raijin RGB SCART cable (available from RetroGamingCables, Otaku's Store, etc.)
2. Break out the SCART end to the GBS-8200 screw terminals
3. These cables are explicitly CSYNC and often include a 470Ω resistor on sync for compatibility

### GBS-8200 Connection Steps

1. **Connect RGB signals:**
   - Wire the 8-pin connector as described above to the GBS-8200's RGBS input block (typically labeled P11 or similar)
   - Ensure GND is properly connected

2. **GBS-8200 to Monitor:**
   - Connect the GBS-8200's VGA OUT (P4) to the NEC LCD2690WUXi's VGA input using a standard VGA cable
   - The monitor's built-in scaler will handle resolution conversion from the GBS-8200's output
   - Use the monitor's OSD to adjust aspect ratio and screen expansion as needed

3. **Power the GBS-8200:**
   - Connect a 5V DC power supply to the GBS-8200's power input (P7 or P9)

4. **Configuration:**
   - Power on the GBS-8200 and monitor
   - Use the On-Screen Display (OSD) menu to adjust image position, zoom, and output resolution

### Signal Level Considerations

**Sync Level / Termination:**
- Some GBS-8200 boards require proper sync termination
- If you get no lock or rolling picture, try adding a 100Ω resistor from SYNC to GND at the GBS input
- This helps with TTL-level sync signals that some devices output

**RGB Amplitude (Brightness):**
- Some Sigma Raijin outputs can be "too hot" for modern scalers
- If the picture is overbright or clipped, add series resistors:
  - ~220-330Ω on R, G, B lines
  - ~470Ω on sync line (often included in commercial SCART cables)

**Pin Numbering Confusion:**
- Be careful with pin numbering - some diagrams show the connector from the solder side
- Verify pin 8 is sync (CSYNC) on your specific connector
- Double-check the connector orientation before wiring

### Troubleshooting Checklist

**No picture at all:**
- Confirm you're using the GBS RGBS/RGB input, not composite
- Verify GND is properly connected
- Check that you're using the correct 8-pin RGB connector (not AV/S-Video port)

**Rolling / won't sync:**
- Ensure CSYNC is connected to HSYNC (not VSYNC)
- Try adding 100Ω resistor from SYNC to GND at the GBS input
- Verify pin 8 (CSYNC) is correctly wired

**Picture too bright / washed out:**
- Add series resistors on R/G/B lines (start with ~220-330Ω)
- Check RGB signal levels

**Colors wrong / swapped:**
- Verify pin order: Pin 5=Green, Pin 6=Blue, Pin 7=Red
- Check for swapped connections

**Reference:** Information compiled from Arcade-Projects Forums and GBS-8200 community documentation

## Setup Notes

1. Ensure proper power supply for the Neo Geo MVS board through the supergun
2. Configure dipswitches on the multi cart as needed
3. Connect controls (joystick/buttons) to the supergun
4. Resolve the video connection between supergun and GBS 8200
5. Connect GBS 8200 VGA output to your display

## Additional Resources

- Neo Geo MVS documentation and dipswitch settings
- GBS 8200 user manual for proper RGB input configuration
- Sigma Raijin supergun wiring diagrams
- **Cabinet Build Plans:** See `Cabinet_Build_Plans.md` for resources and plans for building a Neo Geo-style tabletop cabinet to house the 25.5" monitor

### Finding Sigma Raijin Supergun Documentation

If you need detailed specifications or a manual for the Sigma Raijin supergun, try:
- Check the physical unit for model numbers, serial numbers, or manufacturer labels
- Search arcade forums (Shmups Forum, Arcade-Projects, Neo-Geo.com)
- Check retro gaming communities and marketplaces
- Look for any included documentation or packaging
- Contact the seller or manufacturer if possible

## Project Status

- Components identified and listed
- Sigma Raijin 8-pin RGB pinout documented
- Direct connection method to GBS-8200 documented (no SCART adapter needed)
- Signal level considerations and troubleshooting guide included

