This guided project consists of the four exercises:

- Exercise 1: Deploy Log Analytics
- **Exercise 2: Monitor web apps**
- Exercise 3: Configure monitoring for compute services
- Exercise 4: Configure alerts

In Exercise 2, you configure monitoring for web applications.

- Task 1: Enable Application Insights.
- Task 2: Disable logging for .NET core snapshot debugger.
- Task 3: Configure web app HTTP logs to be written to a Log Analytics workspace.
- Task 4: Configure SQL Insights data to be written to a Log Analytics workspace.
- Task 5: Enable file and configuration change tracking for web apps.

Launch the exercise and follow the instructions. When you're done, be sure to return to this page so you can continue learning.

> [!NOTE]
> To complete this lab you will need an [Azure subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_devrel).

This exercise should take approximately **20** minutes to complete.

## Skilling tasks

* Enable Application Insights
* Disable logging for .NET core snapshot debugger
* Configure web app HTTP logs to be written to a Log Analytics workspace
* Configure SQL Insights data to be written to a Log Analytics workspace
* Enable file and configuration change tracking for web apps

## Exercise instructions

### Enable Application Insights

1. In the Azure Portal Search Bar, enter **rg-alpha** and select **rg-alpha** from the list of results.
2. From the list of items in the resource group, choose **App Services for the Web App with an SQL Database**.
3. Under **Monitoring** choose **Application Insights**.
4. On the **Application Insights** page, choose **Turn On Application Insights**.
5. On the **Application Insights** page, ensure that **Create a new resource** is selected and that the Log Analytics Workspace is set to **LogAnalytics1** and choose **Apply**.
6. On the **Apply monitoring settings** dialog, choose **Yes**.

### Disable logging for .NET core snapshot debugger

1. In the Azure Portal Search Bar, enter **rg-alpha** and select **rg-alpha** from the list of results.
2. From the list of items in the resource group, choose **App Services for the Web App with an SQL Database**.
3. Under **Monitoring** choose **Application Insights**.
4. Under **Instrument your application**, choose **.NET Core** and then set the Snapshot Debugger setting to **Off**. Choose **Apply**.
5. On the **Apply Monitoring Settings** dialog box, choose **Yes**.

### Configure web app HTTP logs to be written to a Log Analytics workspace

1. In the Azure Portal Search Bar, enter **rg-alpha** and select **rg-alpha** from the list of results.
2. From the list of items in the resource group, choose **App Services for the Web App with an SQL Database**.
3. Under **Monitoring**, choose **Diagnostic settings**.
4. On the **Diagnostic settings** page, select **+ Add diagnostic settings**.
5. On the **Diagnostic settings** page, choose the following and select **Save**.

   | Property | Value |
   | --- | --- |
   | Diagnostic setting name | httplogs |
   | Categories | HTTP logs |
   | Destination details | Send to Log Analytics workspace |
   | Subscription | Your subscription |
   | Log Analytics workspace | LogAnalytics1 |

### Configure SQL Insights data to be written to a Log Analytics workspace

1. In the Azure Portal Search Bar, enter **rg-alpha** and select **rg-alpha** from the list of results.
2. From the list of items in the resource group, choose the sample SQL database.
3. Under **Monitoring**, choose **Diagnostic settings**.
4. On the **Diagnostic settings** page, choose **Add diagnostic setting**.
5. On the **Diagnostic setting page**, provide the following information and choose **Save**.

   | Property | Value |
   | --- | --- |
   | Diagnostic setting name | InsightLogAnalytics |
   | Categories | SQL Insights |
   | Destination details | Send to Log Analytics workspace |
   | Subscription | Your subscription |
   | Log Analytics workspace | LogAnalytics1 |

Next step: [Monitor Compute Services] (https://microsoft.github.io/azure-monitor-lab/instructions/05-execise-configure-monitoring-compute-services/)

[Click here to navigate to this page on the GitHub repo if not using pages](https://github.com/microsoft/azure-monitor-lab/blob/main/instructions/05-exercise-configure-monitoring-compute-services/index.md)
