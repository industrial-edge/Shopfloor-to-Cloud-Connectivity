# Installation

- [Installation](#installation)
  - [Configure PLC project](#configure-plc-project)
  - [Configuration Device Energy1 and Energy2](#configuration-device-energy1-and-energy2)
  - [Configure Device Central](#configure-device-central)
  

## Configure PLC project

- Open TIA portal and open the project containing the EnergyManagement application (Adapt the IP addresses to your system)
- Download the PLC program to the PLC and set the PLC into RUN
   

## Configuration Device Energy1 and Energy2

**IE Databus**

- Launch the IE Databus Configurator and add your related credentials/topics:
`"ie/#"`

![ie_databus_user](graphics/IE_Databus_User.png)

![ie_databus](graphics/IE_Databus.png)


**S7 Connector**
  
![S7_connector](graphics/S7_Connector.png)

- Launch the S7 Connector and configure the PLC connection 
- Import the JSON file "ernergy1_S7_Connector" for Energy1 and "ernergy2_S7_Connector" for Energy2
- Deploy and start your S7 Connector configuration


**Mindsphere Connector** 

Configure starting from the left side "Bus Adaptor" to the right the "Cloud Connector Clients" Adapt the IP addresses to your system.
To deploy the configuration, initially click on your route and connect your topics from the bus adaptor with your cloud topics 
Then click on deploy. 
Note: You must create one topic for the data and one topic for the metadata. 

- Add the Topics in the Bus Adaptor Field
  One for the data and one for the metadata

  Energy1:
  `"ie/m/j/simatic/v1/iefc/"`
  `"ie/d/j/simatic/v1/iefc/dp/r/Line1/default"`
  
  Energy2:
  `"ie/m/j/simatic/v1/iefc/dp"` 
  `"ie/d/j/simatic/v1/iefc/dp/r/line2/default"`

![Mindsphere_Connector1](graphics/Mindsphere_Connector_Topic1.png)
  
![Mindsphere_Connector2](graphics/Mindsphere_Connector_Topic2.png)

- Add Connecting Routes
  
  Energy1:
  `"central-data"` 
  `"central-metadata"`
  
  Energy2:
  `"central-data2"`
  `"central-metadata2"`

![Mindsphere_Connector3](graphics/Mindsphere_Connector_Rout.png)

- Add Cloud Connector Clients
  Type: `"LOCAL_LAKE"`
  
  Energy1:
  Data: `"ie/d/j/simatic/v1/iecc/dp/r/energy1line1/raw"`
  Metadata: `"ie/m/j/simatic/v1/iecc/dp/energy1line1"`
  
  Energy2:
  Data: `"ie/d/j/simatic/v1/iecc/dp/r/energy2line2/raw"`
  Metadata: `"ie/m/j/simatic/v1/iecc/dp/energy2line2"`

![Mindsphere_Connector4](graphics/Mindsphere_Connector_Client1.png)
  
![Mindsphere_Connector5](graphics/Mindsphere_Connector_Client2.png)

- Mark the data and metadata routs an click "Save Route" 
    
![Mindsphere_Connector6](graphics/Mindsphere_Connector_Rout1.png)
  
![Mindsphere_Connector7](graphics/Mindsphere_Connector_Rout2.png)

- Deploy your configuration

**Flow Creator**
- Import the JSON-File
  
  Energy1:
  `"FlowCreator_Energy1"`
  Energy2:
  `"FlowCreator_Energy2"`

![FlowCreator1](graphics/Flow_Creator1.png)

- Double click to a MQTT-Node  
- Login to the Databus
  
![FlowCreator2](graphics/Flow_Creator2.png)
  
![FlowCreator3](graphics/Flow_Creator3.png)

- Deploy the Flows

## Configure Device Central
