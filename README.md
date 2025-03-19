<p align="center">
  <img src="https://github.com/user-attachments/assets/04b84d63-8a32-46e4-9210-850756f64cfe" width="150" height="auto">
  <h1 align="center">Optimized Threat Hunting with Microsoft Sentinel</h1>
</p>

#### *In this tutorial, we will:*
*•	Set up Microsoft Sentinel by creating a Log Analytics workspace and configuring data retention.*

*•	Connect security data sources, including Microsoft Defender for Cloud and Windows Event Logs.*

*•	Automate threat detection using scheduled queries and ASIM parsers.*

*•	Visualize security data with Sentinel workbooks and perform threat hunting using MITRE ATT&CK mapping.*

#### Tasks:
 1. Initialize Log Analytics for Security Data Collection.
 2. Deploy Microsoft Sentinel to a Workspace.
 3. Set Retention Policies for Log Data in Sentinel.
 4. Connect Microsoft Defender for Cloud Data Connector.
 5. Monitor Azure Platform Activity in Sentinel.
 6. Collect Windows Event Logs for Threat Detection.
 7. Automate Threat Detection with Scheduled Queries.
 8. Standardize Security Data with ASIM Parsers.
 9. Visualize Threat Data with Sentinel Workbooks.
 10. Create a Hunt with MITRE ATT&CK Mapping.

## Task 1: Initialize Log Analytics for Security Data Collection.

In this task, we will create a Log Analytics workspace in Azure to store and process security logs. This workspace serves as the foundation for Microsoft Sentinel's data ingestion and threat detection capabilities.

1.  In the Azure portal search bar, type 'Microsoft Sentinel' and select it.
2.  Click '+ Create'.
3.  Choose 'Create a new workspace'.

<p align="center">
<img src="https://github.com/user-attachments/assets/a6ce3ed6-9b54-45f5-bec4-861cdd6f4bee">
</p>

4.  Select 'Create new' for the Resource group and enter 'Security-RG'.
5.  For the Name, enter 'Sec-Workspace'.
6.  Choose a region.

<p align="center">
<img src="https://github.com/user-attachments/assets/94b10a00-cf6e-4855-9910-904e92563d3d">
</p>

7.  Click 'Review + create' and then 'Create' to deploy the workspace.

## Task 2: Deploy Microsoft Sentinel to a Workspace.

In this task, we will enable Microsoft Sentinel in our Log Analytics workspace. This step activates Sentinel's security monitoring and analytics features, allowing us to collect and analyze security events.

1.  In the Azure portal search bar, type 'Sentinel' and select 'Microsoft Sentinel'.
2.  Click '+ Create'.

<p align="center">
<img src="https://github.com/user-attachments/assets/95286d36-c567-4d47-818e-bf886a3319fe">
</p>

3.  Select the 'Log Analytics workspace' created earlier and click 'Add'.

## Task 3: Set Retention Policies for Log Data in Sentinel.

In this task, we will adjust the data retention settings for our Log Analytics workspace. This ensures that logs are stored for an appropriate duration to support long-term threat analysis and compliance requirements.

1.  In the Azure portal, navigate to 'Log Analytics workspaces'.
2.  Select the 'Sec-Workspace'.
3.  Under 'Settings', select 'Usage and estimated costs'.

<p align="center">
<img src="https://github.com/user-attachments/assets/69ca3088-28e1-46da-8b98-304e155a5040">
</p>

4.  Click 'Data retention'.
5.  Change the retention period to '180 days' and confirm by clicking 'OK'.

<p align="center">
<img src="https://github.com/user-attachments/assets/28275eca-646a-471c-b063-70cf46b23fd0">
</p>

## Task 4: Connect Microsoft Defender for Cloud Data Connector.

In this task, we will connect Microsoft Defender for Cloud to Sentinel. This allows security alerts, threat intelligence, and compliance data from Defender for Cloud to be ingested into Sentinel for further analysis.

1.  In the Microsoft Sentinel portal, navigate to 'Content Hub'.
2.  Search for 'Microsoft Defender for Cloud' and click 'Install'.

<p align="center">
<img src="https://github.com/user-attachments/assets/a459e6bd-29bc-495a-9ed9-7d9019e031dc">
</p>

3.  In the solution details page, select 'Manage'.
4.  Choose 'Subscription-based Microsoft Defender for Cloud (Legacy) Data connector'.

<p align="center">
<img src="https://github.com/user-attachments/assets/6d898fa4-4973-48c0-866e-29aea9a7a683">
</p>

5.  Under 'Configuration', enable 'Connected' and 'Bi-directional sync'.

<p align="center">
<img src="https://github.com/user-attachments/assets/733ebfa8-51c9-4ec8-aee6-1f9f20a39ebc">
</p>

## Task 5: Monitor Azure Platform Activity in Sentinel.

In this task, we will integrate Azure Activity logs with Sentinel. These logs help monitor administrative actions and changes in Azure resources, which can be crucial for identifying unauthorized access or policy violations.

1.  In the Microsoft Sentinel portal, go to 'Content Hub'.
2.  Search for 'Azure Activity' and click 'Install'.
3.  In the solution details page, select 'Manage'.

<p align="center">
<img src="https://github.com/user-attachments/assets/6bae2fa2-efda-4496-925c-6ad9d502c7e2">
</p>

4.  Open the 'Azure Activity Data connector' and go to 'Configuration'.
5.  Click 'Launch Azure Policy Assignment Wizard'.

<p align="center">
<img src="https://github.com/user-attachments/assets/d2e9e8fe-7f44-4289-851c-eaf443196ed0">
</p>

