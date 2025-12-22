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

3. **GBS 8200 Video Converter**
   - Converts arcade RGB video signals to VGA output
   - Allows connection to modern monitors and displays
   - Note: Does not accept SCART connections directly

4. **138 in 1 Multi Cart**
   - Multi-game cartridge containing 138 Neo Geo games
   - Requires dipswitch modification for proper operation

## Connection Setup

### Video Connection Issue

**Current Status:** There is a known connection challenge:
- RGB to SCART lead is available that fits the Sigma Raijin supergun
- However, the GBS 8200 video converter does not accept SCART connections
- A solution is needed to bridge the RGB/SCART output from the supergun to the VGA input of the GBS 8200

### Recommended Solution

To connect the supergun to the GBS 8200, you will need:
- An RGB to VGA adapter/converter, OR
- A direct RGB cable (not SCART) that connects to the GBS 8200's RGB input
- Alternatively, use a SCART to RGB breakout adapter to extract the RGB signals from the SCART connector

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

## Project Status

- Components identified and listed
- Video connection issue documented
- Awaiting resolution of RGB/SCART to GBS 8200 connection

