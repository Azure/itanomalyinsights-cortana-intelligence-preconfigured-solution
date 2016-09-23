[IT Anomaly Insights Solution](https://gallery.cortanaintelligence.com/solutiontemplate/c0cc7d49409b4be99fa99dcf8ccba98b)
============================================
Sample Data Generator Instructions
----------------------------------
# Overview

Sample data generator is a desktop application which sends sample data to a successfully deployed [IT Anomaly Insights Solution](https://gallery.cortanaintelligence.com/solutiontemplate/c0cc7d49409b4be99fa99dcf8ccba98b). The usage instructions are provided below.

# Instructions

1. Download data generator files from [GitHub location](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/tree/master/Samples/Data-Generator).

2. Launch application VisGenerator.exe from the local folder.
   
3. Provide the following input and click on "Save Configuration Changes".
This is a one-time setting, and will be persisted for future use. You can change the settings any time by stopping the data generator and modifying these inputs and saving them.
![VisGenerator.exe screenshot](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Samples/Data-Generator/figures/sdg_visgenerator.png)

	**Event Hub Name (required):** Event hub name from the deployed solution to which the data generator will send data.
	
	**Event Hub Connection String (required):** Event hub connection string for the event hub provided above
	
	**Path of sample data file: (optional)** Sample data file path on the local machine. If path is not provided a default data file will be used
	
	>Formatting: CSV

	>Schema:
	>
		{
			"Time"        :  DATETIME     (required) "The timestamp of the event in UTC or UNIX timestamp format (Seconds since Epoch)",
			"Value"       :  FLOAT        (required) "The metric value of the event",
			"Metric"      :  VARCHAR(500) (required) "The unique identifier of a particular time series",
			"Host"        :  VARCHAR(100) (required) "The name of the host where the event is fired",
			"Region"      :  VARCHAR(100) (optional) "The region where the event occurs; can be empty",
			"Scenario"    :  VARCHAR(100) (optional) "The scenario to which the event belongs to, can be empty,
			"Category"    :  VARCHAR(100) (optional) "The category associated with the event; can be empty",
			"Application" :  VARCHAR(500) (optional) "Originating application of the event; can be empty",
			"Brand"       :  VARCHAR(500) (optional) "Originating brand of the event; can be empty"
		}
	>
4. Click on Start button to start sending sample data events into the Event Hub.
  
   ![VisGenerator.exe screenshot](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Samples/Data-Generator/figures/sdg_running.png)
   
5. You can stop the generation using the Stop button which will stop sending the events.

6. You can change the configuration by stopping the application, and making changes to the input parameters and clicking "Save Configuration Changes".

###Troubleshooting guide

1. Data generator Start button disabled.
   >Solution: Start button is disabled if either the data generator is not initialized with required inputs like Event Hub name and connection string or if the sample data file path is not valid.
   Please ensure that the required fields are valid. If providing a sample data file, make sure the local path is valid and accessible to the application, schema and format match the requirements mentioned above.

2. Starting the data generator stops with error message.
   >Solution: The error message will indicate why the data generator could not proceed. Please fix the problem and retry. You might have to edit and save the configuration so ensure the 
data generator can pick up the latest changes. If you still notice issues, please follow the below options to reset the data generator.

3. Data generator is not picking up new changes even on editing and saving changes.
   >Solution: You can reset the configs of the data generator by closing the application, going to the directory location of the application and deleting the config file named "ADDataGenConfig.json".
   Once deleted, relaunch the application and make the edits and save again. This should fix the problem.

4. How to update the config file of the data generator in configs
   >Solution: You can set the config of the data generator directly by editing the file named "ADDataGenConfig.json" in the directory location of the application. If this file is not present, start the application and enter any input and click on "Save Configuration Changes" which will force this file to be created. Then you can modify this file directly. Once the application is relaunched it will use this saved config.
   
For any additional questions, please feel free to contact us at adpcs_support@microsoft.com. 