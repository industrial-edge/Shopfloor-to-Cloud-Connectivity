# Installation

- [Installation](#installation)
  - [Configure PLC project](#configure-plc-project)
  - [Configuration Device Energy1](#configuration-device-energy1)
  

## Configure PLC project

1) Open TIA portal and open the project containing the EnergyManagement application (Adapt the IP addresses to your system)
2) Download the PLC program to the PLC and set the PLC into RUN
   

## Configuration Device Energy1

**IE Databus**

- Launch the IE Databus Configurator and add your related credentials/topics:
`"ie/#"`

![ie_databus_user](graphics/IE_Databus_User.png)

![ie_databus](graphics/IE_Databus.png)

**S7 Connector**

- Import the JSON file "ernergy1_S7_Connector"
  
![S7_connector](graphics/S7_Connector.png)

- Launch the S7 Connector and configure the PLC connection 
- Deploy and start your S7 Connector configuration

**Mindsphere Connector** 

**Flow Creator**


