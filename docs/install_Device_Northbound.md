# Configuration Steps

- [Configuration Steps](#configuration-steps)
- [Configure Northbound](#configure-northbound)
  - [IE Databus](#ie-databus)
  - [IE MQTT Connector](#ie-mqtt-connector)
  - [Option 1: IIH Mindsphere Sync](#option-1-iih-mindsphere-sync)
    - [Integrate Data Service](#integrate-data-service)
    - [Configure Connections](#configure-connections)
    - [Create the Asset Model](#create-the-asset-model)
  - [Option 2: MindConnect IoT Extension](#option-2-mindconnect-iot-extension)
    - [IE Flow Creator](#ie-flow-creator)
    - [IE Cloud Connector - MindConnect IoT Extension](#ie-cloud-connector---mindconnect-iot-extension)
  - [Northbound Device - Energy Manager](#northbound-device---energy-manager)
- [Navigation](#navigation)
  
# Configure Northbound

The Northbound consist of one device. In the following this is called "Central Device".
Installed Apps on Central Device:
  - Data Service
  - IE Databus
  - Energy Manager
  - IE MQTT Connector  
  - Option 1: IIH Mindsphere Sync
    - IIH Core
    - IIH Configurator
    - IIH Registry Service
    - IIH Databus Gateway
  - Option 2: MindConnect IoT Extension
    - IE Flow Creator
    - IE Cloud Connector

## IE Databus

Configure the User and Topic in the IE Databus Configurator as described [here](install_PLC_Devices_Southbound.md).  

Instead of manually configuring you can also import the configuration files:

[IE_Databus_Central](../src/CentralDevice/IE-Databus.json) (Password = Edge1234!)

1. Launch the IE Databus Configurator and add your related Credentials/Topics:

   - Username: `edge`
   - Password: `edge`
   - Topic: `ie/#`
   - Permission: `Publish and Subscribe`
  
    
  ![ie_databus_user](graphics/IE_Databus_User.png)
  
 2. Deploy configuration to device

  ![ie_databus](graphics/IE_Databus.png)

## IE MQTT Connector

To receive the data from the IE Cloud Connector from Energy1 and Energy2 the IE MQTT Connector has to be configured

Instead of manually configuring you can also import the configuration files:

[IE_MQTT_Connector_Central](../src/CentralDevice/IE_MQTT_Connctor_Central.json) (Password = Edge1234!)

1. Launch the IE MQTT Connector Configurator and add your related Credentials/Topics:

   - Username: `edge`
   - Password: `edge`

![ie_mqtt_Connector](graphics/IE_MQTT_Connector_User.png)

2. Add Topic and Permission

- Topic: `ie/#`
- Permission: `Publish and Subscribe`

![ie_mqtt_Connector](graphics/IE_MQTT_Connector_Topic.png)
    
![ie_mqtt_Connector](graphics/MQTT_Connector.png)

3. Set "Unsecure" in IE MQTT Connector

![IE_MQTT_Connector](graphics/IE_MQTT_Connector_Certificate.png)

4. Bridge Configure

   - Insert User: `edge`
   - Insert password: `edge`
   - Select Topic:  `ie/#`
   - Direction: `IE MQTT Connector` :arrow_right: `IE Databus`

![IE_MQTT_Connector](graphics/IE_MQTT_Connector_Bridge.png)

##  Option 1: IIH Mindsphere Sync

All the following steps for this option will be performed in the "IIH Configurator" app on the Central Device.

### Integrate Data Service

To store data in the Industrial Information Hub (IIH), it is required to integrate the Data Service Application. 
Be aware that all data that was previously stored will be lost.

1. Go to the "Store Data" tab

2. Click on "Integrate"
   
  ![IIH_IntegrateDataService](graphics/IIH_IntegrateDataService.png)

3. Confirm the integration in the popup window

  ![IIH_IntegrateDataServiceConfirmation](graphics/IIH_IntegrateDataServiceConfirmation.png)

### Configure Connections

The IIH needs a connection to the IE Databus and to Mindsphere. You need to have a Mindsphere account and create
certificates to allow a connection from the IIH.

1. Configure the IE Databus credentials under "Settings > Databus credentials"

  ![IIH_DatabusCredentials](graphics/IIH_DatabusCredentials.png)

2. Save the configuration

3. Check if the device has a online connection in the "Home" tab. If the status is offline, please check your
   network settings and make sure that everything is configured correctly.

  ![IIH_OnlineStatus](graphics/IIH_OnlineStatus.png)

4. Click on "Add parent IED / Connect to Mindsphere"

  ![IIH_MindsphereConfig1](graphics/IIH_MindsphereConfig1.png)

5. Select the device type "Mindsphere Device"

6. Enter credentials for the application. Those are required, to allow the IIH to interact with Mindspheres REST-API.
   The Mindsphere Tenant Administrator has to create them and assign the role "mdsp:core:Admin3rdPartyTechUser", to
   allow the IIH to update the asset model in Mindsphere. More information can be found [here](https://documentation.mindsphere.io/MindSphere/apps/operator-cockpit/application-credentials-for-API-applications.html)

  ![IIH_MindsphereConfig2](graphics/IIH_MindsphereConfig2.png)

7. Enter the certificate details and upload the certificate and key. Information on how to create connector certificates
   can be found [here](https://documentation.mindsphere.io/MindSphere/howto/howto-managing-ca-certificates.html)

8. Select your region and save the configuration.

  ![IIH_ConnectionSuccessfull](graphics/IIH_ConnectionSuccessfull.png)

9. The connection will be established and you should see a green status in the IIH "Home" window

### Create the Asset Model

1. Go to "Define Data > Organize" to create a Asset Model and connect the variables

2. Add a Asset Model and name it by double clicking on it

3. Add two Aspects to structure the data according two our two machines

  ![IIH_CreateAssetModel1](graphics/IIH_CreateAssetModel1.png)

4. Now add 4 variables for each Aspect and give them names

5. On the left side below "Data Sources" you should see the two Databus topics with the variables from each machine

6. Assign those tags two the variables in your Asset model per drag & drop

  ![IIH_CreateAssetModel2](graphics/IIH_CreateAssetModel2.png)

7. Check the "Storage" and "Cloud Sync" checkbox for each variable

8. Deploy the configuration

The incoming data will now be stored in the integrated Data Service. Under "Store Data" you can see the created 
Asset model and the datapoints.

  ![IIH_StoreData](graphics/IIH_StoreData.png)

In MindSphere Energy Manager, you should now also see your data structure from the IIH.

  ![MindSphere_Datamodel](graphics/MindSphere_Datamodel.png)

## Option 2: MindConnect IoT Extension

### IE Flow Creator 

> **_NOTE:_** Only required when connecting to MindConnect IoT Extension. Otherwise you can skip to [Northbound Device - Energy Manager](#northbound-device---energy-manager)

The IE Flow Creator will extract the packaged data from IE Cloud Connector
and also converts the data to MindSphere IOT Extension data format

1. Import the Flows from the JSON-File [FlowCreator_Central](../src/CentralDevice/FlowCreator_Central.json) as described [here](install_PLC_Devices_Southbound.md)
   
2. Enter IE-Databus credentials

### IE Cloud Connector - MindConnect IoT Extension

Requirements:

- You must have a MindSphere account
- You must have the MindConnect IoT Extension Upgrade. This allows to use the MindConnect IoT Extension. To get the upgrade, your tenant admin needs to contact their assigned Account Executive or Customer Success Manager.
- For MindConnect IoT Extension user: [Managing Users Documentation](https://documentation.mindsphere.io/MindSphere/apps/mindconnect-IoT-extension/account-managing-users.html)
  - **Devicemanagement User**, assigned in MindConnect IoT Extension 

For the communication with MindSphere configure IE Cloud Connector accordingly.
The steps are similar to the description for Energy1 and Energy2. 
Instead of manually configuring you can also import the configuration files:

[CloudConnector_Central](../src/CentralDevice/CloudConnector_Central.json) (Password = Edge1234!)

1. Click "Edit Configuration" and login to the Databus.

  ![Cloud_Connector](graphics/Cloud_Connector_Login.png)
  
2. Add the topics: `ie/cloudconnector/energy1` and `ie/cloudconnector/energy2` 
  
    
  ![Cloud_Connector_Central](graphics/Cloud_Connector_Topic_Cantral.png)

3. Add Route
  
    
  ![Cloud_Connector_Route_Central](graphics/Cloud_Connector_Route_Cantral.png)
  
4. Add Cloud Connector Clients
  
   
  ![Cloud_Connector_Central_Clients1](graphics/Cloud_Connector_Clients_Central1.png)

  ![Cloud_Connector_Central_Clients2](graphics/Cloud_Connector_Clients_Central2.png)

Example:  
- Hostname: mciotextension.eu1.mindsphere.io
- Tenant Name: demo
- Username: TenantName/username
  
1. Mark the Topics, Route and Client and save the Route
   
  
  ![Cloud_Connector_Central_Route](graphics/Cloud_Connector_Central_Rout1.png)
  
6. Deploy the configuration


## Northbound Device - Energy Manager

To analyze the data locally on the Edge Device, you can use Energy Manager App on the Northbound Device

Energy Manager displays the total energy consumption, the energy consumption per bottle and the associated costs for each line.

  ![EnergyManageroverview1](graphics/EnergyManager_overview1.png)

  ![EnergyManageroverview2](graphics/EnergyManager_overview2.png)

  ![EnergyManageroverview3](graphics/EnergyManager_overview3.png)

At first a ned dashboard, that contains the widgets will be created.


1. Add a new dashboard  "Overview Media Consumption"
  
  ![EnergyManager1](graphics/EnergyManager1.png)

2. Do the same for the dashboards "Media Consumption per Bottle Line1" and "Media Consumption per Bottle Line2"
  
Show the produced bottles from Line1 in a Value on Dashboard "Overview Media Consumption"

3. Click on "Create first widget"
   
4. Select type "Value" and continue

  ![EnergyManager2](graphics/EnergyManager2.png)

5. Name the widget "Produced Bottles Line1" and select the calculation period
  
  ![EnergyManager3](graphics/EnergyManager3.png)

6. Select parameter
  
  ![EnergyManager4](graphics/EnergyManager4.png)

7. Select "counter" for the aggregation

  ![EnergyManager5](graphics/EnergyManager5.png)

8. Click "continue" twice and finish the configuration
   
9.  Do the same for "Produced Bottles Line2"

Show the "Media Consumption Line1" as a line diagram

10. Click "New widget"
    
11. Select type "Diagram" and continue 
    
12. Name the widget "Media Consumption Line1" and select the calculation 
  
  ![EnergyManager6](graphics/EnergyManager6.png)

Select parameter

  ![EnergyManager7](graphics/EnergyManager7.png)

13. Select "counter" for the aggregation
    
14. To change the colour of the lines click on the gear and select the colour

  ![EnergyManager8](graphics/EnergyManager8.png)

Because of different units it´s necessary to adapt the "Y-axis"

15. On rubric 5 "Chart-Display options" click on the gear next to "Y-axis"
    
16. Assign the parameters as shown in the picture below

  ![EnergyManager9](graphics/EnergyManager9.png)

17. Do the same for the other line diagrams 
  
  Note: for some diagrams KPIs are necessary, how to set them is explained in the next step

A gauge diagram is a way to give a quick overview about the current values e.g. Energy per Bottle Line1  
Here it´s necessary to generate a KPI that calculates the value

In order not to configure all calculations individually, it´s helpful to create KPIs

18. Click "Configuration" on the left side and select "KPI types"

  ![EnergyManager12](graphics/EnergyManager12.png)

19. Add "New KPI type"
    
20. Edit Name and Unit
    
21. Add the formula in case of this example `totalEnergyLine1 / ProducedBottlesLine1`
  
  ![EnergyManager13](graphics/EnergyManager13.png)

22. After saving switch back to "My Plant" 
    
23. Select the Dashboard "Media Consumption Bottle Line1"
    
24. Add a new widget
    
25. Select type "Gauge"
  
  ![EnergyManager10](graphics/EnergyManager10.png)

26. Name the widget "Energy per Bottle Line1" and select the calculation period
  
  ![EnergyManager11](graphics/EnergyManager11.png)

27. Click "New KPI instance"
    
28. Mark "on basis of a KPI type" and select the KPI type
    
29. Add the associated variable to the operands

  ![EnergyManager14](graphics/EnergyManager14.png)

  ![EnergyManager15](graphics/EnergyManager15.png)

30. Add the limits of the gauge

  ![EnergyManager16](graphics/EnergyManager16.png)

  ![EnergyManager17](graphics/EnergyManager17.png)


Used KPI types:
  
- CostsPerBottle: `(Energy / 1000 * cost_kWh + PressuredAir * cost_Liter_Air + Water * cost_Liter_Water) / Bottles` Unit: €

- CostsPerLine: `(Energy / 1000 * cost_kWh + PressuredAir * cost_Liter_Air + Water * cost_Liter_Water)` Unit: €

- EnergyPerBottle: `Energy / Bottles` Unit: Wh

- PressuredAirPerBottle: `PressuredAir / Bottles` Unit: ml

- WaterPerBottle: `Water / Bottles` Unit: ml

# Navigation

[Overview](../README.md)

[Configuration Southbound Device](install_PLC_Devices_Southbound.md)

[Configuration MindSphere](install_MindSphere.md)
