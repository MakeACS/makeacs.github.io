---
icon: lucide/circuit-board
---

# 2. Hardware

## Hardware Overview

The MakeACS hardware is what enables the system to control machine-level access, track usage of the shops, and automatically generate maintenance tasks based on usage. 

MakeACS hardware is a modular, shared-bus system; multiple individual components can be interconnected to tailor the hardware to the application at hand. Each component is self-contained and in most cases does not require any specialized training or skills to integrate with the equipment. 

The MakeACS bus is standardized and easy to integrate into your own device, so you can easily make your own components to suit any need that the already-existing hardware does not. 

## The Core

The Core is the heart of a MakeACS deployment. It is where the end-user interacts with the system, and is how the deployment communicates with the server. 

All Cores are equipped with both a 2.4GHz Wi-Fi radio, and a 100Mbps Ethernet connection, to communicate with the server. 

There are multiple different styles of Core, depending on the intended application, and how your shop identifies users. In most applications, MakeACS uses your already-issued university ID card to identify the user, with hardware supporting NFC (13.56MHz, all generations up to DESFire EV3) and RFID (125KHz, FSK or ASK, up to 39 byte identifier length). Hardware supports either *tapping* the ID card to start an equipment session, which decays on a timer, or *inserting* the card, and the equipment stays online as long as the card is present.

The Core has a basic RGB LED and buzzer for communicating state, but also has an open-ended connection interface to allow for a display module.

In the event of a network outage, the Core can continue to operate based on an offline list of previously-approved users, for up to 30 days.

## The Switch

The Switch is the part of the access control hardware that actually controls access. There are a number of switches developed for MakeACS, depending on the piece of equipment in use. Multiple switches can also be used together, to form more complex access control setups all from a single card reader.

In most cases, the switch is also where the MakeACS deployment harvests power from, so there is usually no need for an additional power cable or connection. This allows the deployment to be mounted wherever is best for accessability and ergonomics, with no need to worry about additional cables.

### AC Power Switch

The AC Power Switch is by far the most popular MakeACS switch. It simply goes inline between the outlet on the wall and your equipment's power cable. There is no need for any invasive in-machine wiring or doing your own AC connections. 

The AC Power Switch is rated for highly inductive loads, and can handle a sustained 20A. This makes it ideal for anything from a sewing machine to a bandsaw.

The switch will monitor for any faults such as over-temperature, or blown fuses, and can also be configured to not allow a machine to be activated if it is detected to be in the "on" state. 

### USB Hub Switch

For a lot of complex equipment, the easiest way to control access to it is by locking down its computer. This strategy works great on laser cutters, water jets, and CNC machines. For this, the USB Hub Switch is a great fit. The switch will activate or de-activate 4 downstream USB ports for keyboards, mice, USB drives, etc.

The USB Hub Switch has a 5th downstream USB port that is connected when the switch is off, which can be used to automatically execute a cleanup script. For instance at RIT, when a user removes their ID card from a laser cutter's computer, it will go through and force-close all windows, make sure the user is logged out of any accounts, etc., before restarting the laser cutter software to give a blank slate to the next user. 

### Relay Switch

For applications that require more direct integration with equipment, the Relay Switch is the best choice. The relay switch provides galvanically isolated dry contacts, that can be integrated with any arbitrary power or signal to control a piece of equipment. Common examples include interrupting an interlock or e-stop loop, or switching a larger purpose-installed contactor for very large loads like a welding station. 

There are 3 variants of the Relay Switch in MakeACS:

1. The Signal Relay Switch has special gold-plated contacts, allowing it to work with small digital signals, like those from a microcontroller. It has 2 sets of NC and NO contacts, so you can switch multiple things in parallel.

2. The DIN Relay Switch is rated for 250V at 5A, for integration with larger electrical cabinets. It is usually used to drive a larger contactor.

3. The DIN Controller is similar to the DIN Relay Switch, but with 5 independent control channels. This allows you more control over how a system is controlled. For example at RIT, this switch is used on the paint booth: the lights, fan, and heater are on 3 separate channels, so anyone can turn on the fan and lights, but only those who are authorized can turn on the burner. 

## Other Components

Beyond simply controlling access, MakeACS supports additional accessories in a deployment, to further augment the capabilities. Here are some examples of these;

### Temperature Monitor

The temperature monitor allows an arbitrary temperature probe to be attached to a deployment, that can be used to lock out access if a temperature gets too cold or too hot. 

At RIT, this is used to ensure the paint booth is not drawing in too much cold outside air, chilling the entire makerspace. 

### Indicator Light

To help users see equipment availability, this add-on allows the attachment of a standard Andon light tower, which can show deployment state. 

### Laser Fume Monitor

This add-on integrates with the Epilog Laser fume extractor control interface, and will monitor for and report any faults related to the filters or the air assist supply line. If either is found to be malfunctioning, the equipment is locked out automatically.

### Hobbs Timer

While MakeACS automatically tracks usage time based on the total time on, this add-on allows for a specific signal to be used for hours tracking. This is useful on something like a CNC, where maintenance tasks should be based on spindle run-time, versus machine on-time.

### Buddy System Enforcer

This add-on lets two Cores control one deployment, in one of three modes. This allows hardware-enforcement of the buddy policy on high-risk equipment, or more complex user authorization setups.

* AND Mode: Both Cores need an approved user present to activate the equipment. This ensures 2 trained users are present at all times.

* OR Mode: Either Core needs an approved user to activate the equipment. This allows trained users to hand off equipment without disrupting its operation.

* AND-OR Mode: Both Cores need an approved user to activate, but then either one can keep it online. This is useful on equipment where you want staff to check over things before the user starts running, but once it is approved they can work on their own.

### Blast Gate Controller

This add-on enables MakeACS to open blast gates based on what equipment is in use. This ensures maximum suction to the equipment in use, and prevents excessive wear on the vacuum system when nothing is un use. It is designed for use with iVac automated blast gates, but can work with any generic 12v blast gate system.

## Deployment Examples

Below are some examples of how MakeACS is deployed at RIT.