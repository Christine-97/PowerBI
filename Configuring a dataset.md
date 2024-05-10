Exercise: Configuring a dataset


Introduction
You should now understand the fundamentals of configuring datasets and gateways.
In this exercise, you can apply your knowledge of these concepts by following all necessary aspects of deploying and maintaining a dataset.
By completing this exercise, you’ll demonstrate your ability to:
Publish a dataset and configure its gateway.
Authenticate a data source and schedule refresh times.
Endorse the dataset and verify all settings with an on-demand refresh.

Scenario
The Contoso Sales dataset logs sales records for various departments within the organization. Each department has been asked to produce their annual sales report using this dataset. To ensure these reports are accurate, you must publish and configure the dataset and check it’s correctly connected and available.

Instructions
Download the Contoso FactSales.xlsx file and follow the prompts below to complete the exercise.

Step 1: Load and publish the dataset.
Launch a new Power BI Desktop file and import the AdventureWorks FactSales.xlsx file. The file contains multiple tables related to the company’s sales.
Load the Customer, Date, Product, and Sales tables.
Save the Power BI file as AW Sales Dataset.
Log in to Power BI Service and create a new shared workspace named AW Sales.
Upload your content to the new workspace.

Step 2: Configure the connection between the gateway and cloud service
Navigate to the dataset settings. If you have already installed a gateway on your machine, you can verify that it’s active in the dataset from the settings, then move on to Step 3.
If this is your first time connecting a dataset from your machine, you must download and install the gateway.
Sign in with your Power BI Service credentials to finalize the gateway's configuration.
Select the new gateway to be used on the dataset. Verify that it is applied successfully.

Step 3: Authenticate the data source
Navigate to the credentials sector and update the authentication credentials.
Insert the authentication method and privacy level setting.
Sign in on the dataset.

Tip: Don’t worry about which settings you choose. The dataset is used only for this exercise, so there is no difference in the selection.

Step 4: Configure a scheduled refresh
Enable the scheduled refresh.
Set a daily UTC refresh frequency.
Set a three-times-per-day refresh with eight-hour intervals.
Identify the maximum refresh frequency and keep only the three relevant scheduled times.
Apply and confirm your scheduled refresh time.

Step 5: Endorse the dataset and verify all configurations
Promote the dataset to share its accountability.
Make the dataset discoverable to others.
From the workspace view, verify that the dataset scheduled refresh is enabled and is now endorsed.
Perform an on-demand refresh to confirm that all settings are working.

Tip: In a real-case scenario, a thorough testing of the dataset’s data quality should be made beforehand when endorsing a dataset.

Conclusion
In this exercise, you have successfully helped Contoso deploy and maintain a dataset. You’ve also helped to authenticate the data source and schedule refresh times, ensuring the dataset remains updated. And you’ve demonstrated a solid understanding of maintaining data.
You improved data management processes significantly through these steps, showcasing the practical application of acquired skills.

