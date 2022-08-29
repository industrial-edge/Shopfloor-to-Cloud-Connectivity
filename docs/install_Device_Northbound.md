# Configuration Steps

- [Configuration Steps](#configuration-steps)
- [Configure Northbound](#configure-northbound)
  - [IE Databus](#ie-databus)
  - [IE MQTT Connector](#ie-mqtt-connector)
  - [Data Service](#data-service)
  - [Option 1: MindConnect MQTT](#option-1-mindconnect-mqtt)
    - [Create an agent private key](#create-an-agent-private-key)
    - [Configure IE MindSphere Connector](#configure-ie-mindsphere-connector)
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
  - Option 1: MindConnect MQTT
    - IE Mindsphere Connector
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

##  Data Service

In order to store the data send by the Cloud Connector of the Energy 1 and Energy 2 device, configure two adapters with the metadata topic from the Cloud Connector in Energy1 and Energy2.  

1. Go to the Data Service and select "Adapters"
     
  ![IE_Dataservice1](graphics/IE_Dataservice1_Central.png)

2. Click "+" to add a new adapter 
   
3. Add one adapter for Energy1 and one adapter for Energy2
   
4. Add the data as shown in the picture
  
  URL for Energy1 `ie/m/j/simatic/v1/energy1line1:iefc/dp`

  URL for Energy2 `ie/m/j/simatic/v1/energy2line2:iefc/dp`

5. Save the configuration
   
6. Open the configuration again and set the status on "Active"
  
    
  ![IE_Dataservice2](graphics/IE_Dataservice2.png)
  
After the adapters are connected you can find the data in the Dataservice.

7. Click on the first button on the left side
  
    
  ![IE_Dataservice3](graphics/IE_Dataservice3.png)

8. With a click on the three points you can edit the asset.
  
    
  ![IE_Dataservice4](graphics/IE_Dataservice4.png)

9. To add the variables to the Data Service click "Add multiple variables"
    
10. Select the adapter "energy1" mark all four variables and click "save"
    
11. Do the same for the adapter "energy2"
  
    
  ![IE_Dataservice5](graphics/IE_Dataservice5.png)


To sort the data add aspects in the Data Service.

12. Click in the Data Service on the right side on the "Add aspect"
  

  ![IE_Dataservice6](graphics/IE_Dataservice6.png)

13. Choose the data for Line1 and add them to the aspect. Do the same for Line2
  

  ![IE_Dataservice7](graphics/IE_Dataservice7.png)
  

## Option 1: MindConnect MQTT

### Create an agent private key

On how to create the agent key, please refer to the [How To](https://documentation.mindsphere.io/MindSphere/howto/howto-onboard-mindconnect-mqtt.html) on https://mindsphere.io

```
set TENANT=<yourtenant>
set DEVICE_NAME=<yourdevicename>
set COUNTRY_CODE=<COUNTRY_CODE>
set CITY=<CITY>
set ORGANIZATION=<ORGANIZATION>
set CLIENT_ID="%TENANT%"_"%DEVICE_NAME%"
```

1. ```openssl genrsa -out %DEVICE_NAME%.key 2048```
2. ```openssl req -new -key %DEVICE_NAME%.key -out %DEVICE_NAME%.csr -subj "/C=%COUNTRY_CODE%/ST=%CITY%/O=%ORGANIZATION%/OU=IT/CN=%DEVICE_NAME%"```
3. ```openssl x509 -req -in %DEVICE_NAME%.csr -CA "%TENANT%.pem" -CAkey "%TENANT%.key" -CAcreateserial -out %DEVICE_NAME%.pem -days 365 -sha256```
4. ```type %DEVICE_NAME%.pem "%TENANT%.pem" > "%DEVICE_NAME%"_chain.pem```

You now have a private key for your agent: ```%DEVICE_NAME%".pem```

### Configure IE MindSphere Connector
In your management system, go to Data Connections -> IE MindSphere Connector -> Choose your device -> Launch.

1. Set up the Databus adapter for IE MindSphere Connector -> Click Add Topic, fill in the required info and select the correct topic.
   
  - Username: `edge`

  - Password: `edge`

  - Metadata for Subscription: `ie/m/j/simatic/v1/iefc/dp/energy1line1`

  Then select List Data Topics and choose `ie/d/j/simatic/v1/iefc/dp/r/energy1line1/default` from "Select Data Topics".
  Repeat these steps for `ie/m/j/simatic/v1/iefc/dp/energy2line2`

   ![IEMindSphereConnector_Adapter](graphics/IEMindSphereConnector_Adapter.png)

2. Create the MindSphere client by selecting "Add Client". 
   
  Choose a name and the type (Depending on your MindSphere tenant).
  Upload the previously created client certificate and key.

   ![IEMindSphereConnector_CloudClient1](graphics/IEMindSphereConnector_CloudClient1.png)

3. Edit your Cloud Client and select the Tenant & Client ID.
  > **_NOTE:_**  The Client ID must be in the format `tenant_yourClientName`.

  ![IEMindSphereConnector_CloudClient2](graphics/IEMindSphereConnector_CloudClient2.png) 


5. Prepare the Model by selecting the data model on Edge which should be transferred to MindSphere.
   
  ![IEMindSphereConnector_CloudClient3](graphics/IEMindSphereConnector_CloudClient3.png) 

6. Create a Route by clicking "Add Route", select a name, connect the topics and the client and click "Save Route".
  
  ![IEMindSphereConnector_route](graphics/IEMindSphereConnector_route.png)  

6. Deploy the configuration.
 
 ![IEMindSphereConnector](graphics/IEMindSphereConnector.png)  

In MindSphere Energy Manager, you should now see your data structure from Data Service.

  ![MindSphere_Datamodel](graphics/MindSphere_Datamodel.png)

## Option 2: MindConnect IoT Extension

### IE Flow Creator 

> **_NOTE:_** Only required when connecting to MindConnect IoT Extension. Otherwise you can skip to [Northbound Device - Energy Manager](#northbound-device---energy-manager)

The IE Flow Creator will extract the packaged data from IE Cloud Connector
and also converts the data to MindSphere IOT Extension data format

1. Import the Flows from the JSON-File [FlowCreator_Central](../src/CentralDevice/FlowCreator_Central.json) as described [here](install_PLC_Devices_Southbound.md)
   
2. Enter IE-Databus credentials

### IE Cloud Connector - MindConnect IoT Extension

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
  
  
5. Mark the Topics, Route and Client and save the Route
   
  
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