6.  Under 'Scope', select your Azure subscription.
7.  Under 'Parameters', choose 'Sec-Workspace'.
8.  Enable 'Create a remediation task' and click 'Review + Create', then 'Create'.

<p align="center">
<img src="https://github.com/user-attachments/assets/1386133b-a8c1-4e81-8de9-a3a6ad0da0c3">
</p>

<p align="center">
<img src="https://github.com/user-attachments/assets/0664f003-b578-4563-872c-c7dcb165a6c8">
</p>

## Task 6: Collect Windows Event Logs for Threat Detection.

In this task, we will configure Sentinel to ingest Windows Security Events using the AMA data connector. This will allow us to track user logins, policy changes, and security-related events across Windows systems. A Virtual Machine called VM1 is pre deployed to have a source of data.

1.  In Microsoft Sentinel, select 'Content Hub'.
2.  Search for 'Windows Security Events' and click 'Install'.
3.  In the solution details page, select 'Manage'.

<p align="center">
<img src="https://github.com/user-attachments/assets/96ee59ac-f9d9-4b06-b4b1-cc1f90d089da">
</p>

4.  Select 'Windows Security Events via AMA' Data connector.

<p align="center">
<img src="https://github.com/user-attachments/assets/250fc6fe-faea-4c4d-b622-8e57ab4b6483">
</p>

5.  Click 'Open connector page'.
6.  Under 'Configuration', create a new 'Data Collection Rule' named 'testdcr'.

<p align="center">
<img src="https://github.com/user-attachments/assets/fb39e944-bfaf-4ed2-80ef-7b3c932be955">
</p>

7.  Select 'Azure subscription > Security-RG > VM1 (test VM)'.

<p align="center">
<img src="https://github.com/user-attachments/assets/cd0e7caf-cbb3-411b-8ab7-d016a3181074">
</p>

8.  Keep 'All Security Events' selected.

<p align="center">
<img src="https://github.com/user-attachments/assets/ca4f2eee-24fc-4946-8723-8ad49118f04c">
</p>

9.  Click 'Next: Review + Create', then 'Create'.

<p align="center">
<img src="https://github.com/user-attachments/assets/05b3e09f-3db9-4b35-aed5-635436e36329">
</p>

## Task 7: Automate Threat Detection with Scheduled Queries.

In this task, we will create a scheduled query using Kusto Query Language (KQL) to detect specific threat patterns. This helps automate the identification of suspicious activities and triggers alerts when anomalies are detected.

1.  In Microsoft Sentinel, select 'Analytics'.
2.  Go to 'Rule templates' and search for 'New CloudShell User'.
3.  Click 'Create rule'.

<p align="center">
<img src="https://github.com/user-attachments/assets/176a5b99-4a56-4da3-9928-758515489396">
</p>

4.  Under 'Severity', set it to 'Medium'.

<p align="center">
<img src="https://github.com/user-attachments/assets/4187824e-ef2c-40e3-b726-80be55f52d78">
</p>

5.  Configure query scheduling: 'Run Query every: 5 minutes', 'Lookup data from the last: 1 day'.

<p align="center">
<img src="https://github.com/user-attachments/assets/96e483f3-dc49-4156-ad7c-c9f49fb22d9d">
</p>

6.  Click 'Next: Incident settings', then 'Next: Automated response', then 'Review + Create' and 'Save'.

<p align="center">
<img src="https://github.com/user-attachments/assets/09a89529-6a5e-4f71-9dee-e9238d994668">
</p>

## Task 8: Standardize Security Data with ASIM Parsers.

In this task, we will deploy ASIM (Advanced Security Information Model) parsers to normalize log data. This helps ensure consistency across different log sources, making it easier to query and analyze security events.

1.  In Microsoft Sentinel, go to 'Logs'.
2.  Open 'Schema and Filter' and navigate to 'Functions'.
3.  Search for 'Registry Event ASIM parser'.
4.  Click 'Load the function code'.

<p align="center">
<img src="https://github.com/user-attachments/assets/115f2762-54a5-46c8-9660-6abbb90ec170">
</p>

5.  Run a test query using the parser to confirm proper log normalization.

<p align="center">
<img src="https://github.com/user-attachments/assets/242c3a11-86ab-48ba-a2e0-2adca32d46cc">
</p>

## Task 9: Visualize Threat Data with Sentinel Workbooks.

In this task, we will create and customize workbooks in Microsoft Sentinel. These workbooks provide visual representations of security data, helping security teams monitor and analyze threats effectively.

1.  In Microsoft Sentinel, navigate to 'Workbooks'.
2.  Select the 'Templates' tab and search for 'Azure Activity'.

<p align="center">
<img src="https://github.com/user-attachments/assets/4ed6f77d-b665-46d3-ab81-b928708e718b">
</p>

3.  Click 'View template' and customize the visualization.
4.  Save it for ongoing monitoring.

<p align="center">
<img src="https://github.com/user-attachments/assets/c09e8c6d-8dac-455a-9412-6de37c82b813">
</p>

## Task 10: Create a Hunt with MITRE ATT&CK Mapping.

1.  Navigate to MITRE ATT&CK (Preview) under Threat Management.
2.  Filter by Hunting queries.

<p align="center">
<img src="https://github.com/user-attachments/assets/13909bc3-7f01-46be-a006-df82a88067b2">
</p>

3.  Select Account Manipulation and view related hunting queries.

<p align="center">
<img src="https://github.com/user-attachments/assets/9a5647d0-ac3a-44d7-993e-e5131805e374">
</p>

4.  Create a new hunt, provide details, and execute selected queries.

<p align="center">
<img src="https://github.com/user-attachments/assets/a721b3e7-fe46-4444-8f81-c159c2edac9b">
</p>

5.  Analyze results and escalate findings if necessary.
