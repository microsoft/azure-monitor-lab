This guided project consists of the four exercises:

- **Exercise 1: Deploy Log Analytics**
- Exercise 2: Monitor web apps
- Exercise 3: Configure monitoring for compute services
- Exercise 4: Configure alerts

In Exercise 1, you deploy and configure a Log Analytics workspace

- Task 1: Create a Log Analytics workspace.
- Task 2: Configure Log Analytics data retention and archive policies.
- Task 3: Enable access to a Log Analytics workspace.

> [!NOTE]
> To complete this lab you will need an [Azure subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_devrel).

I'll fetch that page and convert it to markdown for you.Here's the page converted to clean markdown:

## Skilling tasks

This exercise should take approximately **10** minutes to complete.

### Skilling tasks

* Create a Log Analytics workspace
* Configure Log Analytics data retention and archive policies
* Enable access to a Log Analytics workspace

## Exercise instructions

### Create a Log Analytics workspace

1. In the Azure Portal Search Bar, enter **Log Analytics** and select **Log Analytics workspaces** from the list of results.
2. On the **Log Analytics workspaces** page, choose **Create**.
3. On the **Basics** page of the Create Log Analytics workspace wizard, provide the following information and choose **Review + Create**.

   | Property | Value |
   | --- | --- |
   | Subscription | Your subscription |
   | Resource Group | rg-alpha |
   | Name | LogAnalytics1 |
   | Region | East US |

4. Choose **Review + Create**.
5. Review the information and choose **Create**.

### Install and configure the Azure Monitor Agent on Linux-VM using a Data Collection Rule

1. In the Azure Portal, enter **Data Collection Rules** in the search bar and select **Data Collection Rules** from the results.
2. Select **+ Create** to start a new data collection rule.
3. On the **Basics** page, provide the following:
   * **Rule name:** DCR-Linux-VM
   * **Subscription:** Your subscription
   * **Resource Group:** rg-alpha
   * **Region:** East US (choose the region matching your VM/workspace)
   * **Platform type:** Select Linux
   * Select **Next: Resources >**
4. Under **Resources**, select **+ Add resources**.
   * Search for and select **Linux-VM**.
   * Select **Apply**.
   * Select **Next: Collect and deliver >**
5. In the **Collect and deliver** tab:
   * Select **+ Add data source**.
   * For **Data source type**, choose **Performance Counters**.
   * Select **Next: Destination >**.
   * Select **+ Add destination**.
   * Under **Destination type** choose **Azure Monitor Logs**.
   * Under **Destination Details** choose **LogAnalytics1 (rg-alpha)**.
   * Select **Add data source**.
   * Select **Next: Review + create**
6. On the **Review + create** page, review your selections, and select **Create** to deploy the DCR.

> **Note:** Assigning a DCR to a VM automatically deploys the Azure Monitor Agent extension to the VM. You do **NOT** need to manually add the agent in the Extensions blade.

#### Verify agent installation and data ingestion:

1. In the Azure Portal, use the search bar to search for **Log Analytics workspaces** and select it from the results.
2. In the list of workspaces, select **LogAnalytics1**.
3. In the left-hand menu of the LogAnalytics1 workspace, select **Logs**.
4. Use the mode drop-down to change from **Simple mode** to **KQL mode**.
5. In the query window, enter the following query:

   ```
   Heartbeat
   | where Computer contains "Linux-VM"
   | sort by TimeGenerated desc
   ```

6. Select **Run** or press **Shift + Enter** to execute the query.
7. If results are returned, data is flowing and the Azure Monitor Agent is working.

### Configure Log Analytics data retention and archive policies

1. In the Azure Portal Search Bar, enter **Log Analytics** and select **Log Analytics workspaces** from the list of results.
2. On the **Log Analytics workspaces** page, choose **LogAnalytics1**.
3. On the **Log Analytics workspace** page for LogAnalytics1, under **Settings**, choose **Usage and estimated costs**.
4. Select **Data Retention** and set the slider to 60 days. Select **OK**.
5. On the **Log Analytics workspace** page for LogAnalytics1, choose **Usage and estimated costs**.
6. Select **Daily cap**. Select **On**. Set the daily cap to 10 GB and select **OK**.

### Enable access to a Log Analytics workspace

1. In the Azure Portal Search Bar, enter **Log Analytics** and select **Log Analytics workspaces** from the list of results.
2. On the **Log Analytics workspaces** page, choose **LogAnalytics1**.
3. Select **Access control (IAM)**.
4. Choose **Add** and then choose **Add role assignment**.
5. On the list of roles, select **Log Analytics Reader** and choose **Next**.
6. On the **Members** page, choose **Select Members** and choose the App Log Examiners security group. **Choose Select**.
7. On the **Members** step, choose **Review + Assign**.

Next step: Monitor Web Apps [Click here to navigate to this page on the GitHub repo if not using pages](https://github.com/microsoft/azure-monitor-lab/blob/main/instructions/04-exercise-monitor-web-apps/index.md)
