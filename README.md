# EC Pro2

Open source HHKB Pro2 Controller and mainboard.

## **DEPRECATED**

Project deprecated in favor of the EC Pro X.

Please note that no further support will be provided, let alone give support for boards not sourced from my official runs or approved sources.

# EC PRO X Available for direct purchase!

If you want to buy directly and support my work you can now do it so [here](https://cannonkeys.com/products/cipulot-ec-pcbs-and-daughterboards).

## Introduction

This project is a continuation of my development of open source EC boards.

The supported layout options are the following:

![Layout option](/Assets/Layout_option.png)

## Technical information

### Mainboard

- Layout size: HHKB Pro2 ANSI and some additions
- Compatible switches: EC switches (Topre and NIZ)
- Microcontroller: STM32F401
- Connector: JST connector for controller board
- Firmware compatibility: QMK (with VIA/VIAL support)
- Protection hardware (present on both the mainboard and both controller versions):
  - Fused
  - ESD protection

### Lite Controller board

The Lite controller board is a slimmed down version of the controller board, featuring only protection hardware and a JST connector for the mainboard.

This is cost effective choice in case the user doesn't need the USB hub feature or the aftermarket case doesn't take advantage of it.

### Normal Controller board

The Normal Controller instead is a full featured controller board, featuring a USB hub, a JST connector for the mainboard and a USB Type-C connector for the PC.

The USB hub is a USB 2.0 hub, featuring 3 USB-A 2.0 ports, one of which is internal, to be used for dongles or small USB drives.

Key features of the Normal Controller are:

- USB 2.0 hub based on the FE1.1 IC
- 2x USB-A 2.0 ports in the same position as the original HHKB Pro 2
- 1x internal USB-A 2.0 port
- Per port current limit on each downstream port using MIC2026-2 for the 2 externally accessible USB ports.

**NOTES**

- The internal USB port is intended only for low power devices, such as dongles and small usb drives as previously mentioned. It is not intended for high power devices. Furthermore it is not ESD protected nor current limited and shares the power rail with the rest of the controller.

- The main USB-C port, as well as the 2x externally accessible USB-A downstream ports are ESD protected and current limited.

Keep in mind the the USB 2.0 power budget sets a typical current limit of **500mA**, therefore that is the total budget available to the entire board (controller + mainboard + devices connected to the hub).

## Renders and Prototypes

### Render

Mainboard:

![PCB Front Render](/Assets/PCB_render_front.png)

![PCB Back Render](/Assets/PCB_render_back.png)

Lite Controller board:
![Lite Controller Render](/Assets/lite_controller_render.png)

Normal Controller board:
![Normal Controller Render](/Assets/normal_controller_render.png)

### Prototypes

Mainboard:

![PCB Front](/Assets/PCB_front.png)

![PCB Back](/Assets/PCB_back.png)

Lite Controller:
![Lite Controller](/Assets/lite_controller.png)

Normal Controller:
![Normal Controller](/Assets/normal_controller.png)

## Revisions and relative features

### Rev1

This revision implements all the main features of the mainboard ad controllers mentioned in the specifications.

#### Connectivity

The Revision 1 (Rev1) implements a USB hub based on the FE1.1 USB HUB IC.

Connection to the PC is achieved through a USB-C connector while devices downstream will use USB-A ports.

Mind that the USB-C connector is wider than the original USB mini connector used, therefore modifications to enlarge the port cutout on the case will be needed. In case you will use this board in an aftermarket case already designed with USB-C in mind n o further modifications are needed.

#### RGB header

![RGB header](/Assets/rgb_header.png)

The mainboard features an RGB header for connecting +5V addressable RGB strips. THe properties of the lihting can be controlled through Vial or by assigning RGB control keycodes on the board itself.

On the bottom right corner of the PCB, near the bootloader instructions, a pinout diagram shows how to connect the strip to the header:

![RGB legend](/Assets/rgb_legend.png)

#### DFU

To access the DFU mode of the mainboard you can perform one of the following actions:

- press the key to which the `QK_BOOT` keycode is assigned (if available)
- while plugging in the board keep the `ESC` (top left corner key) pressed
- while plugging in the board short the `Boot0` pins on the mainboard

![Boot0 pins](/Assets/boot0_pins.png)

## PCB order procedure

In order to have me highers compatibility possible with PCB manufacturers, I decided to design the board around the [JLC7628 Stackup](https://cart.jlcpcb.com/impedance#:~:text=4%2DLayer%20Impedance%20Control%20Stackup) from JLCPCB.

The rational behind this is that the JCPCB stackup is relatively cheap and if the board worked with the stackup, it would be easier to get the board to work with pretty much any other many that offer an equivalent stackup and higher prices.

Both the `Lite` and `Normal` controllers can be instead be ordered with standard 2 layer stackup.

### Production files

The production can be found in the [Production folder](/Production).

As usual the `*.zip` files are the gerber files, `BOM-*.csv` are the BOM (Bill Of Material) files and `POS-*.csv` are the POS/CPL (Footprint POSition/Component Placement List) files.

## Mainboard

As mentioned above, the mainboard is designed around the JLCPCB stackup. The mainboard is a 4 layer board.

Here are the options to select when ordering the mainboard:

- PCB thickness: 1.6mm
- Impedance: NO
- Layer stackup:
  - L1(Top layer): `EC_Pro2_Mainboard-F_Cu.gbr`
  - L2(Inner layer1): `EC_Pro2_Mainboard-In1_Cu.gbr`
  - L3(Inner layer2): `EC_Pro2_Mainboard-In2_Cu.gbr`
  - L4(Bottom layer): `EC_Pro2_Mainboard-B_Cu.gbr`
- PCB Color: whatever you like
- Surface Finish: whatever you like
- Material Type: `FR-4 TG155`

All the other options can be left as default.

### Assembly options

Here follows the options to be used for assembly:

- Assembly Side: Bottom
- Tooling holes: `Added by JLCPCB`
- Confirm Parts Placement: `yes`

**USB-A connector**

An alternative part that has been tested and works is the `JINJIA USB-SMT-04F-S1-B1-R11` from [LCSC](https://www.lcsc.com/product-detail/USB-Connectors_JINJIA-USB-SMT-04F-S1-B1-R11_C718023.html).

As a general rule of thumb the USB-A connectors are interchangeable if they meet the following requirmemnts:

- fits the PCB outline
- has the same number of pins and mounting
- has the following receptor configuration

  ![USB-A receptacle](/Assets/usb_a_receptacle.png)

  To be more specific, the plastic part of the connector should be on the top and not the bottom.

  **BEWARE** that some USB-A connectors have the plastic part on the bottom, in this case the connector will have the pinout reversed, therefore causing inverse polarity on the USB lines.
  The following picture shows the correct orientation of the USB-A connector on the top board while the incorrect one on the bottom board:

  ![USB-A orientation](/Assets/usb_a_right_vs_wrong_orientation.png)

### NOTES ABOUT THE OPTIONS

- Once you upload the gerber files wait for the system to automatically recognize the board outline and layers. It will take a while, be patient.

- `PCB thickness` has been tested on both 1.6mm and 1.2mm so it's your call on which one to use.

- For `Material Type` I strongly suggest to use `FR-4 TG155`, using the standard `FR4-Standard TG130-140` material might result in the board delamination and generally is not advised on 4 layer boards.

## Compatibility notice

The EC Pro2 project is intended as a full replacement kit for the OEM HHKB Pro2 controller and main PCB. Therefore it **IS NOT** compatible with the OEM PCBs (both controller and mainboard).

## Copyright notice

This project is not endorse nor sponsored in any way by Topre Corporation and PFU Limited. The HHKB Logo and Topre logo are trademarks of their respective owners.

## License

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.
