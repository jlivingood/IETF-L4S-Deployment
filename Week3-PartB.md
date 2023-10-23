# Week 3 - Low Latency DNS Benchmark

This testing is optional and requires a device running Windows.  The configuration required for the test is **recommended for advanced users.**

### Step 1 - Download DNS Benchmark 
1. Get the application at https://www.grc.com/files/DNSBench.exe.
1. Download the .ini file with the DNS servers pre-configured: <URL_HERE>.
1. Place the files in the same folder.

### Step 2 - Run the DNS Benchmark Application without Low Latency
1. Double-click the DNSBench.exe file to launch the application.
2. Click the Nameservers tab.
3. Click the "Run Benchmark" button.
4. When the test is finished running, click the "Tablular Data" tab in the DNS Benchmark app.
5. For the four nameservers we're testing to, please enter **Uncached Name Avg** result on the results form.

![Screenshot of Benchmark Tabular Data tab](https://github.com/elocmcs/IETF-L4S-Deployment/blob/main)/Screenshot_231019-1.jpg)

 
### Step 3 - Install Group Policy Editor for Windows 10/11 Home Edition
**If you have Windows 10/11 Pro installed, please skip to step 3**

Please **chose only one of the following methods** to install and enable Group Policy Editor into Windows Home Edition:
1. **Method 1**: Download and run a batch script to automate the installation
   * Download the batch script here: <URL_HERE>
   * Right-Click on the downloaded file and select "Run as Administrator." You will get errors if you skip this step.
   * A window will popup and show the progress of downloading and installing the software. This will take several minutes.
   * Reboot your PC and continue to Step 3.
1. **Method 2**: Manual Installation
   * Click the Window Start Menu and type: cmd
   * In the search popup window, click "Run as administrator".
   * In the Command Prompt window that opened, cut and paste the following line followed by Enter. It may take a few minutes to finish running:
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
1. Click the Windows Start Menu and type: gpedit.msc
2. In the search popup window, click "Run as administrator"
3. In the Local Group Policy Editor window on the left side, click the arrow to the left of **Computer Configuration** to expand the menu.
4. Expand the **Windows Settings** menu.
5. Right-click on **Policy-based QoS** and select "Create new policy..."
6. On the first screen, enter the following:
   * Policy name: **Low Latency DNS**
   * **Check** the box next to "Specify DSCP Value:" and enter **45** in the number field.
7. Click Next.
8. On the second screen, select **All applications**
9. Click Next.
10. On the third screen, choose the following options:
    * **Any source IP address**
    * **Any destination IP address**
11. Click Next.
12. On the final screen, make the following selections:
    * "Select the protocol this QoS policy Applies to": **TCP and UDP**
    * "Specify the source port number": **From any source port**
    * "Specify the destination port number": **53**
13. Click Finish.
14. Reboot your PC.
 
#### Step 4 - Run the DNS Benchmark Application (Without Low Latency)
Back in the DNS Benchmark client - **click “Run Benchmark”**. Take note of the results in this [survey form](https://app.smartsheet.com/b/form/8266ec3c2c0a47c485334a7dc7461b07).

#### Step 2 - Install Group Policy Editor into Windows 10/11 Home Edition

 
#### Step 3 – Configure the Low Latency DNS Policy
- On  the Name the policy “**DNS Low Latency**”
- Enter “**45**” into the “**Specify DSCP Value Field**”.
- Select “**All Applications**” and select next to continue.
- Select **Any** source and **Any** destination IP address, then select next to continue. 
- Select **UDP** from the “Select the protocol this QoS policy applies to” drop box.
- Select “From this source port” and enter **53**.
- Next, select “To this destination port” and enter **53**.
- Then select “Finish” 

#### Step 4 - Run the DNS Benchmark Application (With Low Latency)
Back in the DNS Benchmark client - **click “Run Benchmark”**. Take note of the results in the [survey form](https://app.smartsheet.com/b/form/8266ec3c2c0a47c485334a7dc7461b07) and then submit it.

## Complete the Survey Form to Submit Results
https://app.smartsheet.com/b/form/8266ec3c2c0a47c485334a7dc7461b07

## Report Problems Here: 
https://app.smartsheet.com/b/form/c91c06bb97914742bdf54f25e294eb07
