# Configuration Steps


- [Configuration Steps](#configuration-steps)
- [IIH Insights Hub Sync](#iih-insights-hub-sync)
- [Configure Energy Manager](#configure-energy-manager)
- [Navigation](#navigation)
  
# IIH Insights Hub Sync

To analyze incoming data from the Shopfloor-To-Cloud edge device in Insights Hub Cloud, you can use the Energy Manager application to create dashboards so you can process and display the supplied data.

For this, the following dashboards are created using the data collected from the Shopfloor:

1) **Overview:**
- Produced Bottles of Each Line
- Consumption Graphic of Each Line
- Cost of each Line

2) **Line 1 - Media Consumption:**
- Energy per Bottle
- Water per Bottle
- Pressured Air per Bottle
- Consumption per Bottle
- Cost per Bottle

3) **Line 2 - Media Consumption:**
- Energy per Bottle
- Water per Bottle
- Pressured Air per Bottle
- Consumption per Bottle
- Cost per Bottle

# Configure Energy Manager

From here, the step-by-step process of creating each dashboard will be explained.

## Overview Dashboard

Let's start by builidng the **Overview** dashboard. This is the final result of the dashboard:

<img id="Overview" src="graphics/OVERVIEW_DASHBOARD.png" alt="OVERVIEW" width="900"/>

Now, create a new dashboard by going to *My Plant*, select the asset where the variables are added, click on "Add dashboard" and name it "Overview":

<img id="add_new_dasboard" src="graphics/Insights1.png" alt="CreateDashboard2" width="900"/>

### Create widget for Produced Bottles of Each Line:

Here, the creation of this section of the dashboard will be explained:

<img id="value" src="graphics/Value.png" alt="Value" width="900"/>

To do that, in the created dashboard, proceed to create a widget. 

<img id="add_widget" src="graphics/addwidget.png" alt="KPI" width="900"/>

Create a "Value" widget to display the Produced Bottles of the Line 1 and attach it to the "Line1_ProducedBottles", like so:

<img id="tag1" src="graphics/tag1.png" alt="Tag1" width="900"/>

Chosse the KPI Calculation Period of your preference. Then, just click save, place the widget in the dashboard layout and repeat the same proccess for Line 2.

### Create widget for Consumption Graphic of Each Line

Here, the creation of this section of the dashboard will be explained:

<img id="graphic1" src="graphics/Graphic.png" alt="Graphic" width="900"/>

To do that, create a "Diagram" widget and attach it to the following parameters:

<img id="tag2" src="graphics/tag2.png" alt="Tag2" width="900"/>

And make sure to have this Y-Axis configuration:

<img id="yaxis" src="graphics/yaxis.png" alt="yaxis" width="900"/>

Chosse the KPI Calculation Period of your preference. Then, just click save, place the widget in the dashboard layout and repeat the same proccess for Line 2.

### Create widget for Cost of each Line

Here, the creation of this section of the dashboard will be explained:

<img id="cost" src="graphics/cost.png" alt="cost" width="900"/>

For this widget, the following KPI type needs to be created:

<img id="KPI" src="graphics/KPI1.png" alt="KPI" width="900"/>

In order to do that, go to *Energy Manager UI > Configuration > KPI Types* and create a new KPI type with the information provided in the picture above.

Then, create a KPI instance named "CostLine1" based on the previously created KPI type, like so:

<img id="CostLine1" src="graphics/CostLine1.png" alt="CostLine1" width="900"/>

Now, create a "Gauge" widget and attach it to the KPI instance you just created:

<img id="CostLine1_tag" src="graphics/costline_tag.png" alt="CostLine1_tag" width="900"/>

Then, just click save, place the widget in the dashboard layout and repeat the same proccess for Line 2.

You just created the "Overview" Dashboard !

## Line 1 - Media Consumption Dashboard

This is the final result of the dashboard:

<img id="Line1_media" src="graphics/LINE1_MEDIACOMSUMPTION.png" alt="Line1-media-consumption" width="900"/>

Create a new dashboard by going to *My Plant*, select the asset where the variables are added, click on "Add dashboard" and name it "Line 1 - Media Consumption".

### Create widget for Energy Per Bottle:

Here, the creation of this section of the dashboard will be explained:

<img id="energy" src="graphics/energyPerBottle.png" alt="energyPerBottle" width="900"/>

For this widget, create the following KPI type:

<img id="energyPerBottle" src="graphics/energyxbottle.png" alt="energyPerBottle" width="900"/>

Then, create a KPI instance named "EnergyPerBottleLine1" based on the previously created KPI type, like so:

<img id="EnergyPerBottleLine1" src="graphics/EnergyPerBottleLine1.png" alt="EnergyPerBottleLine1" width="900"/>

Now, create a "Gauge" widget and attach it to the KPI instance you just created:

<img id="EnergyLine1Gauge" src="graphics/EnergyLine1Gauge.png" alt="EnergyLine1Gauge" width="900"/>

Then, just click save, place the widget in the dashboard layout and repeat the same proccess for Line 2.






### Create widget for Water per Bottle:

Here, the creation of this section of the dashboard will be explained:

<img id="WaterPerBottleWidget" src="graphics/WaterPerBottleWidget.png" alt="WaterPerBottleWidget" width="900"/>

For this widget, create the following KPI type:

<img id="WaterPerBottleKPIType" src="graphics/WaterPerBottleKPIType.png" alt="WaterPerBottleKPIType" width="900"/>

Then, create a KPI instance named "WaterPerBottleLine1" based on the previously created KPI type, like so:

<img id="WaterPerBottleLine1" src="graphics/WaterPerBottleLine1.png" alt="WaterPerBottleLine1" width="900"/>

Now, create a "Gauge" widget and attach it to the KPI instance you just created:

<img id="WaterPerBottleGauge" src="graphics/WaterPerBottleGauge.png" alt="WaterPerBottleGauge" width="900"/>

Then, just click save, place the widget in the dashboard layout and repeat the same proccess for Line 2.



### Create widget for PressuredAir per Bottle:

Here, the creation of this section of the dashboard will be explained:

<img id="PressuredAirPerBottleWidget" src="graphics/PressuredAirPerBottle_Widget.png" alt="PressuredAirPerBottleWidget" width="900"/>

For this widget, create the following KPI type:

<img id="PressuredAirPerBottleKPIType" src="graphics/PressuredAirPerBottleKPIType.png" alt="PressuredAirPerBottleKPIType" width="900"/>

Then, create a KPI instance named "PressuredAirPerBottleLine1" based on the previously created KPI type, like so:

<img id="PressuredAirPerBottleLine1" src="graphics/PressuredAirPerBottleLine1.png" alt="PressuredAirPerBottleLine1" width="900"/>

Now, create a "Gauge" widget and attach it to the KPI instance you just created:

<img id="PressuredAirPerBottleGauge" src="graphics/PressuredAirPerBottleGauge.png" alt="PressuredAirPerBottleGauge" width="900"/>

Then, just click save, place the widget in the dashboard layout and repeat the same proccess for Line 2.



### Create widget for Consumption Per Bottle:

Here, the creation of this section of the dashboard will be explained:

<img id="ConsumptionDiagram" src="graphics/ConsumptionDiagram.png" alt="ConsumptionDiagram" width="900"/>

Now, create a "Diagram" widget and attach it to the following KPI instances:

<img id="ConsumptionPerBottleDiagram" src="graphics/ConsumptionPerBottleDiagram.png" alt="ConsumptionPerBottleDiagram" width="900"/>

And make sure to have this Y-Axis configuration:

<img id="ConsumptionDiagramYaxis" src="graphics/ConsumptionDiagramYaxis.png" alt="ConsumptionDiagramYaxis" width="900"/>

Then, just click save, place the widget in the dashboard layout and repeat the same proccess for Line 2.



### Create widget for Cost per Bottle (Gauge):

Here, the creation of this section of the dashboard will be explained:

<img id="CostGauge" src="graphics/CostGauge.png" alt="CostGauge" width="900"/>

For this widget, create the following KPI type:

<img id="CostPerBottleKPIType" src="graphics/CostPerBottleKPIType.png" alt="CostPerBottleKPIType" width="900"/>

Then, create a KPI instance named "CostPerBottleLine1" based on the previously created KPI type, like so:

<img id="CostPerBottleKPIInstance" src="graphics/CostPerBottleKPIInstance.png" alt="CostPerBottleKPIInstance" width="900"/>

Now, create a "Gauge" widget and attach it to the KPI instance you just created:

<img id="CostPerBottleGauge" src="graphics/CostPerBottleGauge.png" alt="CostPerBottleGauge" width="900"/>

Then, just click save, place the widget in the dashboard layout and repeat the same proccess for Line 2.


### Create widget for Cost per Bottle (Diagram):

Here, the creation of this section of the dashboard will be explained:

<img id="CostDiagram" src="graphics/CostDiagram.png" alt="CostDiagram" width="900"/>

Now, create a "Diagram" widget and attach it to the following KPI instance:

<img id="CostDiagramKPIInstance" src="graphics/CostDiagramKPIInstance.png" alt="CostDiagramKPIInstance" width="900"/>

Then, just click save, place the widget in the dashboard layout and repeat the same proccess for Line 2.


## Line 2 - Media Consumption Dashboard

This is the final result of the dashboard:

<img id="LINE2_MEDIACONSUMPTION" src="graphics/LINE2_MEDIACONSUMPTION.png" alt="LINE2_MEDIACONSUMPTION" width="900"/>

Create a new dashboard by going to *My Plant*, select the asset where the variables are added, click on "Add dashboard" and name it "Line 2 - Media Consumption".

Follow the same steps you took to create the 'Line 1 - Media Consumption' dashboard.

Now all dashboards have been created, demonstrating the purpose of this app example.

# Navigation

[Overview](../README.md)

[Configuration Southbound Device ](install_PLC_Devices_Southbound.md)

[Configuration Northbound Device](install_Device_Northbound.md)
