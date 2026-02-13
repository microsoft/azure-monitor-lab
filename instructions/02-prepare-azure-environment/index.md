You must first complete the following exercise to prepare your Azure environment before you begin the lab exercises.

**Exercise: Prepare your Azure Environment**

**Tasks**:
- Create a Log Analytics workspace.
- Configure Log Analytics data retention and archive policies.
- Enable access to a Log Analytics workspace.

> [!NOTE]
> To complete this lab you need an [Azure subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_devrel).

## Prepare your bring-your-own-subscription (BYOS)

This exercise should take approximately **30** minutes to complete.

### Prepare your bring-your-own-subscription (BYOS)

This set of lab exercises assumes that you have global administrator permissions to an Azure subscription.

1. In the Azure Portal Search Bar, enter **Resource Groups** and select **Resource groups** from the list of results.
2. On the **Resource Groups** page, select **Create**.
3. On the **Create a Resource Group** page, select your subscription and enter the name rg-alpha. Set the region to East US, choose **Review + Create**, and then choose **Create**.

> **Note:** This set of exercises assumes that you choose to deploy in the East US Region, but you can change this to another region if you choose. Just remember that each time you see East US mentioned in these instructions you will need to substitute the region you have chosen.

## Create App Log Examiners security group

In this exercise, you create an Entra ID security group.

1. In the Azure Portal Search Bar, enter Azure Active Directory (or Entra ID) from the list of results.
2. On the **Default Directory** page, select **Groups**.
3. On the **Groups** page, choose **New Group**.
4. On the **New Group** page, provide the values in the following table and choose **Create**.

   | Property | Value |
   | --- | --- |
   | Group type | Security |
   | Group name | App Log Examiners |
   | Group description | App Log Examiners |

## Deploy and configure WS-VM1

In this exercise, you deploy and configure a Windows Server virtual machine.

1. In the Azure Portal Search Bar, enter **Virtual Machines** and select **Virtual Machines** from the list of results.
2. On the **Virtual Machines** page, choose **Create** and select **Azure Virtual Machine**.
3. On the **Basics** page of the Create A Virtual Machine wizard, select the following settings and then choose **Review + Create**.

   | Property | Value |
   | --- | --- |
   | Subscription | Your subscription |
   | Resource Group | rg-alpha |
   | Virtual machine name | WS-VM1 |
   | Region | East US |
   | Availability options | No infrastructure redundancy required |
   | Security type | Standard |
   | Image | Windows Server 2022 Datacenter: Azure Edition – x64 Gen2 |
   | VM architecture | x64 |
   | Size | Standard_D4s_v3 – 4 vcpus, 16 GiB memory |
   | Administrator account | prime |
   | Password | [Select a unique secure password] P@ssw0rdP@ssw0rd |
   | Inbound ports | RDP 3389 |

4. Review the settings and select **Create**.
5. Wait for the deployment to complete. Once deployment completes choose **Go to resource**.
6. On the **WS-VM1 properties** page, choose **Networking**.
7. On the **Networking** page, select the RDP rule.
8. On the RDP rule space, change the Source to My IP address and choose **Save**.

   This restricts incoming RDP connections to the IP address you're currently using.

9. On the **Networking** page, choose **Add inbound port rule**.
10. On the **Add inbound security rule** page, configure the following settings and choose **Add**.

    | Property | Value |
    | --- | --- |
    | Source | Any |
    | Source port ranges | * |
    | Destination | Any |
    | Service | HTTP |
    | Action | Allow |
    | Priority | 310 |
    | Name | AllowAnyHTTPInbound |

11. On the **WS-VM1** page, choose **Connect**.
12. Under Native RDP, choose **Select**.
13. On the **Native RDP** page, choose **Download RDP file** and then open the file. Opening the RDP file opens the Remote Desktop Connection dialog box.
14. On the **Windows Security** dialog box, choose **More Choices** and then choose Use a different account.
15. Enter the username as .\prime and the password as the secure password you chose in Step 3, and choose **OK**.
16. When signed into the Windows Server virtual machine, right-click on the **Start** hint and then choose **Windows PowerShell (Admin)**.
17. At the elevated command prompt, type the following command and press **Enter**.

    ```powershell
    Install-WindowsFeature Web-Server -IncludeAllSubFeature -IncludeManagementTools
    ```

