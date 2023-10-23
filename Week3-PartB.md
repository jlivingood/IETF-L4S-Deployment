# Week 3 - Low Latency DNS Benchmark

This testing is optional and requires a device running Windows.  The configuration required for the test is **recommended for advanced users.**

### Step 1 - Download DNS Benchmark 
1. Download the DNS Benchmark application at https://www.grc.com/files/DNSBench.exe.
1. Download the .ini file with the DNS servers pre-configured: 
   *   Click The following link and then the "Download Raw file" button to save the .ini file in the proper format
       * https://github.com/jlivingood/IETF-L4S-Deployment/blob/main/DNSBench.ini
         
       ![Screenshot Download Raw](https://github.com/elocmcs/IETF-L4S-Deployment/blob/main/Screenshot-231023-5.jpg)
3. 1. Place the files in the same folder if not already.

### Step 2 - Run the DNS Benchmark Application without Low Latency
1. Double-click the DNSBench.exe file to launch the application.
2. Click the Nameservers tab.
3. Click the `Run Benchmark` button.
4. When the test is finished running, click the "Tablular Data" tab in the DNS Benchmark app.
5. For each the 4 nameservers we're testing to, please enter the **Uncached Name Avg** on the [results form](https://app.smartsheet.com/b/form/8266ec3c2c0a47c485334a7dc7461b07). 

   ![Screenshot of Benchmark Tabular Data tab](https://github.com/elocmcs/IETF-L4S-Deployment/blob/main/Screenshot_231019-1.jpg)
 
### Step 3 - Install Group Policy Editor for Windows 10/11 Home Edition
**If you have Windows 10/11 Pro installed, please skip to step 4**

Please **choose only one of the following methods** to install and enable Group Policy Editor into Windows Home Edition:
1. **Method 1**: Download and run a batch script to automate the installation
   * Download the and unzip the batch script here: <URL_HERE>
   * Right-Click on the downloaded script and select "Run as Administrator". You will get errors if you skip this step.
   * A window will popup and show the progress of downloading and installing the software. This will take several minutes.
   * Reboot your PC and continue to Step 3.
1. **Method 2**: Manual Installation
   * Click the Window Start Menu and type: `cmd`
   * In the search popup window, click `Run as administrator`.
   * In the Command Prompt window that opened, cut and paste the following line followed by Enter. It will take a few minutes to finish running:
   ```
   FOR %F IN ("%SystemRoot%\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientTools-Package~*.mum") DO (DISM /Online /NoRestart /Add-Package:"%F")
   ```
   * After the above command is done running, cut and paste the following line in followed by Enter:
   ```
   FOR %F IN ("%SystemRoot%\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientExtensions-Package~*.mum") DO (DISM /Online /NoRestart /Add-Package:"%F")
   ```
   * After the above command is done running (it will take a few minutes), reboot your PC.

### Step 4 - Configure DNS requests for low latency using Group Policy Editor
The following steps will configure Windows to mark DNS requests as low latency traffic.
1. Click the Windows Start Menu and type: `gpedit.msc`
   
   ![Screenshot of Policy Editor](https://github.com/elocmcs/IETF-L4S-Deployment/blob/main/Screenshot_231023-2.jpg)
   
3. In the search popup window, click "Run as administrator"
4. In the Local Group Policy Editor window on the left side, click the arrow to the left of **Computer Configuration** to expand the menu.
5. Expand the **Windows Settings** menu.
6. Right-click on **Policy-based QoS** and select "Create new policy..."

   ![Screenshot of Policy Editor new QoS](https://github.com/elocmcs/IETF-L4S-Deployment/blob/main/Screenshot-231023-3.jpg)
   
8. On the first screen, enter the following:
   * Policy name: **`Low Latency DNS`**
   * **Check** the box next to "Specify DSCP Value:" and enter **`45`** in the number field.
9. Click Next.
10. On the second screen, select **All applications**
11. Click Next.
12. On the third screen, choose the following options:
    * **Any source IP address**
    * **Any destination IP address**
13. Click Next.
14. On the final screen, make the following selections:
    * "Select the protocol this QoS policy Applies to": **TCP and UDP**
    * "Specify the source port number": **From any source port**
    * "Specify the destination port number": **`53`**
15. Click Finish.
16. Reboot your PC.
 
### Step 5 - Run the DNS Benchmark Application with Low Latency
1. Double-click the DNSBench.exe file to launch the application.
1. Click the Nameservers tab.
1. Click the `Run Benchmark` button.
1. When the test is finished running, click the "Tablular Data" tab in the DNS Benchmark app.
1. For each the 4 nameservers we're testing to, please enter the **Uncached Name Avg** on the [results form](https://app.smartsheet.com/b/form/8266ec3c2c0a47c485334a7dc7461b07).

### Step 6 - Removal of DNS Low Latency Policy (Optional)
Leaving the policy we created in step 4 on your computer will not affect your PC even if you no longer have Low Latency service, but if you wish to remove it, follow these steps:
1. Click the Windows Start Menu and type: `gpedit.msc`
2. In the search popup window, click "Run as administrator"
3. Click the arrows to the left of **Computer Configuration** > **Windows Settings** > **Policy-Based QoS** to expand the menus
4. Right-click on the **Low Latency DNS** policy created earlier and select **Delete policy**.
5. Reboot your PC.

   ![Screenshot of delete LLD DNS QoS](https://github.com/elocmcs/IETF-L4S-Deployment/blob/main/Screenshot_231023-4.jpg)

## Complete the Survey Form to Submit Results
https://app.smartsheet.com/b/form/8266ec3c2c0a47c485334a7dc7461b07

## Report Problems Here: 
https://app.smartsheet.com/b/form/c91c06bb97914742bdf54f25e294eb07
