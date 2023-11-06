# Design Rationale

I used Tailwind CSS to design my Flask app. Tailwind CSS is great for those who want to streamline the styling process and promote consistency in design as opposed to writing custom CSS code which requires more time. For my design, I opted for "bg-gray-200 p-4". This was the example code from the class demo and it provided a minimalistic and neutral design. This reads as background color is a shade of gray, and "gray-200" is the specific shade. The "p" represents padding and the "4" corresponds to the specific size o spacing value. Furthermore, "overflow-hidden rounded-lg bg-black" means 'overflow-hidden':setting the CSS property "overflow" to "hidden" (any content overflowing the element's defined boundaries will be hidden from view, and there will not be scrollbars to access the hidden content), 'rounded-lg': rounds the corners, "lg"=large, "sm"=small and "md"=medium, and there is a black background stylistic choice applied.

# How to set up and use CDN with my Flask app

1) I navigated to 'storage accounts' on Azure to create a storage account. I mainly looked at the basics settings with this, just confirm the resource group, and region (my additional preferences include: East US Region, Standard Performance, Geo-redundant Storage, *check* the 'Make read access to data available in the event of regional unavailability'. **NOTE**: For the purpose of this assignment, I had to navigate to advanced settings to *check* 'Require secure transfer for REST API operations', 'Allow enabling anonymous access on individual containers' and'Enable storage account key access'. 

2) Then, I navigated to 'Containers' under the storage account, which essentially acts as a google drive/drop box. I created a container  **NOTE**: For the purpose of this assignment, in the 'Anonymous access level' category, I *checked* Container (anonymous read access for containers and blobs", so anyone can use the items if they have the link. Then, in my container, I uploaded my video. This provided my URL.

3) Next, I went to 'Front Door and CDN' under the storage account, then selecting 'Azure CDN' (service type), and created a new profile. Select the endpoint name and profile name! After creating, a URL endpoint hostname should be created. **NOTE**: When clicking this URL, it will show as invalid query. This is when we navigate back to the URL generated in step 2 (video URL in container with a phrase of 'blob.core.windows.net/') I believe using this original step 2 URL requires the regional data center of the storage account, in this case-US and this will be a bit slower for those in other parts of the world. Therefore, we will copy everything in the link that follows the '/' after 'blob.core.windows.net/' and paste it into the endpoint host name at the end with the addition of a '/' at the end prior to pasting. This will lead to using other data centers across the world closer to the person accessing and therefore load faster.

# Observations and Benefits of using CDN and cloud deployment

### CDN

-Faster Content Delivery because CDNs consist of a network of geophrahically distributed centers (using various data centers)

-Global Scalability because they tolerate spikes of traffic and since it's global, they can distribute this laod across their diverse network of centers

-Security because many CDNs have security features, such as web application firewall, DDoS protection, ect.

The link can load faster using the CDN

### Cloud Deployment

-Scalability because cloud platforms have a lot of resources for you to adjust the demands of your application

-Cost efficient because you pay for what you want to use and can stop/pause when you choose to, which is super handy and I have used multiple times

-Easy to manage because there is so much available and it makes it easy also to set up and maintain what you create/use

# How to deploy the Flask application to Azure

### Make sure you have a requirements.txt file with whatever module you imported in your app file! or else, there will be an error of for example, 'import pandas as pd', followed by 'No module named 'pandas' in the logstream. (Faced this error, initially-screenshot in 'Errors' folder

### Install Azure CLI 

To deploy, install Azure CLI using **'curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash'** This is not a one-time installment! This is done in one command or can be done step-by step following the [instructions](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=apt). Following that, we want to test that it installed with **'az'**. Following would be **'az login --use-device-code'**, which would prompt a code to be copied and pasted in the Microsoft login pop-up.

### Specific to our class/if you suspect the subscription id to be used is set to something else

Get azure student subscription ID **'az account list --output table'** and this would show three subscription IDs to which we would copy the Azure for Students one and paste in the following command **'az account set --subscription [yoursubscriptionID]. This would change the subscription id. 

### Create a new resource group, if you have not done so

Go into the azure web portal and under 'Navigate' in the home page, select 'Resource groups' to create a new resource group and make sure the subscription is for 'Azure for Students'. You can also check the group names using **'az group list'** to see if it already exists.

### Create the azure web app 

The **'az webapp up --resource-group *<groupname>* --name *<app-name>* --runtime <PYTHON:3.9> --sku <B1>'** command is unique to you. The app name is specific. The italicized is unique to you! 

### Deployment

To deploy, use **'az webapp up'** and this takes a while, especially if it's a first time. This will prompt a creating webapp....status code 202...**BE PATIENT**, it will take some time to create! If you click the link too immediately after generating, it will take a while to load and may run into an error 404, check the the app service in Azure and navigate to 'deployments' category to see if it's still loading for a more accurate status on it's completion

My application is (https://flaskappvid.azurewebsites.net/) 