18. When the installation completes run the following command to change to the web server root directory.

    ```powershell
    cd c:\inetpub\wwwroot\
    ```

19. Run the following command.

    ```powershell
    Wget https://raw.githubusercontent.com/Azure-Samples/html-docs-hello-world/master/index.html -OutFile index.html
    ```

## Deploy and configure LX-VM2

In this exercise you deploy and configure a Linux virtual machine.

1. In the Azure Portal Search Bar, enter **Virtual Machines** and select **Virtual Machines** from the list of results.
2. On the **Virtual Machines** page, choose **Create** and select **Azure Virtual Machine**.
3. On the **Basics** page of the Create A Virtual Machine wizard, select the following settings and then choose **Review + Create**.

   | Property | Value |
   | --- | --- |
   | Subscription | Your subscription |
   | Resource Group | rg-alpha |
   | Virtual machine name | Linux-VM2 |
   | Region | East US |
   | Availability options | No infrastructure redundancy required |
   | Security type | Standard |
   | Image | Ubuntu Server 20.04 LTS – x64 Gen2 |
   | VM architecture | x64 |
   | Size | Standard_D2s_v3 – 2 vcpus, 8 GiB memory |
   | Authentication type | Password |
   | Username | Prime |
   | Password | [Select a unique secure password] P@ssw0rdP@ssw0rd |
   | Public inbound ports | None |

4. Review the information and choose **Create**.
5. After the VM deploys, open the **VM properties** page and choose **Extensions + Applications** under **Settings**.
6. Choose **Add** and select the **Network Watcher Agent for Linux**. Choose **Next** and then choose **Review and Create**. Choose **Create**.

> **Note:** The installation and configuration of the OmsAgentForLinux extension will be performed in Exercise 2 after the Log Analytics workspace is created.

## Deploy a web app with an SQL Database

1. Ensure that you're signed into the Azure Portal.
2. In your browser, open a new browser tab and navigate to https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.web/web-app-sql-database
3. On the GitHub page, choose **Deploy to Azure**.
4. A new tab opens. If necessary, re-sign into Azure with the account that has Global Administrator privileges.
5. On the **Basics** page, select **Edit template**.
6. In the template editor, delete the contents of lines 158 to 174 inclusive and delete the "," on line 157. Choose **Save**.
7. On the **Basics** page, provide the following information and choose **Next**.

   | Property | Value |
   | --- | --- |
   | Subscription | Your subscription |
   | Resource Group | rg-alpha |
   | Region | East US |
   | Sku Name | F1 |
   | Sku Capacity | 1 |
   | Sql Administrator Login | prime |
   | Sql Administrator Login Password | [Select a unique secure password] P@ssw0rdP@ssw0rd |

8. Review the information presented and select **Create**.
9. After the deployment completes, choose **Go to resource group**.

## Deploy a Linux web app

1. Ensure that you're signed into the Azure Portal.
2. In your browser, open a new browser tab and navigate to https://learn.microsoft.com/en-us/samples/azure/azure-quickstart-templates/webapp-basic-linux/
3. On the GitHub page, choose **Deploy to Azure**.
4. On the **Basics** page, provide the following information and choose **Next**.

   | Property | Value |
   | --- | --- |
   | Subscription | Your subscription |
   | Resource Group | rg-alpha |
   | Region | East US |
   | Web app Name | AzureLinuxAppWXYZ (assign a random number to the final four characters of the name) |
   | Sku | S1 |
   | Linux Fx version | php\|7.4 |

5. Review the information and choose **Create**.

Next step: [Deploy Log Analytics](https://microsoft.github.io/azure-monitor-lab/instructions/03-exercise-deploy-log-analytics/)

[Click here to navigate to this page on the GitHub repo if not using pages](https://github.com/microsoft/azure-monitor-lab/blob/main/instructions/03-exercise-deploy-log-analytics/index.md)
