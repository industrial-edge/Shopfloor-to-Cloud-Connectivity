# Anchor-Use-Case-Cloud-Integration

Use case for communication from Edge Device to Edge Device and the Mindesphere via MQTT 

- [Anchor-Use-Case-Cloud-Integration](#anchor-use-case-cloud-integration)
    - [Overview](#overview)
      - [Reference Architecture](#reference-architecture)
      - [Network Architecture](#network-architecture)
    - [General task](#general-task)
  - [Requirements](#requirements)
    - [Prerequisites](#prerequisites)
    - [Used components](#used-components)
  - [Configuration Southbound Devices](#configuration-southbound-devices)
  - [Configuration Northbound Device](#configuration-northbound-device)
  - [Configuration MindSphere](#configuration-mindsphere)
  - [Documentation](#documentation)
  - [Contribution](#contribution)
  - [Licence and Legal Information](#licence-and-legal-information)

### Overview 

![overview](docs/graphics/overview.png)

#### Reference Architecture

![overview3](docs/graphics/overview3.png)

#### Network Architecture

![overview2](docs/graphics/overview2.png)

### General task

Allows gathering energy data from various Devices and converting them to a standardized 
form in a southbound Edge Device with no Internet access. 


Sharing the standardized data with a northbound Edge Device, with internet connectivity, via MQTT.


Structuring the energy data in asset models according to the MindSphere design in the northbound Edge Device
and forwarding them to the MindSphere.


Allows centrally monitoring energy data from multiple location in dash boards.

## Requirements

###  Prerequisites
- Industrial Edge Learning Path (Module 1-3)
- Established connection to 2 PLCs for getting data into the Edge Device
- Onboarded 3 Industrial Edge Devices (IEDs) on Industrial Edge Management
- Access to an Industrial Edge Management System (IEM)
- Installed system configurators (S7 Connector Configurator, IE Databus Configurator, Cloud Connector Configurator, IE MQTT Connector Configurator) 
- Installed apps on Southbound-Devices (SIMATIC S7 Connector, IE Cloud Connector, IE Databus, IE Flow Creator)
- Installed apps on Northbound-Device (Data Service, IE Databus, IE Flow Creator, Energy Manager, IE MQTT Connector, IE Cloud Connector)
- Google Chrome (Version ≥ 72) or Firefox (Version ≥ 62)
- Access to the MindSphere
  
### Used components

TIA & PLCs:
- TIA V16
- PLC 1512SP-1 PN FW V2.1

Industrial Edge:
- Industrial Edge Management V1.3.0
- IE Databus V1.3.5
- SIMATIC S7 Connector V 1.3.27
- MQTT Connector V1.2.9
- Cloud Connector V 1.3.1
- Data Service V1.3.0
- IE Flow Creator V1.1.10
- Energy Manager V1.2.0
- Industrial Edge Device V1.2.0-56
- Web browser (Mozilla or Chrome)

MindSphere:
- Asset Manager 
- MindConnect IoT Extension
- Energy Manager

## Configuration Southbound Devices

You can find the further information about the following steps in the [docs](docs/install_PLC_Devices_Southbound.md)

- Configure PLC project in TIA-Portal
- Configure PLC connections in Industrial Edge
  - S7 Connector
  - Databus 
- Configure Data preprocessing 
  - Flow Creator 
- Configure Connection to Northbound
  - Cloud Connector 


## Configuration Northbound Device

You can find the further information about the following steps in the [docs](docs/install_Device_Northbound.md)

- Configure Connection to Southbound
  - Databus 
  - MQTT Connector
  - Flow Creator
  - Data Service
- Configure Connection to MindSphere
  - Cloud Connector
- Configure visualization
  - Energy Manager


## Configuration MindSphere
You can find the further information about the following steps in the [docs](docs/install_MindSphere.md)

- Configure Connection to Northbound
  - Asset Manager
  - MindConnect IoT Extension
- Configure visualization
  - Energy Manager 


## Documentation

You can find further documentation and help in the following links
  - [Industrial Edge Hub](https://iehub.eu1.edge.siemens.cloud/#/documentation)
  - [Industrial Edge Forum](https://www.siemens.com/industrial-edge-forum)
  - [Industrial Edge landing page](https://new.siemens.com/global/en/products/automation/topic-areas/industrial-edge/simatic-edge.html)
  - [Industrial Edge Learning Path](https://siemens-learning-simaticedge.sabacloud.com/)
## Contribution

Thanks for your interest in contributing. Anybody is free to report bugs, unclear documentation, and other problems regarding this repository in the Issues section or, even better, is free to propose any changes to this repository using Merge Requests.

## Licence and Legal Information

Please read the [Legal information](LICENSE.md).

