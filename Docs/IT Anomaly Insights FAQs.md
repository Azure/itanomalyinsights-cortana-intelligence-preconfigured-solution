[IT Anomaly Insights Preconfigured Solution](https://gallery.cortanaintelligence.com/solutiontemplate/c0cc7d49409b4be99fa99dcf8ccba98b)
====================================
Frequently Asked Questions (FAQs)
------------------------------------------

### Deployment Failures 
When the [Cortana Intelligence Quick Start](https://start.cortanaintelligence.com/) (CIQS) portal reports a failure to deploy the solution, please navigate to the Resource Group link provided in the deployment page, which will take you to the Azure portal. Under Settings -> Deployment tab you will be able to see the deployments and get more logs if there were failures. 
Here are the most frequently encountered issues when deploying the solution:
>1. Deployment of Azure Data Factory failed with error code MaxOnDemandComputeCoresReached and message “HDI Not enough cores for deployment”.
**Solution:** ADF reserves a certain number of cores for on-demand clusters in each Azure Region and this message indicated that your subscription has already reached the limit for this region. You will need to delete unused ADF pipelines or preconfigured solutions in order to free up some cores or try deploying in another region that might have room. Alternatively, you can also raise a customer request via Azure portal to increase the ADF reserved quota for HDI cores, for this region if you need more capacity.
2. Deployment latencies – my deployment is taking too long, what is happening?
**Solution:** The solution deploys multiple Azure resources as part of the deployment and customers may notice longer durations occasionally especially in some busy Azure regions. Please try a different region if that is possible or contact us.

Please, feel free to [contact us](adpcs_support@microsoft.com) with any additional questions you might have.
Thanks!
