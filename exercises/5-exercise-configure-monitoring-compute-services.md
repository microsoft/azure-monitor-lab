This guided project consists of the four exercises:

- Exercise 1: Deploy Log Analytics
- Exercise 2: Monitor web apps
- **Exercise 3: Configure monitoring for compute services**
- Exercise 4: Configure alerts

In Exercise 3, you configure monitoring for compute services and perform tasks related to integrating IaaS virtual machines with Azure Monitor.

You create a data collection endpoint and a data collection rule to collect Windows Event logs. You then add an existing IIS log collection to the data collection rule. Finally, you configure Network Connection Monitor for a Linux IaaS virtual machine.

- Task 1: Create a data collection endpoint.
- Task 2: Create a data collection rule.
- Task 3: Add an IIS log collection to an existing data collection rule.
- Task 4: Configure Network Connection Monitor for a Linux IaaS virtual machine.

> [!NOTE]
> To complete this lab you will need an [Azure subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_devrel).

This exercise should take approximately **15** minutes to complete.

## Skilling tasks

* Create a data collection endpoint
* Create a data collection rule
* Add an IIS log collection to an existing data collection rule
* Configure Network Connection Monitor for a Linux IaaS virtual machine

## Exercise instructions

### Create a data collection endpoint

1. In the Azure Portal Search Bar, enter **Monitor** and select **Monitor** from the list of results.
2. In the **Monitor** page, under **Settings**, choose **Data Collection Endpoints**.
3. On the **Data Collection Endpoints** page, choose **Create**.
4. On the Create Data Collection Endpoint page, provide the following settings and then choose Review + Create.

   | Property | Value |
   | --- | --- |
   | Endpoint name | IaaSVMCollectionEndpoint |
   | Subscription | Your subscription |
   | Resource Group | rg-alpha |
   | Region | East US |

5. Review the settings and choose **Create**.

### Create a data collection rule

1. In the Azure Portal Search Bar, enter **Monitor** and select **Monitor** from the list of results.
2. In the **Monitor** page, under **Settings**, choose **Data Collection Rules**.
3. On the **Data Collection Rules** page, choose **Create**.
4. On the **Create Data Collection Rule** page, configure the following settings and choose **Next**.

   | Property | Value |
   | --- | --- |
   | Rule name | WinVMDCR |
   | Subscription | Your subscription |
   | Resource Group | rg-alpha |
   | Region | East US |
   | Platform type | Windows |
   | Data collection endpoint | IaaSVMCollectionEndpoint |

5. On the **Resources** page, choose **Add Resources**.
6. On the **Select a scope** page, enable the **WS-VM1** checkbox and choose **Apply**.
7. On the **Create Data Collection Rule** page, choose **Next**.
8. On the **Collect and Deliver** page, choose **Add data source**.
9. On the **Add data source** page, select **Windows Event Logs**. In the **Application** category enable the **Critical** and **Error** categories. In the **Security** category, choose the **Audit Failure** category. In the **System** category, enable the **Critical** and **Error** categories.
10. Choose **Next**.
11. On the **Destination** page, configure the following settings:

    | Property | Value |
    | --- | --- |
    | Destination type | Azure Monitor Logs |
    | Subscription | Your subscription |
    | Account or namespace | LogAnalytics1 |

12. Choose **Add data source**.
13. Choose **Review + Create** and then choose **Create**.

### Add an IIS log collection to an existing data collection rule

1. In the Azure Portal Search Bar, enter **Monitor** and select **Monitor** from the list of results.
2. In the **Monitor** page, under **Settings**, choose **Data Collection Rules**.
3. Choose the **WinVMDRC** rule in rg-alpha.
4. Under **Configuration**, choose **Data Sources**.
5. On the **Data Sources** page, choose **Add**.
6. On the **Add Data Source** page, select **IIS Logs**.
7. Choose **Next**.
8. On the **Destination** page, configure the following settings:

   | Property | Value |
   | --- | --- |
   | Destination type | Azure Monitor Logs |
   | Subscription | Your subscription |
   | Account or namespace | LogAnalytics1 |

9. Choose **Add data source**.

### Configure Network Connection Monitor for a Linux IaaS virtual machine

1. In the Azure Portal Search Bar, enter **Network Watcher** and select **Network Watcher** from the list of results.
2. Under **Monitoring**, choose **Connection Monitor**.
3. On the **Connection Monitor** page, choose **Create**.
4. On the **Basics** page of the **Create Connection Monitor** wizard, provide the following information and choose **Next**.

   | Property | Value |
   | --- | --- |
   | Connection Monitor name | LinuxVMPubIP |
   | Subscription | Your subscription |
   | Region | East US 2 |
   | Workspace | LogAnalytics1 |

5. On the **Add test group details** page, enter the name **LinuxIPTest** and choose **Add sources**.
6. On the **Add Sources** page, select **Azure Endpoints** and set the type to **Virtual machines**. Select **Subnet** and then enable the **Linux-VM** checkbox. Choose **Add Endpoints**.
7. Choose **Add Test Configuration**.
8. On the **Add Test Configuration** page, enter the name **DefaultHTTP** and then choose **Add Test Configuration**.
9. Choose **Add Destinations**. Select **Azure Endpoints** and set the type to **Virtual machines**. Select **Subnet** and then enable the **WS-VM1** checkbox. Select **Add Endpoints**.
10. Choose **Add Test Group**.
11. Choose **Review and Create** and then choose **Create**.


