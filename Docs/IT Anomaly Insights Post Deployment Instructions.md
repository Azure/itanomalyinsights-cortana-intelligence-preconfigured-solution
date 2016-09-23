[IT Anomaly Insights Solution](https://gallery.cortanaintelligence.com/solutiontemplate/c0cc7d49409b4be99fa99dcf8ccba98b)
============================================
# Overview

The IT Anomaly Insights Solution will deploy an end to end solution into your subscription. The goal of this document is to explain
   1. the reference architecture and different azure components provisioned as part of the deployment
   2. how to start sending sample data or real data to the solution to gather anomaly insights, and
   3. how to setup the pre-built Power BI dashboard on your data

# Architecture

The architecture diagram shows various Azure services services that are deployed by [IT Anomaly Insights Solution](https://gallery.cortanaintelligence.com/solutiontemplate/c0cc7d49409b4be99fa99dcf8ccba98b) using [Cortana Intelligence Quick Start](https://start.cortanaintelligence.com), and how they are connected to each other in the end to end solution.  The deployed Azure services include Storage, Event Hubs, Stream Analytics, HDInsight, Data Factory, Azure SQL DB, Application Insights and [Anomaly Detection API](https://datamarket.azure.com/dataset/aml_labs/anomalydetection).  


![IT Anomaly Insights Pipeline Architecture](https://az712634.vo.msecnd.net/solutiontemplates/IT_Operations_Insights_Preconfigured_Solution/Anomaly_detection_Topology1.png)


## Data Source and Ingestion
####Azure Event Hub
The [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) is a highly scalable publish-subscribe service that can ingest millions of events per second and stream them into multiple applications. Here, they are setup to ingest raw timeseries data from a variety of sources such as cloud gateways, monitoring agents, sensors, etc. For quick start, the solution provides a [sample data generator](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/tree/master/Samples/Data-Generator) that can read time series data from CSV file and send it to event hubs. 

## Data Preparation and Analysis

####Azure Stream Analytics
The [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) service is used to aggregate the raw incoming data from the event hubs at 5 mins interval and store it to [Azure Storage](https://azure.microsoft.com/services/storage/) for later processing by [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) service. This job also pushes the time series data to SQL DB to visualize in PowerBI. 

####Azure Data Factory
The [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) service orchestrates the movement and processing of data. The data factory is made up of [pipelines](https://azure.microsoft.com/en-us/documentation/articles/data-factorydata-factory-create-pipelines/) and activities for preparing, analyzing and publishing results. It uses custom activities to read raw data from the input storage tables, prepare individual time series datasets, makes calls to [Anomaly Detection API](https://datamarket.azure.com/dataset/aml_labs/anomalydetection) from Azure Machine Learning for detecting anomalous events and then publishes the results. 

## Data Publishing

####Azure SQL Database Service and Service Bus Topics 
The [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) service is used to store the raw time series and the anomaly scores received from the [Anomaly Detection API](https://datamarket.azure.com/dataset/aml_labs/anomalydetection) so that they can be visualized in [Power BI](https://powerbi.microsoft.com/) dashboard. 
The ADF also publishes any anomalies detected in the current slice to [Service Bus Topics](https://azure.microsoft.com/en-us/documentation/services/service-bus/). These anomaly messages can be subscribed to and consumed by variety of applications such as ticketing systems, chat clients, mobile apps, pagers, etc. 

## Data Consumption

####Power BI
The solutions offers a pre-built [Power BI](https://powerbi.microsoft.com/) dashboard template that can be linked to the deployed and loaded with real time data from your deployment. The dashboard shows views over the raw time series that are monitored by the pipeline and any anomalies detected by the Anomaly Detection API.  The data for the dashboard is sourced from [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) that is deployed with the solution. For Instructions on how to use the Power BI dashboard for this solution, refer to the section below.

# Getting Started After Deployment

Once the solution is deployed to the subscription, you can see the services deployed by clicking the resource group name on the final deployment screen in the CIS. 

![CIS resource group link](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/CIS-resourcegrp.PNG)

This will show all the resources under this resource groups on [Azure management portal](https://portal.azure.com/). After successful deployment, the pipeline is ready to ingest time series data, detect anomalies and push results to dashboard and anomalies to topic queues. 
Here are the next steps: 

###Step 1: Send data to the solution
The [sample data generator](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/tree/master/Samples/Data-Generator), a desktop application, can be run locally to send real data or sample data to the event hub after successful deployment. Alternatively, you can use [Get Started with Event Hubs](https://azure.microsoft.com/en-us/documentation/articles/event-hubs-csharp-ephcs-getstarted/) reference to get sample code for publishing data to event hub. You will find the instructions to download and install this application from Data Generator Instructions (also available in GitHub). Please use the sample that comes with data generator for refering to schema. 
 
####How to bring your own data 
This section describes how to bring your own data to Azure. As long as the events sent to Azure Event Hub follow the required schema, encoding and format, there are no changes required to get the pipeline running

**Encoding:** UTF-8

**Formatting:** JSON

**Schema:**
```
{
	"Host": "Hostname (required)",
	"Metric": "Counter/metric name (required)",
	"Value": "Numeric value (required)",
	"Application": "Originating application of the event (optional)",
	"Category": "Originating category of the event (optional)"
}
```

The Azure Event Hub service is generic and can ingest data in either CSV or JSON format. No special processing occurs in the Azure Event Hub, but it is important you understand the data that is published to it. You can find more details on how to send events or data to an Azure Event Hub in [Event Hub guide](https://azure.microsoft.com/en-us/documentation/articles/event-hubsevent-hubs-programming-guide/).


###Step 2: Monitor pipeline progress
You can do this by looking at the incoming messages on the input event hub, input and output events on ASA, looking at ADF slices (once every 15mins) and finally the output into Sql tables.
----------------
Once the data generator/data source starts sending events, the pipeline starts getting hydrated and the different components of the solution start kicking into action following the commands issued by the Data Factory. The pipeline progress can be monitored using one or more of the following options: 
#### 1. **Check input data in Azure Table Storage and Azure SQL Database.**
The Stream Analytics job writes aggregated incoming data to table storage and SQL database. Click the resource group link on the solution deployment page by first clicking on the deployment name in [CIS](https://start.cortanaintelligence.com/Deployments) to see the deployed solution and the resource group 's resource group on [Azure management portal](https://portal.azure.com/). Once there, click on **Tables**. In the next panel, check if you see the two tables **"asaEgressPartitions"** and **“asaEgress”**. You can also check the if data is being populated in the tables using tools like [Azure Storage Explorer](http://storageexplorer.com/). If you see these tables and data, it indicates that the raw data is successfully being generated on your computer and stored in table storage. 
You can also check the data being populated in SQL database by going to your Resource Group, and locating your database (ex: demo123456db ) and connecting to it using the SQL server username and password provided in the CIQS portal. Once connected, you can check **“AdditionalInfo”** table in the database and make sure it has records being populated by the Stream Analytics Job (e.g. “select count(*) from AdditionalInfo”). 
>
#### 2. **Check the results output data from Azure SQL Database.**
The last step of the pipeline is to write data (e.g. anomalies detected using Machine Learning API) into SQL Database table named **“AdScoreResults”**. You might have to wait for a minimum of 15 minutes for the output data to appear in table. Here, you can query for the number of rows (e.g. "select count(*) from AdScoreResults"). As your database grows, the number of rows in the table should increase.
>
#### 3. **Check Azure Data Factory dashboard.**
The Azure Data Factory service orchestrates the movement and processing of data. You can access your data factory from the Azure management portal resource group (e.x. demo12345adf) . If you see errors under your datasets, you can ignore those as they are due to data factory being deployed before the data generator was started. Those errors do not prevent your data factory from functioning. Read more about monitoring and managing the ADF pipeline [here](https://azure.microsoft.com/en-us/documentation/articles/data-factory-monitor-manage-pipelines/).


###Step 3: Visualize in Power BI
Lastly, you can visualize the output in Power BI using the [PBI template file](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Power-BI-Templates/IT%20Anomaly%20Insights%20Solution%20Dashboard.pbix) on github. See [PBI section](#pbi-setup) for details. 



## Power BI Dashboard <a id="pbi-setup"/>

####Overview
This section describes how to set up Power BI dashboard to visualize the output results of the pipeline. Power BI connects to an Azure SQL database as its data source, where the Machine Learning score results are stored. Below are the steps to setup the Power BI dashboard.
> 1) Get the database server name, database name, user name and password from the deployment summary page.
>    ![SQL Database credentials in deployment summary page](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/SqlServerCredentials.png)
> 2) Update the data source of the Power BI file.
> - Make sure you have the latest version of [Power BI desktop](https://powerbi.microsoft.com/desktop) installed.
> - Download the Power BI desktop file for the solution from [here](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Power-BI-Templates/IT%20Anomaly%20Insights%20Solution%20Dashboard.pbix). The initial visualizations are based on sample data. **Note:** If you see an error message, please make sure you have the latest version of Power BI Desktop installed.
>   Click **‘Edit Queries’** and choose **‘Data Source Settings’** from the menu.
>   
>   ![Changing datasource in Power BI](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/PBI_DataSource_settings.png)
>   
> - The resulting dialog will show SQL Server which is queried to fetch data for Power BI dashboard. Click the **‘Change Source...’** button and replace **‘Server’** and **‘Database’** settings in the resulting dialog with your own server and database names from step 1. Click **‘OK’**.
>   
>   ![Adding your SQL server and database](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/PBI_DataSource_dialog.png)
>   
> - Click **‘Close’** to exit the **‘Data Source Settings’** dialog. A warning will appear prompting you to apply the changes. Click the **‘Apply Changes’** button.
>   
>   ![PBI warning message prompting the user to apply Data Source changes](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/PBI_update_ribbon.png)
>   
> - A dialog prompting the user for Database credentials will appear. Click **‘Database’**, fill in your **‘Username’** and **‘Password’** from step 1. Then click **‘Connect’**.
>   
>   ![Database credentials prompt](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/PBI_SqlServerUsernamePassword_prompt.png)
>   
> - Save the dashboard. Your Power BI file now has an established connection to the server. If your visualizations are empty, make sure you clear the selections on the visualizations to visualize all the data by clicking the eraser icon on the upper right corner of the legends. Use the refresh button to reflect new data on the visualizations. Initially, you will only see the seed data on your visualizations as the data factory is scheduled to refresh every 3 hours. After 3 hours, you will see new scores reflected in your visualizations when you refresh the data.
> 
> 3) (Optional) Publish the dashboard to [Power BI online](http://www.powerbi.com/). Note that this step needs a Power BI account (or Office 365 account).
> - Click **‘Publish’** and few seconds later a window appears displaying "Publishing to Power BI Success!" with a green check mark. To find detailed instructions, see [Publish from Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop).
> - To create a new dashboard: click the + sign next to the **Dashboards** section on the left pane. Enter the name "IT Anomaly Insights" for this new dashboard.
> 
> 4) (Optional) Schedule refresh of the data source.
> - To schedule refresh of the data, hover your mouse over the dataset, click "..." and then choose **Schedule Refresh**. **Note:** If you see a warning massage, click **Edit Credentials** and make sure your database credentials are the same as those described in step 1.
> - Expand the **Schedule Refresh** section. Turn on "keep your data up-to-date". - Schedule the refresh based on your needs. To find more information, see [Data refresh in Power BI](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/).

Pipeline Health Monitoring
--------------------------

This section outlines the steps to monitor if data flowing into the pipeline is successfully scored. Anomaly Detection scoring activity runs inside Azure Data Factory. It fetches input data from Azure Table Storage and passes that data to Machine Learning - Anomaly Detection API for scoring. Scoring results are then persisted in Azure SQL database. Metrics are tracked for every service call. Collected telemetry data is sent to Application Insights (AI) which allows customers to set up monitoring dashboards and alarms.

Steps to set up a sample health dashboard are outlined below.
> 1. The name of Application Insights account will be displayed on the deployment summary page in CIQS. Make a note of it.
>
> 2. Navigate to portal.azure.com and search for the AI account noted above.
>
> 3. Once in the Application Insights blade, click on the "Metric Explorer" button.
>    
>    ![Application Insights Metrics Explorer button] (https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/appInsights_bar.png)
> 
> 4. You should see two blank charts under "Metric Explorer" blade. Click on the “Edit” link in the top right of a blank chart to configure it. 
>    
>    ![Metrics Explorer Blade] (https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/appInsights_metricsExplorer.png)
>
> 5. Pipeline health metrics will be listed under "Custom" section.
>    
>    ![Pipeline health metrics] (https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/appInsights_CustomMetrics.png)
>
> 6. Below is a sample dashboard that gives users a high-level overview of scoring activity health. 
>    
>    ![Sample Pipeline Health Dashboard] (https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/appInsights_sampleDashboard.png)
>    
>    The top chart shows the number of successful and failed Azure Data Factory activity runs. A failed activity run generally indicates that no data has been processed. The next chart below shows the number of successfully scored timeseries. An occasional timeseries evaluation failure is expected, the pipeline is built in such a way that any missing results will be recorded during the next activity run. The next chart shows the number of result rows written to the Azure SQL table. If all datapoints in this chart were zero, it would be an indication that new data stopped flowing into the pipeline. The bottom chart shows the number of anomalies that were successfully published to a Service Bus Topic. Note that non-zero values are expected only when anomalies are detected.

Integrating IT Anomaly Insights Results with On-premise Systems
---------------------------------------------------------------

#### Overview
IT Anomaly Insights PCS will publish Anomaly Detection results to Azure Service Bus Topic. This section covers steps to configure which anomalies will be published to the Service Bus Topic, as well as how to integrate with Service Bus Topics.

#### Configuring Service Bus Topic Result Publishing
Follow the instructions below to learn how to configure the types of anomalies (i.e. spikes, bi-level changes or slow trends) that will be published to Service Bus Topics.

> 1. In Azure Portal navigate to the Resource Group bearing the name of your CIQS project. Find the Data Factory resource.
>    
>    ![How to find ADF resource] (https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/ServiceBus_adfLocation.png)
>
> 2. Click the “Author and deploy” button. Expand “Pipelines” section and select “Anomaly-Detection-Pipeline”.
>    
>    ![ADF blades] (https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/ServiceBus_adfBlades.png)
>
> 3. Azure Data Factory pipeline definition will appear on the right-most blade. 
>    
> 4. Look for “anomalyQuery” parameter under “PublishAnomalies” activity. This query will be run against Azure SQL database where Anomaly Detection results are stored. One Service Bus Topic message will be published for each row returned by the query.
>    
>    The default query (`SELECT * FROM [dbo].[AdScoreResults] WHERE [ScoredTimeseriesEndTimestamp] > @startDateTime AND [ScoredTimeseriesEndTimestamp] <= @endDateTime AND [ZSpike] = 1`) will only publish messages for level spikes. By modifying the query, the user can fine-tune which anomalies (spikes, level changes, trend, etc.) will be published to Service Bus.
>
>    ![ADF pipeline definition] (https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/ServiceBus_adfPipelineDef.png)
>    
> 5. Upon modifying the query, make sure to click the “Deploy” button to save the changes.
>    
>    ![ADF pipeline deploy] (https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/ServiceBus_adfPipelineDeploy.png)

#### Receiving Service Bus Topics Messages

Three pieces of information are needed to start consuming Service Bus Topics messages: topic name, subscription name and Service Bus connection string. All three are provided under “Deployment summary” in CIQS.

There is a wealth of documentation and code samples that show how to receive Service Bus messages from a topic subscription. The following Microsoft documentation [article](https://azure.microsoft.com/en-us/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/) gives a quick overview and provides sample code which will help users integrate their services with Service Bus. 

Service Bus Topics are also supported in Azure WebJobs (see [documentation](https://azure.microsoft.com/en-us/documentation/articles/websites-dotnet-webjobs-sdk-service-bus/)).

Customers who do not have existing infrastructure are encouraged to try [Azure Functions](https://azure.microsoft.com/en-us/documentation/articles/functions-reference/). Azure Functions have built-in Service Bus [support](https://azure.microsoft.com/en-us/documentation/articles/functions-bindings-service-bus/) and allow users to start receiving and processing messages without the cost of infrastructure setup and maintenance. 
