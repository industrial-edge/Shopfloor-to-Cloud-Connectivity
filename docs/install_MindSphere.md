# Configuration Steps


- [Configuration Steps](#configuration-steps)
- [IIH Mindsphere Sync](#iih-mindsphere-sync)
- [Configure Energy Manager](#configure-energy-manager)
- [Navigation](#navigation)
  
# IIH Mindsphere Sync

No further steps have to be done to connect the data to MindSphere. Data in MindSphere should already be available from [previous steps](install_Device_Northbound.md)

> **_NOTE:_** Continue with [configuration of Energy Manager on MindSphere](#configure-energy-manager)

# Configure Energy Manager

The Energy Manager shows the data from the whole Factory1
  
  ![Mindsphere_EnergyManager1](graphics/Mindspehre_EnergyManager1.png)
  
  ![Mindsphere_EnergyManager2](graphics/Mindspehre_EnergyManager2.png)

1. The handling is the same as described under [Central Device Energy Manager ](install_Device_Northbound.md#northbound-device---energy-manager)
  
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
