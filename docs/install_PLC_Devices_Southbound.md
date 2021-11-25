# Configuration Steps
- [Configuration Steps](#configuration-steps)
- [Configure PLC-Project in TIA-Portal](#configure-plc-project-in-tia-portal)
- [Configuration Southbound for Industrial Edge](#configuration-southbound-for-industrial-edge)
  - [IE Databus](#ie-databus)
  - [SIMATIC S7 Connector](#simatic-s7-connector)
  - [IE Flow Creator](#ie-flow-creator)
  - [IE Cloud Connector](#ie-cloud-connector)
- [Navigation](#navigation)
  

# Configure PLC-Project in TIA-Portal

1. Open TIA portal and open the project containing the EnergyManagement application (Adapt the IP addresses to your system)
   
![TIA_IP](graphics/TIA_IP.png)

2. Download the PLC program to the PLC and set the PLC into RUN
   

# Configuration Southbound for Industrial Edge

The Southbound consist of two devices. In the following they are called "Energy1" and "Energy2"

Installed Apps Device Energy1 and Energy2: 
  - SIMATIC S7 Connector
  - IE Cloud Connector
  - IE Databus
  - IE Flow Creator

## IE Databus

Add a user in the IE Databus Configurator with username and password and provide necessary access right to the required topics so the SIMATIC S7 Connector, IE Flow Creator and IE Cloud Connector can publish and subscribe to topics.

1. Launch the IE Databus Configurator and add your related credentials/topics:
`ie/#`

  ![ie_databus_user](graphics/IE_Databus_User.png)

2. After adding user deploy configuration to device

  ![ie_databus](graphics/IE_Databus.png)


## SIMATIC S7 Connector

To provide data from the PLC on the IE Databus connect the SIMATIC S7 Connector to the PLC and add the required PLC variables

1. Launch the S7 Connector and configure the PLC connection 
2. Import the JSON file [energy1_S7_Connector](../src/Device_Energy1/energy1_S7_Connector.json) for Energy1 and [energy2_S7_Connector](../src/Cevice_Energy2/energy2_S7_Connector.json) for Energy2 
3. Deploy and start your S7 Connector configuration

  ![S7_connector](graphics/S7_Connector.png)

## IE Flow Creator

Aggregate the raw data from the PLC to:
- Energy
- Water
- Pressured Air
- Produced Bottles 

After aggregation the data and metadata are published to IE Databus. IE Cloud Connector subscribes to these topics and sends them to the central device 

The aggregated values are published on newly defined topics to prevent collision with SIMATIC S7-Connector

1. Import the JSON-File
  
    Energy1: [FlowCreator_Energy1](../src/Device_Energy1/FlowCreator_Energy1.json)

    Energy2:[FlowCreator_Energy2](../src/Cevice_Energy2/FlowCreator_Energy2.json)
  
    
  ![FlowCreator1](graphics/Flow_Creator1.png)

2. Double click on a MQTT-Node  
3. add IE Databus Credentials
  
  ![FlowCreator2](graphics/Flow_Creator2.png)
  
    
  ![FlowCreator3](graphics/Flow_Creator3.png)

4. Deploy the Flows

## IE Cloud Connector

For the communication from Energy1 and Energy2 to the Central device configure the IE Cloud Connector. 
Instead of manually configuring you can also import the configuration files:

[CloudConnector_Energy1](../src/Device_Energy1/CloudConnector_Energy1.json) (Password = Edge1234!)

[CloudConnector_Energy2](../src/Cevice_Energy2/CloudConnector_Energy2.json) (Password = Edge1234!)

1. Click "Edit Configuration" and login to the Databus.

  ![Cloud_Connector](graphics/Cloud_Connector_Login.png)

Configure starting from the left side "Bus Adaptor" to the right the "Cloud Connector Clients" Adapt the IP addresses to your system.

To save the configuration, initially click on your route and connect your topics from the bus adaptor with your cloud topics 

Then click on deploy.

Note: Create one topic for the data and one topic for the metadata. 


2. Add the Metadata-topic in the Bus Adaptor Field

    Energy1: `ie/m/j/simatic/v1/iefc/dp`

    Energy2: `ie/m/j/simatic/v1/iefc/dp` 
  
      
  ![Cloud_Connector1](graphics/Cloud_Connector_Topic2.png)
  
3. Add the Data-topic
   
   Energy1:
   `ie/d/j/simatic/v1/iefc/dp/r/Line1/default`
  
   Energy2:
   `ie/d/j/simatic/v1/iefc/dp/r/line2/default`
    
  ![Cloud_Connector2](graphics/Cloud_Connector_Topic1.png)

4. Add Connecting Routes
  
   Energy1:
   `central-data` 
   `central-metadata`
  
   Energy2:
   `central-data2`
   `central-metadata2`
  
    
  ![Cloud_Connector3](graphics/Cloud_Connector_Route.png)

5. Add Cloud Connector Clients
  Type: `LOCAL_LAKE`
  
   Energy1:
   Data: `ie/d/j/simatic/v1/iecc/dp/r/energy1line1/raw`
   Metadata: `ie/m/j/simatic/v1/iecc/dp/energy1line1`
  
   Energy2:
   Data: `ie/d/j/simatic/v1/iecc/dp/r/energy2line2/raw`
   Metadata: `ie/m/j/simatic/v1/iecc/dp/energy2line2`
  
    
  ![Cloud_Connector4](graphics/Cloud_Connector_Client1.png)
    
      
  ![Cloud_Connector5](graphics/Cloud_Connector_Client2.png)

6. Mark the data and metadata routs an click "Save Route" 
      
        
  ![Cloud_Connector6](graphics/Cloud_Connector_Route1.png)
    
      
  ![Cloud_Connector7](graphics/Cloud_Connector_Route2.png)

7. Deploy your configuration





# Navigation

[Overview](../README.md)

[Configuration Central Device](install_Device_Northbound.md)

[Configuration MindSphere](install_MindSphere.md)

dSphere.md)

