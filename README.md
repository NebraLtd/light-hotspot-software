# Nebra Light Helium Hotspot Software

This repository contains the dockerfile that can configure a Hotspot running Balena to act as a Helium Light Hotspot.

<img src='https://jenkins.ryanteck.uk/buildStatus/icon?job=Helium-Guides+Download'>

## Getting Started
You can either get going by doing the following.

### Balena Open Fleets
Download an image powered by Balena Open Fleets, as we push out updates your system should automatically update.

https://hub.balena.io/nebraltd/helium-light-hotspot

### Balena Deploy
Alternatively you can click the button below to create your own Balena Application with the code ready to go.

[![balena deploy button](https://www.balena.io/deploy.svg)](https://dashboard.balena-cloud.com/deploy?repoUrl=https://github.com/NebraLtd/light-hotspot-software)

## Envrionment Variables

The Light Hotspot software requires the following variables to be set in Balena's Device or Fleet Variables.

**VARIANT** : The ENV Identifier from the list of hardware supported at https://github.com/NebraLtd/helium-hardware-definitions . **This is required**

**REGION_OVERRIDE** : Overrides for the specific region plan you wish to use. A list can be found at https://github.com/NebraLtd/hm-pktfwd/blob/variant-handler/README.md . **Currently requied**

**FREQ** : Optional but ideal, this variable should be set to the frequency of the Radio module for easy identification.


## Mining Notice

Currently light hotspots are unable to earn HNT, this is currently intended for development purposes and for those who wish to run just a packetforwarder compatible with the Helium Network.

Even when Light Hotspots are able to earn HNT this would only be possible with a hotspot from an approved manufacturer. DIY Hotspots will not be able to earn HNT in the future.

Full Details of the helium roadmap can be found at https://docs.helium.com/mine-hnt/light-hotspots

## Hardware Support

The Nebra Light Hotspot Software has been written to support multiple variants of hardware, both to be compatible with all of Nebra's hotspots but also some alternatives & DIY solutions.

The file and information of multiple hardware support can be found at https://github.com/NebraLtd/helium-hardware-definitions
