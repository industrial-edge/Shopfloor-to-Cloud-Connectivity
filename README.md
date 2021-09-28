# Anchor-Use-Case-Cloud-Integration

Use case for communication from Edge Device to Edge Device and the Mindesphere via MQTT 

- [Anchor-Use-Case-Cloud-Integration](#anchor-use-case-cloud-integration)
    - [Overview](#overview)
    - [General task](#general-task)
    - [Prerequisities](#prerequisities)
    - [Used components](#used-components)
  - [Configuration Central Edge Device](#configuration-central-edge-device)
  - [Configuration Energy Device 1](#configuration-energy-device-1)
  - [Documentation](#documentation)
  - [Contribution](#contribution)
  - [Licence and Legal Information](#licence-and-legal-information)

### Overview 

![overview](docs/graphics/overview.png)

### General task

Gathering energy data from two Edge Devices and converting them to a standardized form in a southbound Edge Device with no Internet access. 
Sharing the standardized data with a northbound Edge Device, with Internet connectivity, via MQTT.
Structuring the energy data in asset models according to the MindSphere design in the northbound Edge Device and forwarding them to the MindSphere.
Central monitoring the energy data from two locations in one dash board.

###  Prerequisities
- Establish Connection to 2 PLC for getting data into the Edge Devices
- Access to an Industrial Edge Management System (IEM)
- Onboarded 3 Edge Devices 
- Installed Apps on Central Device: Data Service, Databus, Flow Creator, Energy Manager, MQTT Connector, Cloud Connector
- Installed Apps Device Energy1 and Energy2: S7 Connector, Cloud Connector, Databus, Flow Creator
- Google Chrome (Version ≥ 72) or Firefox (Version ≥ 62)

### Used components

- Industrial Edge Management V1.3.10
- IE Databus V1.3.5
- SIMATIC S7 Connector V 1.3.27
- MQTT Connector V1.2.9
- Cloud Connector V 1.3.1
- Data Service V1.2.0
- IE Flow Creator V1.1.2
- Energy Manager V1.2.0
- Industrial Edge Device V1.3.0-41
- Web browser (Mozilla or Chrome)


## Configuration Central Edge Device

You can find the further information about the following steps in the [docs](docs/install.md)
- Install Databus, Flow Creator, Energy Manager, MQTT Connector, Cloud Connector


## Configuration Energy Device 1

You can find the further information about the following steps in the [docs](docs/install.md)
- Install S7 Connector, Cloud Connector, Databus, Flow Creator 


## Documentation

You can find further documentation and help in the following links
  - [Industrial Edge Hub](https://iehub.eu1.edge.siemens.cloud/#/documentation)
  - [Industrial Edge Forum](https://www.siemens.com/industrial-edge-forum)
  - [Industrial Edge landing page](https://new.siemens.com/global/en/products/automation/topic-areas/industrial-edge/simatic-edge.html)
  
## Contribution

Thanks for your interest in contributing. Anybody is free to report bugs, unclear documenation, and other problems regarding this repository in the Issues section or, even better, is free to propose any changes to this repository using Merge Requests.

## Licence and Legal Information

Please read the [Legal information](LICENSE.md).

