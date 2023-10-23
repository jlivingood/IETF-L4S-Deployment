# Week 3 - Low Latency DNS Benchmark

This testing is optional and requires a device running Windows.  The configuration required for the test is **recommended for advanced users.**

### Step 1 - Download DNS Benchmark 
1. Download the DNS Benchmark application at https://www.grc.com/files/DNSBench.exe.
1. Download the .ini file with the DNS servers pre-configured: <URL_HERE>.
1. Place the files in the same folder if not already.

### Step 2 - Run the DNS Benchmark Application without Low Latency
1. Double-click the DNSBench.exe file to launch the application.
2. Click the Nameservers tab.
3. Click the `Run Benchmark` button.
4. When the test is finished running, click the "Tablular Data" tab in the DNS Benchmark app.
5. For each the 4 nameservers we're testing to, please enter the **Uncached Name Avg** as shown in the below screenshot on the results form. 

   ![Screenshot of Benchmark Tabular Data tab](https://github.com/elocmcs/IETF-L4S-Deployment/blob/main/Screenshot_231019-1.jpg)

 
### Step 3 - Install Group Policy Editor for Windows 10/11 Home Edition
**If you have Windows 10/11 Pro installed, please skip to step 3**

Please **chose only one of the following methods** to install and enable Group Policy Editor into Windows Home Edition:
1. **Method 1**: Download and run a batch script to automate the installation
   * Download the batch script here: <URL_HERE>
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
   
3. In the search popup window, click "Run as administrator"
4. In the Local Group Policy Editor window on the left side, click the arrow to the left of **Computer Configuration** to expand the menu.
5. Expand the **Windows Settings** menu.
6. Right-click on **Policy-based QoS** and select "Create new policy..."
7. On the first screen, enter the following:
   * Policy name: **`Low Latency DNS`**
   * **Check** the box next to "Specify DSCP Value:" and enter **`45`** in the number field.
8. Click Next.
9. On the second screen, select **All applications**
10. Click Next.
11. On the third screen, choose the following options:
    * **Any source IP address**
    * **Any destination IP address**
12. Click Next.
13. On the final screen, make the following selections:
    * "Select the protocol this QoS policy Applies to": **TCP and UDP**
    * "Specify the source port number": **From any source port**
    * "Specify the destination port number": **`53`**
14. Click Finish.
15. Reboot your PC.
 
#### Step 5 - Run the DNS Benchmark Application with Low Latency
1. Double-click the DNSBench.exe file to launch the application.
1. Click the Nameservers tab.
1. Click the `Run Benchmark` button.
1. When the test is finished running, click the "Tablular Data" tab in the DNS Benchmark app.
1. For each the 4 nameservers we're testing to, please enter the **Uncached Name Avg** as shown in the below screenshot on the results form. 

![Screenshot of Benchmark Tabular Data tab](https://github.com/elocmcs/IETF-L4S-Deployment/blob/main/Screenshot_231019-1.jpg)



## Complete the Survey Form to Submit Results
https://app.smartsheet.com/b/form/8266ec3c2c0a47c485334a7dc7461b07

## Report Problems Here: 
https://app.smartsheet.com/b/form/c91c06bb97914742bdf54f25e294eb07
