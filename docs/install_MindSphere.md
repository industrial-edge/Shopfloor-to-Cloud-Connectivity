# Configuration Steps


- [Configuration Steps](#configuration-steps)
- [Configure MindSphere](#configure-mindsphere)
  - [Asset Manager](#asset-manager)
  - [MindConnect IoT Extension](#mindconnect-iot-extension)
  - [Energy Manager](#energy-manager)
- [Navigation](#navigation)
  


# Configure MindSphere

## Asset Manager

In order to display the data of the lines in MindSphere, it´s necessary to create the corresponding assets and aspects

1. Go to "library" and select "Aspect Types"
  
  ![Mindsphere_Asset_Manager1](graphics/Mindsphere_AssetManager1.png)

2. Add a new Aspect "Media_Consumption_Line"
   
3. Fill in the name and select "Dynamic"

  ![Mindsphere_Asset_Manager2](graphics/Mindsphere_AssetManager2.png)

4. Add the variables

   ![Mindsphere_Asset_Manager3](graphics/Mindsphere_AssetManager3.png)

5. Go to "Asset Types"

  ![Mindsphere_Asset_Manager4](graphics/Mindsphere_AssetManager4.png)

6. Create new type
  
  ![Mindsphere_Asset_Manager5](graphics/Mindsphere_AssetManager5.png)

7. Add name and aspects
  
  ![Mindsphere_Asset_Manager6](graphics/Mindsphere_AssetManager6.png)

  ![Mindsphere_Asset_Manager7](graphics/Mindsphere_AssetManager7.png)

8. Create the aspects "Line1" and "Line2" 

  ![Mindsphere_Asset_Manager8](graphics/Mindsphere_AssetManager8.png)

9. Go to "Assets"

  ![Mindsphere_Asset_Manager9](graphics/Mindsphere_AssetManager9.png)

10. Create asset
    
11. Select type "Media Consumption"

  ![Mindsphere_Asset_Manager10](graphics/Mindsphere_AssetManager10.png)

12. Name the Asset "Media Consumption Factory1" and safe your configuration


## MindConnect IoT Extension

The MindConnect connects the data from the Central Edge Device with the assets. 
The Central Device is named "Media Consumption Factory1" this name was defined in CloudConnector as ClientID. 
1. Go to "Device mapping" -> "Device mapping"
  
  ![Mindsphere_MindConnect1](graphics/Mindsphere_MindConnect1.png)

2. Select the asset "Media Consumption Factory1"

  ![Mindsphere_MindConnect2](graphics/Mindsphere_MindConnect2.png)

3. Click "Add mapping"
   
4. Map the Source to the created Target
  
  ![Mindsphere_MindConnect3](graphics/Mindsphere_MindConnect3.png)

  ![Mindsphere_MindConnect4](graphics/Mindsphere_MindConnect4.png)

5. Commit changes

## Energy Manager

The Energy Manager shows the data from the whole Factory1
  
  ![Mindsphere_EnergyManager1](graphics/Mindspehre_EnergyManager1.png)
  
  ![Mindsphere_EnergyManager2](graphics/Mindspehre_EnergyManager2.png)

1. The handling is the same as described under [Central Device Energy Manager ](install_Device_Northbound.md)
  
- CostsPerBottle: `((EnergyLine1 + EnergyLine2) / 1000 * cost_kWh + (PressuredAirLine1 + PressuredAirLine2)`
                     `* cost_Liter_Air + (WaterLine1 + WaterLine2) * cost_Liter_Water) / Bottles` Unit: €

- CostsPerFactory: `((EnergyLine1 + EnergyLine2) / 1000 * cost_kWh + (PressuredAirLine1 + PressuredAirLine2)`
                     `* cost_Liter_Air + (WaterLine1 + WaterLine2) * cost_Liter_Water)/100` Unit: €

- EnergyPerBottle: `(EnergyLine1 + EnergyLine2) / (BottlesLine1 + BottlesLine2)` Unit: Wh

- PressuredAirPerBottle: `(PressuredAirLine1 + PressuredAirLine2) / (BottlesLine1 + BottlesLine2)` Unit: ml

- WaterPerBottle: `(WaterLine1 + WaterLine2) / (BottlesLine1 + BottlesLine2)` Unit: ml

# Navigation

[Overview](../README.md)

[Configuration Southbound Device ](install_PLC_Devices_Southbound.md)

[Configuration Northbound Device](install_Device_Northbound.md)
