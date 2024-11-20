# Sentinel_homelab

To set up a Microsoft Sentinel Home Lab (FREE - SIEM), we will need to sign up a Microsoft email.

1) Go to https://azure.microsoft.com/en-us/pricing/details/microsoft-sentinel/

    - Click "Try Azure for free".

    - Just follow all the steps to finish setting up the account.

2) Once the Microsoft account is ready, we will be on the Microsoft Azure (portal) page.

3) Click on Virtual machines, and create an "Azure virtual machine with preset configuration"

    - At the resource group, create a new resource group, you can name it whatever you want.
    - Name the virtual machine name and choose a region where need to be the same or close to the region of the Sentinel workplace (we will configure this later).
    - Enter username and password for remote login.
    - At the image section, choose Window 10 Pro or Window 11 Pro.
    - Leave everything as default and click next until you reach "Review + Create".
  
4) Wait for a few minutes for the virtual machine to be deployed. While waiting, go to the search bar at the top and look for "Sentinel".

5) Create a workspace for the Sentinel service.
     - Choose the same resource group, name whatever you want and choose the same region where the newly created virtual machine is located at.
     - Click on "Review + Create".
  
6) Once the workspace is ready, go back to the Microsoft Sentinel page to add Microsoft Sentinel to the workspace.

7)  Click on the settings under "Configuration" section and click on "Workspace settings".

8)  Under Settings, click on the "Agents". We will see no computers connected.

9)  We need to add a computer to the workspace. Go back to Microsoft Sentinel and click on "Data connectors" that located under "Configuration" section.
    - Click on "More content at Content Hub"
    - Look for "Windows Security Events" and install it.

10) Once the connector is installed, click on the "Windows Security Events via AMA" and open the connector page.
    
11) Click on "+ Create data collection rule" and enter any name for the rule.
      - Resource group need to be the same and choose "All Security Events" at the Collect tab.
12) Now we need to add an alert policy to trigger an incident. Go to Configuration -> Analytics.
      - Create a "Scheduled query rule", we need to check if anyone has successfully login into the virtual machine.
      - In General, name the rule with any name and set MITRE ATT&CK to "Initial Access".
      - In Set Rule logic,
      Rule query: SecurityEvent
    | where Activity contains "success" and Account !contains "system" .
      - Query scheduling - run every 5 minutes.
      - Leave everything else as default and Review + create.

13) At this point, the virtual machine should be ready to be used. Go back to virtual machine page, select the newly created VM.
        - Click on "Connect" and use Native RDP.
        - Download RDP file and use the credentials that we entered at step 3.

14) Once we successfully login, Microsoft Sentinel will trigger an incident.
    
