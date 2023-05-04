# Shopfloor to Cloud Connectivity - Integrate machine & production data securely into the company cloud

Use case for communication from Edge Device to Edge Device and company Cloud (e.g. Insights Hub, formerly known as MindSphere) via MQTT 

- [Shopfloor to Cloud Connectivity - Integrate machine \& production data securely into the company cloud](#shopfloor-to-cloud-connectivity---integrate-machine--production-data-securely-into-the-company-cloud)
  - [Overview](#overview)
    - [Reference Architecture](#reference-architecture)
      - [IIH Insights Hub Sync](#iih-insights-hub-sync)
    - [Network Architecture](#network-architecture)
  - [General task](#general-task)
  - [Requirements](#requirements)
    - [Prerequisites](#prerequisites)
    - [Used components](#used-components)
  - [Configuration Southbound Devices](#configuration-southbound-devices)
  - [Configuration Northbound Device](#configuration-northbound-device)
  - [Configuration Insights Hub](#configuration-insights-hub)
  - [Documentation](#documentation)
  - [Contribution](#contribution)
  - [Licence and Legal Information](#licence-and-legal-information)

## Overview

![overview](docs/graphics/overview.png)

### Reference Architecture 

#### IIH Insights Hub Sync

![overview3](docs/graphics/overview4.png)

### Network Architecture

![overview2](docs/graphics/overview2.png)

## General task

Gathering of energy data from various controllers and converting it to a standardized form in a southbound Edge Device with no internet access. 

Central monitoring of energy data from multiple locations in dashboards, with a strict separation between Automation Cell Network (Southbound) and Datacenter (Northbound). Because there is no direct connection between Southbound and the connected PLCs with the Internet, this guideline minimizes security risks.

Sharing the standardized data with a northbound Edge Device, with internet connectivity, via MQTT.

Structuring the energy data in asset models according to the asset design in Insights Hub in the northbound Edge Device
and forwarding them to Insights Hub.




## Requirements

###  Prerequisites
- Industrial Edge Learning Path (Module 1-3)
- Established connection to 2 PLCs to acquire data with the Edge Device
- Access to an Industrial Edge Management System (IEM)
- Onboarded 3 Industrial Edge Devices (IEDs) on Industrial Edge Management
- Installed System App Configurators on IEM (Common Connector Configurator, IE Databus Configurator, IE Cloud Connector Configurator) 
- Installed apps on Southbound-Devices (OPC UA Connector, IE Cloud Connector, Databus, IE Flow Creator)
- Installed apps on Northbound-Device (Data Service, Databus, Energy Manager, External Databus, IIH Core, IIH Configurator)
- Google Chrome (Version ≥ 72) or Firefox (Version ≥ 62)
- Access to Insights Hub
- MindConnect IoT Extension (Optional)
- Energy Manager
  
### Used components

TIA & PLCs:
- TIA V16
- PLC 1512SP-1 PN FW V2.1

Industrial Edge:
- Industrial Edge Management V1.7.4
- Industrial Edge Device V1.5.0-21-amd64
- OPC UA Connector V1.7.0-15
- Databus V2.0.0
- External Databus V2.0.0
- Data Service V1.6.0
- IE Flow Creator V1.3.9
- Energy Manager V1.2.0
- IE Cloud Connector V1.6.2
- IIH Core V1.6.0
- IIH Configurator V1.6.0
- Web browser (Mozilla or Chrome)

Insights Hub:
- Asset Manager 
- Energy Manager

## Configuration Southbound Devices

You can find the further information about the following steps in the [docs](docs/install_PLC_Devices_Southbound.md)

- Configure PLC project in TIA-Portal
- Configure PLC connections in Industrial Edge
  - OPC UA Connector
  - Databus 
- Configure Data preprocessing 
  - IE Flow Creator 
- Configure Connection to Northbound
  - IE Cloud Connector 


## Configuration Northbound Device

You can find the further information about the following steps in the [docs](docs/install_Device_Northbound.md)

- Configure Connection to Southbound
  - Databus 
  - External Databus
  - Industrial Information Hub 
    - Data Service
    - Insights Hub Sync

- Configure visualization
  - Energy Manager


## Configuration Insights Hub
You can find the further information about the following steps in the [docs](docs/install_MindSphere.md)

- Configure visualization
  - Energy Manager 


## Documentation

You can find further documentation and help in the following links
  - [Industrial Edge Hub](https://iehub.eu1.edge.siemens.cloud/#/documentation)
  - [Industrial Edge Forum](https://www.siemens.com/industrial-edge-forum)
  - [Industrial Edge landing page](https://new.siemens.com/global/en/products/automation/topic-areas/industrial-edge/simatic-edge.html)
  - [Industrial Edge Learning Path](https://siemens-learning-simaticedge.sabacloud.com/)
  - [Energy Manager on Insights Hub application manual](https://documentation.mindsphere.io/resources/html/energy-manager/en-US/index.html)
## Contribution

Thanks for your interest in contributing. Anybody is free to report bugs, unclear documentation, and other problems regarding this repository in the Issues section or, even better, is free to propose any changes to this repository using Merge Requests.

## Licence and Legal Information

Please read the [Legal information](LICENSE.md).

