[IT Anomaly Insights Solution](https://gallery.cortanaintelligence.com/solutiontemplate/c0cc7d49409b4be99fa99dcf8ccba98b)
============================================
# Overview

The IT Anomaly Insights Solution will deploy an end to end solution into your subscription. The goal of this document is to explain
   1. the reference architecture and different azure components provisioned as part of the deployment
   1. how to start sending sample data or real data to the solution to gather anomaly insights
   1. how to consume the results using pre-built Power BI dashboard and alerts using Service Bus Topics, and finally
   1. how to customize the solution 

# Architecture

The architecture diagram shows various Azure services that are deployed by [IT Anomaly Insights Solution](https://gallery.cortanaintelligence.com/solutiontemplate/c0cc7d49409b4be99fa99dcf8ccba98b) using [Cortana Intelligence Solutions](https://start.cortanaintelligence.com), and how they are connected to each other in the end to end solution.  The deployed Azure services include Storage, Event Hubs, Stream Analytics, HDInsight, Data Factory, Azure SQL DB, Application Insights and [Anomaly Detection API](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2).  


![IT Anomaly Insights Pipeline Architecture](https://az712634.vo.msecnd.net/solutiontemplates/IT_Operations_Insights_Preconfigured_Solution/Anomaly_detection_Topology1.png)


## Data Source and Ingestion
#### Azure Event Hub
The [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) is a highly scalable publish-subscribe service that can ingest millions of events per second and stream them into multiple applications. Here, they are setup to ingest raw timeseries data from a variety of sources such as cloud gateways, monitoring agents, sensors, etc. For quick start, the solution provides a [sample data generator](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/tree/master/Samples/Data-Generator) that can read time series data from CSV file and send it to event hubs. 

## Data Preparation and Analysis

#### Azure Stream Analytics
The [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) service is used to aggregate the raw incoming data from the event hubs at 5 mins interval and store it to [Azure Storage](https://azure.microsoft.com/services/storage/) for later processing by [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) service. This job also pushes the time series data to SQL DB to visualize in PowerBI. 

#### Azure Data Factory

The [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) service orchestrates the movement and processing of data. The data factory is made up of [pipelines](https://azure.microsoft.com/en-us/documentation/articles/data-factorydata-factory-create-pipelines/) and activities for preparing, analyzing and publishing results. It uses custom activities to read raw data from the input storage tables, prepare individual time series datasets, makes calls to [Anomaly Detection Web Services](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-apps-anomaly-detection-api) deployed in your solution for detecting anomalous events and then publishes the results. 

#### Azure Machine Learning Web Service
The new [Azure Machine Learning Web Service](https://services.azureml.net/quickstart) deploys the [Anomaly Detection API](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2) into your subscription as part of the deployed solution. The solution will have both non-seasonal and seasonal anomaly detection web services. The default end to end solution uses the non-seasonal web service. More details on customizing the solution to use seasonal web service can be found below. You can manage and monitor the web services via the new [Azure Machine Learning Web Services portal](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-manage-new-webservice). 

## Data Publishing

#### Azure SQL Database Service and Service Bus Topics 

The [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) service is used to store the raw time series and the anomaly scores received from the [Anomaly Detection API](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-apps-anomaly-detection-api) so that they can be visualized in [Power BI](https://powerbi.microsoft.com/) dashboard. 
The ADF also publishes any anomalies detected in the current slice to [Service Bus Topics](https://azure.microsoft.com/en-us/documentation/services/service-bus/). These anomaly messages can be subscribed to and consumed by variety of applications such as ticketing systems, chat clients, mobile apps, pagers, etc. 

## Data Consumption

#### Power BI
The solutions offers two options for visualizing the data and insights in Power BI.

1. an embedded Power BI hosted on a website and deployed as part of the solution.

1. a prebuilt [Power BI template](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Power-BI-Templates/IT%20Anomaly%20Insights%20Solution%20Dashboard.pbix) which can be linked to the deployed solution and loaded with real time data from the deployment. Use this option if you need to customize the dashboard to fit your needs. 

These dashboards show views over the raw time series that are monitored by the pipeline and any anomalies detected by the Anomaly Detection API.  The data for the dashboard is sourced from [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) that is deployed with the solution. For Instructions on how to use the Power BI dashboard for this solution, refer to the section below.

# Getting Started After Deployment

Once the solution is deployed to the subscription, you can see the services deployed by clicking the resource group name on the final deployment screen in the CIS. 

![CIS resource group link](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/CIS-resourcegrp.PNG)

This will show all the resources under this resource groups on [Azure management portal](https://portal.azure.com/). After successful deployment, the pipeline is ready to ingest time series data, detect anomalies and push results to dashboard and anomalies to topic queues. 
Here are the next steps: 

### Step 1: Send data to the solution
The [sample data generator](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/tree/master/Samples/Data-Generator), a desktop application, can be run locally to send real data or sample data to the event hub after successful deployment.  You will find the instructions to download and install this application from [Data Generator Instructions](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/tree/master/Samples/Data-Generator). Please use the sample that comes with data generator for referring to schema. Alternatively, you can use [Get Started with Event Hubs](https://azure.microsoft.com/en-us/documentation/articles/event-hubs-csharp-ephcs-getstarted/) reference to get sample code for publishing data to event hub.
 
#### How to bring your own data 
This section describes how to bring your own data to Azure. As long as the events sent to Azure Event Hub follow the required schema, encoding and format, there are no changes required to get the pipeline running

**Encoding:** UTF-8

**Formatting:** JSON

**Schema:**
```
{
	"Time": "Time of originating event. See note (optional)",
	"Host": "Hostname (required)",
	"Metric": "Counter/metric name (required)",
	"Value": "Numeric value (required)",
	"Application": "Originating application of the event (optional)",
	"Brand": "Originating brand of the event (optional)"
}
```

>Note: By default the event enqueue time is used. Please refer to customizations section for using time column in the event.

The Azure Event Hub service is generic and can ingest data in either CSV or JSON format. No special processing occurs in the Azure Event Hub, but it is important you understand the data that is published to it. You can find more details on how to send events or data to an Azure Event Hub in [Event Hub guide](https://azure.microsoft.com/en-us/documentation/articles/event-hubs-programming-guide/).


### Step 2: Monitor pipeline progress


Once the data generator/data source starts sending events, the pipeline starts getting hydrated and the different components of the solution start kicking into action following the commands issued by the Data Factory. The pipeline progress can be monitored using one or more of the following options: 
#### 1. **Check input data in Azure Table Storage and Azure SQL Database**
The Stream Analytics job writes aggregated incoming data to table storage and SQL database. To check this, first click on the [deployments in CIS](https://start.cortanaintelligence.com/Deployments?type=anomalydetectionpcsv2) to see the deployed solution and then on the resource group which takes you to [Azure management portal](https://portal.azure.com/). Once there, click on the storage account that starts with "stg" and click on **Tables**. In the next panel, check if you see the two tables **"asaEgressPartitions"** and **“asaEgress”**. for this, you can also use tools like [Azure Storage Explorer](http://storageexplorer.com/). If you see these tables and data, it indicates that the raw data is successfully being stored in table storage. 
You can also check the SQL database by and locating your database(ex: demo123456db) and connecting to it using the SQL server username and password provided on the CIS portal. Once connected, you can check **“AdditionalInfo”** table for records populated by the Stream Analytics Job (e.g. “select count(*) from AdditionalInfo”). 

#### 2. **Check the results output data from Azure SQL Database**
The pipeline writes the scored results (e.g. alerts and anomaly scores detected using Machine Learning API) into SQL Database table named **“AdScoreResults”**. *You might have to wait for ~15 minutes for the output data to appear in table.* Here, you can query for the number of rows (e.g. "select count(*) from AdScoreResults") which should increase periodically in a functioning solution.

#### 3. **Check Azure Data Factory dashboard.**
The Azure Data Factory service orchestrates the movement and processing of data. You can access the data factory(ex: demo12345adf) from the resource group on [Azure management portal](https://portal.azure.com/). The data factory datasets will show errors initially if the data is not being streamed to the pipeline. These can be ignored and will go away once the data appears on the input (Refer step 1 above). More info on monitoring and managing the ADF pipeline can be found  [here](https://azure.microsoft.com/en-us/documentation/articles/data-factory-monitor-manage-pipelines/).


### Step 3: Viewing pipeline results in Power BI Embedded
If the data is being sent to the pipeline(step 1) and flowing through the pipeline without errors (step 2), it can be visualized in Power BI.
During the deployment a new [Power BI Embedded](https://docs.microsoft.com/en-us/azure/power-bi-embedded/power-bi-embedded-what-is-power-bi-embedded) workspace collection is provisioned. A dashboard for displaying pipeline results is uploaded to the newly provisioned Power BI Embedded Workspace and a website is deployed to your subscription to display the dashboard via the web browser. A link to the provisioned website is listed under "Next Steps" in CIS portal as shown below.

![The link to provisioned website which displays provisioned Power BI Embedded dashboard](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/epbi_website_link.png)

### Step 4 : (optional) Viewing pipeline results in Power BI Desktop
Optionally, the data and insights can be visualized in Power BI Desktop using the [PBI template file](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Power-BI-Templates/ItAnomalyInsightsSolutionDashboard.pbix) available on GitHub.  


#### Using Power BI template for dashboard<a id="pbi-desktop-setup"/>

This section describes how to set up dashboard in Power BI Desktop to visualize the results of the pipeline. Power BI connects to an Azure SQL database as its data source, where the Machine Learning score results are stored. Below are the steps to setup the Power BI dashboard.

1) Get the database server name, database name, user name and password from the [deployment summary page](https://start.cortanaintelligence.com/Deployments?type=anomalydetectionpcsv2) on CIS
![SQL Database credentials in deployment summary page](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/SqlServerCredentials.png)
2) Update the data source of the Power BI file.
 - Make sure you have the latest version of [Power BI desktop](https://powerbi.microsoft.com/desktop) installed.
 - Download the [Power BI template](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Power-BI-Templates/ItAnomalyInsightsSolutionDashboard.pbix) for the solution. 
 - The initial visualizations are based on sample data. **Note:** If you see an error message, please make sure you have the latest version of Power BI Desktop installed.
 Click **‘Edit Queries’** and choose **‘Data Source Settings’** from the menu.

 ![Changing datasource in Power BI](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/PBI_DataSource_settings.png)
 - The resulting dialog will show SQL Server which is queried to fetch data for Power BI dashboard. Click the **‘Change Source...’** button and replace **‘Server’** and **‘Database’** settings in the resulting dialog with your own server and database names from step 1. Click **‘OK’**.
 
![Adding your SQL server and database](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/PBI_DataSource_dialog.png)
   
- Click **‘Close’** to exit the **‘Data Source Settings’** dialog. A warning will appear prompting you to apply the changes. Click the **‘Apply Changes’** button.
   
![PBI warning message prompting the user to apply Data Source changes](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/PBI_update_ribbon.png)
   
- A dialog prompting the user for Database credentials will appear. Click **‘Database’**, fill in your **‘Username’** and **‘Password’** from step 1. Then click **‘Connect’**.
   
![Database credentials prompt](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/PBI_SqlServerUsernamePassword_prompt.png)
   
- Save the dashboard. Your Power BI file now has an established connection to the server. If your visualizations are empty, make sure you clear the selections on the visualizations to visualize all the data by clicking the eraser icon on the upper right corner of the legends. Use the refresh button to reflect new data on the visualizations. 

3) (Optional) Publish the dashboard to [Power BI online](http://www.powerbi.com/). Note that this step needs a Power BI account (or Office 365 account).
- Click **‘Publish’** and few seconds later a window appears displaying "Publishing to Power BI Success!" with a green check mark. To find detailed instructions, see [Publish from Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop).
- To create a new dashboard: click the + sign next to the **Dashboards** section on the left pane. Enter the name "IT Anomaly Insights" for this new dashboard.
 
4) (Optional) Schedule refresh of the data source.
- To schedule refresh of the data, hover your mouse over the dataset, click "..." and then choose **Schedule Refresh**. **Note:** If you see a warning massage, click **Edit Credentials** and make sure your database credentials are the same as those described in step 1.
- Expand the **Schedule Refresh** section. Turn on "keep your data up-to-date". 
- Schedule the refresh based on your needs. To find more information, see [Data refresh in Power BI](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/).

### Step 5: (Optional) Pipeline Health Monitoring

This section outlines the steps to setup health monitoring for the pipeline in production. Anomaly Detection scoring activity runs inside Azure Data Factory. It fetches input data from Azure Table Storage, passes that data to [Machine Learning - Anomaly Detection API](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-apps-anomaly-detection-api) for scoring and persists the results in Azure SQL database. Metrics are tracked for every service call and the collected telemetry data is sent to Application Insights (AI) which allows setting up monitoring dashboards and alarms.

Steps to set up a sample health dashboard are outlined below.
  1. The name of Application Insights account will be displayed on the deployment summary page in Cortana Intelligence Solution. Make a note of it.
  2. Navigate to  [Azure Management Portal](https://portal.azure.com/). and search for the AI account noted above.
  3. Once in the Application Insights blade, click on the "Metric Explorer" button.
    
   ![Application Insights Metrics Explorer button](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/appInsights_bar.png)
   
  4. You should see two blank charts under "Metric Explorer" blade. Click on the “Edit” link in the top right of a blank chart to configure it. 
   
  ![Metrics Explorer Blade](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/appInsights_metricsExplorer.png)
  
  5. Pipeline health metrics will be listed under "Custom" section.
   
   ![Pipeline health metrics](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/appInsights_CustomMetrics.png)

  6. Below is a sample dashboard that gives users a high-level overview of scoring activity health. 
    
 ![Sample Pipeline Health Dashboard](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/appInsights_sampleDashboard.png)
  
 The top chart shows the number of successful and failed Azure Data Factory activity runs. A failed activity run generally indicates that no data has been processed. The next chart below shows the number of successfully scored timeseries. An occasional timeseries evaluation failure is expected, the pipeline is built in such a way that any missing results will be recorded during the next activity run. The next chart shows the number of result rows written to the Azure SQL table. If all datapoints in this chart were zero, it would be an indication that new data stopped flowing into the pipeline. The bottom chart shows the number of anomalies that were successfully published to a Service Bus Topic. Note that non-zero values are expected only when anomalies are detected.

### Step 6: (Optional) Integrating IT Anomaly Insights Results with On-premise Systems
IT Anomaly Insights solution publishes anomalies to Azure Service Bus Topic. This section covers steps to configure anomalies to publish to the Service Bus Topic, and how to integrate with Service Bus Topics.

#### Configuring anomaly publishing to Service Bus Topic
Follow the instructions below to configure the types of anomalies (i.e. spikes, bi-level changes or slow trends) to publish to Service Bus Topics.
  1. In Azure Portal navigate to the Resource Group bearing the name of your Cortana Intelligence Solutions project. Find the Data Factory resource.
   
  ![How to find ADF resource](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/ServiceBus_adfLocation.png)

  2. Click the “Author and deploy” button. Expand “Pipelines” section and select “Anomaly-Detection-Pipeline”.
   
   ![ADF blades](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/ServiceBus_adfBlades.png)

  3. Azure Data Factory pipeline definition will appear on the right-most blade. 
   
  4. Look for “anomalyQuery” parameter under “PublishAnomalies” activity. This query will be run against Azure SQL database where Anomaly Detection results are stored. One Service Bus Topic message will be published for each row returned by the query.
    
   The default query (`SELECT * FROM [dbo].[AdScoreResults] WHERE [ScoredTimeseriesEndTimestamp] > @startDateTime AND [ScoredTimeseriesEndTimestamp] <= @endDateTime AND [ZSpike] = 1`) will only publish spike anomalies. By modifying the query, the user can fine-tune which anomalies (spikes, level changes, trend, etc.) to publish to Service Bus. (Refer to the 'Output' section on [Anomaly Detection API](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-apps-anomaly-detection-api) to understand the column names and their meaning)

   ![ADF pipeline definition](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/ServiceBus_adfPipelineDef.png)
   
  5. Upon modifying the query, make sure to click the “Deploy” button to save the changes.
    
   ![ADF pipeline deploy](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/ServiceBus_adfPipelineDeploy.png)

#### Receiving anomalies from Service Bus Topics

Three pieces of information are needed to start consuming Service Bus Topics messages: topic name, subscription name and Service Bus connection string. All three are provided under “Deployment summary” in Cortana Intelligence Solution.

There is a wealth of documentation and code samples that show how to receive Service Bus messages from a topic subscription. The following Microsoft documentation [article](https://azure.microsoft.com/en-us/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/) gives a quick overview and provides sample code which will help users integrate their services with Service Bus. 

Service Bus Topics are also supported in Azure WebJobs (see [documentation](https://azure.microsoft.com/en-us/documentation/articles/websites-dotnet-webjobs-sdk-service-bus/)).

Customers who do not have existing infrastructure are encouraged to try [Azure Functions](https://azure.microsoft.com/en-us/documentation/articles/functions-reference/). Azure Functions have built-in Service Bus [support](https://azure.microsoft.com/en-us/documentation/articles/functions-bindings-service-bus/) and allow users to start receiving and processing messages without the cost of infrastructure setup and maintenance. 


# Customizing Solution


## Using event time
By default, events are timestamped based on their arrival time to the Event Hub. But in some scenarios, the time at which the event occurred might be more useful. For such cases, we can modify the solution to use the time column in the event by simply adding the 'TIMESTAMP BY Time" clause in the Azure Stream Analytics job which processes the input events. For this, make sure that the events have this Time field present and have valid datetime value.
 
**Modify Azure Stream Analytics job** 
    
1. In Azure portal click "Resource groups" and find the resource group that has the same name as your solution. The resource group should contain one Stream Analytics resource. Click on it.
    
   ![Resource Groups in Azure Portal with Stream Analytics resource](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/SchemaChange_SA_resource.png)

2. Stop the Stream Analytics job and click "Query" under "Job Topology".
    
   ![Stream Analytics Azure Portal blade](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/SchemaChange_SA_blade.png)
    
3. The blade that opens will have three Azure Stream Analytics queries (for more information on syntax, please refer to [Stream Analytics Query Language Reference](https://msdn.microsoft.com/en-us/library/azure/dn834998.aspx)). Modify all the three queries to add a "TIMESTAMP BY Time" clause like in the sample query [here](https://msdn.microsoft.com/en-us/library/azure/mt573293.aspx).

4. Save your changes and re-start Stream Analytics job.

## Adding new dimensions

Suppose that in Power BI dashboard we want to see event breakdown by geographic region. This section will guide you through the steps to customize your deployed solution and the accompanying [Power BI template](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Power-BI-Templates/IT%20Anomaly%20Insights%20Solution%20Dashboard.pbix).

Each event will need to report the region where it originates. Therefore, the event schema above will need to be modified to add "Region" field as follows.

```
{
	"Host": "Hostname (required)",
	"Metric": "Counter/metric name (required)",
	"Value": "Numeric value (required)",
	"Application": "Originating application of the event (optional)",
	"Brand": "Originating brandof the event (optional)",
	"Region": "Originating region of the event (optional)"
}
```

1. **Modify Azure SQL database table schema** 
    
    First, we will need to modify Azure SQL database schema. Deployment summary page will list database credentials we can use to connect to the database.
    
    ![Azure SQL credentials](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/SqlServerCredentials.png)
 
    We will need to connect to the database and run the following two queries:

    ```sql
    ALTER TABLE [dbo].[AdditionalInfo] ADD Region VARCHAR(2000);
    ```

    ```sql
    ALTER VIEW [dbo].[view_AdditionalInfo]
    AS
    (
        SELECT             [InputTimestamp],
            [HostnameMetricname],
            [MetricName],
            [HostName],
            [EventVolumePerHost],
            [Application],
            [Brand],
            [Region]
        FROM [dbo].[AdditionalInfo] WITH (NOLOCK)
        WHERE [InputTimestamp] >= DATEADD(DAY,-3,GETDATE())
    )
    ```

2. **Modify Azure Stream Analytics job** 
    
    Next, we will modify Azure Stream Analytics job to persist the "Region" field of the incoming events into Azure SQL database table.
    
    In Azure portal click "Resource groups" and find the resource group that has the same name as your solution. The resource group should contain one Stream Analytics resource. Click on it.
    
    ![Resource Groups in Azure Portal with Stream Analytics resource](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/SchemaChange_SA_resource.png)

    Stop the Stream Analytics job and click "Query" under "Job Topology".
    
    ![Stream Analytics Azure Portal blade](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/SchemaChange_SA_blade.png)
    
    The blade that opens will have three Azure Stream Analytics queries (for more information on syntax, please refer to [Stream Analytics Query Language Reference](https://msdn.microsoft.com/en-us/library/azure/dn834998.aspx)). Modify the third query to match the query below:
   
    ```sql
    SELECT 
        CONCAT('All hosts', '-', REPLACE(REPLACE(REPLACE(REPLACE(Metric, '/', ' '), '\', ' '), '#', ' '), '?' , ' ')) AS HostnameMetricname,
        System.TIMESTAMP as InputTimestamp, 
        [Metric] as MetricName, 
        [Host] as HostName, 
        count(Host) as EventVolumePerHost, 
        [Application] as Application, 
        [Brand] as Brand,
        [Region] as Region
    INTO [asaEgressSqlDb] 
    FROM [asaIngress] 
        GROUP BY TumblingWindow(Minute, 5), [Metric], [Host], [Application], [Brand], [Region]
    ```
    
    Save your changes and re-start Stream Analytics job.

3. **Modify Power BI dashboard**

    Finally, we will add a visualization in our Power BI dashboard which will display event counts grouped by region. Note that having Power BI dashboard connect to your Azure SQL database is a prerequisite for this step. If you haven't done that yet, please refer to the [instructions](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/IT%20Anomaly%20Insights%20Post%20Deployment%20Instructions.md#power-bi-dashboard-) on how to do it.

    Open your Power BI dashboard and click "Edit Queries".
    
    ![Edit Queries button in Power BI](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/SchemaChange_PBI_editqueries.png)
    
    In Power BI query editor window click "Refresh Preview" to update the data. Make sure that "view_AdditionalInfo" is selected in the left panel. Ensure that "Region" column is being populated. Note that this column is expected to be populated only for records written after modifying Stream Analytics job in step 2. Rows corresponding to the events written prior to that will have null values.
    
    ![Power BI Query Editor](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/SchemaChange_PBI_queryEditor.png)

    Close Power BI Query Editor window.

    Click "Refresh" to refresh Power BI dashboard. Under "Visualizations" pick "Table". Select "Region" and "EventVolumePerHost" under "Fields". Now you can see the event breakdown by region. 

    ![Event breakdown by regions](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/SchemaChange_PBI_add_visualization.png)



# Customizing Solution: Using Seasonal Anomaly Detection Web Service
The solution comes with both non-seasonal and seasonal anomaly detection web services. Based on the characteristics of the data, you might want to pick the right web service. For seasonal data, below are the steps to configure the solution to use the seasonal endpoint.

Step 1: Get the Anomaly Detection Seasonal Web Service API URL from the deployment summary page on [CIS](https://start.cortanaintelligence.com/Deployments?type=anomalydetectionpcsv2)

Step 2: Sign into Azure ML Web services portal and go to the seasonal web service URI obtained from step 1. Get the Primary Key and Request Response endpoint for the Seasonality Web Service.

Step 3: Modify ADF to use the seasonal web service API and key along with the right parameter for the anomaly detection seasonality models.

1. In Azure Portal navigate to the Resource Group bearing the name of your Cortana Intelligence Solutions project. Find the Data Factory resource.
   
  ![How to find ADF resource](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/ServiceBus_adfLocation.png)

2. Click the “Author and deploy” button. Expand “Pipelines” section and select “Anomaly-Detection-Pipeline”.
	![ADF blades](https://github.com/Azure/itanomalyinsights-cortana-intelligence-preconfigured-solution/blob/master/Docs/figures/ServiceBus_adfBlades.png)

3. Azure Data Factory pipeline definition will appear on the right-most blade. 
   
4. Look for “AnalyzeData” activity and update the following parameters
	- **entryPoint**: Activity entry point
	- **mLEndpointBatchLocation**: Azure ML Web Service Seasonality Request Response API (Note: make sure to remove  ‘&swagger=true’ at the end of the URL)
	- **mLEndpointKey**: Primary web service key 
	- **mLParams**: Parameters to the seasonality API. For more information on the API, refer to [Anomaly Detection API](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-apps-anomaly-detection-api) documentation page.
	
	The below snippet shows the required changes in the pipeline activity code

```
	{
                "type": "DotNetActivity",
                "typeProperties": {
                    "assemblyName": "AnomalyDetectionCustomActivities.dll",
                    "entryPoint": " AnomalyDetectionCustomActivity.Activities.AzureMlWebServiceSeasonalityActivity",
                    "packageLinkedService": "AzureStorage-LinkedService",
                    "packageFile": "anomalydetection/AnomalyDetectionCustomActivity.zip",
                    "extendedProperties": {
                        "telemetryInstrumentationKey": "****",
                        "mLEndpointBatchLocation": "<Azure ML Web Service Seasonality API  for Request Response",
                        "mLEndpointKey": "<Primary key for above AML web service>",
                        "mLParams": "{\"postprocess.tailRows\": 0, \"preprocess.aggregationInterval\": 0, \"preprocess.aggregationFunc\": \"mean\", \"preprocess.replaceMissing\": \"lkv\", \"seasonality.enable\": true, \"seasonality.numSeasonality\": 2, \"seasonality.transform\": \"deseason\", \"tspikedetector.sensitivity\": 3, \"zspikedetector.sensitivity\": 3, \"detectors.spikesdips\": \"Both\", \"detectors.historywindow\": 500, \"negtrenddetector.sensitivity\": 3.25, \"bileveldetector.sensitivity\": 3.25, \"postrenddetector.sensitivity\": 3.25 }",
                        "timeseriesStartTime": "$$Text.Format('{0:yyyy-MM-ddTHH:mm:ss.fffffffZ}', Time.AddHours(SliceEnd, -72))",
                        "timeseriesEndTime": "$$Text.Format('{0:yyyy-MM-ddTHH:mm:ss.fffffffZ}', SliceEnd)"
                 }
	}
```

Upon modifying the query, make sure to click the “Deploy” button to save the changes.
