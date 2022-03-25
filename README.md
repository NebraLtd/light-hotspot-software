# Nebra Light Helium Hotspot Software

## Please note this repository has been archived and the functionality has been moved over to our main [helium-miner-software repo](https://github.com/NebraLtd/helium-miner-software) in the [light-hotspot branch](https://github.com/NebraLtd/helium-miner-software/tree/light-hotspot).

This repository includes the main [docker-compose.yml](https://github.com/NebraLtd/light-hotspot-software/blob/master/docker-compose.yml) file that powers the Nebra light hotspots as well as a variety of other hardware versions (see the [hardware support](#hardware-support) section below for more details).

The `docker-compose.yml` file is pushed to [Balena](https://www.balena.io/) (using GitHub Actions), which in turn pulls down the various Docker images outlined below.

There are currently six different services running within this device, which are all outlined below in the [containers](#containers) section.

## Getting Started
You can get going by doing either of the following...

### Balena Open Fleets
Download an image powered by Balena Open Fleets. As we push out updates your system should automatically update.

[Deploy with Balena Open Fleets](https://hub.balena.io/nebraltd/helium-light-hotspot)

### Balena Deploy
Alternatively you can click the button below to create your own Balena Application with the code ready to go.

[![balena deploy button](https://www.balena.io/deploy.svg)](https://dashboard.balena-cloud.com/deploy?repoUrl=https://github.com/NebraLtd/light-hotspot-software)

## Envrionment Variables

The Light Hotspot software requires the following variables to be set in Balena's Device or Fleet Variables.

**VARIANT** : The ENV Identifier from the list of hardware supported on our [hardware definitions repo](https://github.com/NebraLtd/helium-hardware-definitions). **This is required**.

**REGION_OVERRIDE** : Override for the specific region plan you wish to use. A list can be found on our [packet forwarder repo](https://github.com/NebraLtd/hm-pktfwd). **Currently required**.

**FREQ** : Optional but ideal, this variable should be set to the frequency of the radio module for easy identification.

## Containers

### Diagnostics

Repo: [github.com/NebraLtd/hm-diag](https://github.com/NebraLtd/hm-diag)

The diagnostics container is designed for local troubleshooting. It runs a local web server that displays various diagnostics data.

Note that this container is also responsible for serving content to the [Hotspot-Production-Tool](https://github.com/NebraLtd/Hotspot-Production-Tool).

### Packet Forwarder

Repo: [github.com/NebraLtd/hm-pktfwd](https://github.com/NebraLtd/hm-pktfwd)

This container is responsible for configuring packet forwarder's region and starts the radio module.

### Gateway Config

Repo: [github.com/NebraLtd/hm-config](https://github.com/NebraLtd/hm-config)

This container is (partially) responsible for the device onboarding and provides the Bluetooth LE to allow the hotspot to be configured via the Helium App. It is also responsible for configuring WiFi.

### Gateway RS (Light Hotspot Gateway/Miner)

Repo: [github.com/NebraLtd/hm-gatewayrs](https://github.com/NebraLtd/hm-gatewayrs)

This container is the actual Helium Gateway RS software (from upstream), with the required configuration files added.

### gwmfr

Repo: [github.com/NebraLtd/hm-gwmfr](https://github.com/NebraLtd/hm-gwmfr)

This software contains the tool which configures the ECC Key in production and isn't run again after.

### UPnP

Repo: [github.com/NebraLtd/hm-upnp](https://github.com/NebraLtd/hm-upnp)

This container attempts to use UPnP to set up a port forwarding rule, if your router supports it and the function is turned on in your router settings.

## Device Configuration / Fleet Configuration

For some Nebra Hotspots that use spidev1.2 you may need to add a DT overlay in the device or fleet configuration section on balenaCloud to enable spi1.

Additionally, for the SPI ethernet based Nebra Light Hotspot you need to add the DT overlay for the enc28j60.

To do this you need to find the "Define DT Overlays" section, click activate and then add `"enc28j60","spi1-3cs"`

## Mining Notice

Currently light hotspots are unable to earn HNT, this is currently intended for development purposes and for those who wish to run just a packet forwarder compatible with the Helium Network.

Even when Light Hotspots are able to earn HNT this would only be possible with a hotspot from an approved manufacturer. DIY Hotspots will not be able to earn HNT in the future for proof of coverage (PoC) but only for data transfer.

Full Details of the Helium light hotspot roadmap can be found on the [Helium docs site](https://docs.helium.com/use-the-network/light-hotspots/).

## Hardware Support

The Nebra Light Hotspot Software has been written to support multiple variants of hardware, both to be compatible with all of Nebra's hotspots but also some alternatives & DIY solutions.

The file and information of multiple hardware support can be found in the `hardware_definitions.py` file in our [hm-pyhelper repo](https://github.com/NebraLtd/hm-pyhelper).
