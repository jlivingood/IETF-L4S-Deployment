# Week 3 - Field Trial Instructions

This testing is OPTIONAL and requires a device running Windows.  This test is for advanced users.

## Action Requested

### Step 1 - Download DNS Benchmark 
1. Get the application at https://www.grc.com/files/DNSBench.exe.
1. Download the .ini file with the DNS servers pre-configured: <URL_HERE>.
1. Place the files in the same folder.
 
### Step 2 - Install Group Policy Editor for Windows 10/11 Home Edition
**If you have Windows 10/11 Pro installed, please skip to step 3**

Please follow **one** of the two following steps to install and enable Group Policy Editor into your Windows Home Edition:
1. **Method 1**: Download and run a batch script to automate the installation
   * Download the batch script here: <URL_HERE>
   * Right-Click on the downloaded file and select "Run as Administrator." You will get errors if you skip this step.
   * A window will popup and show the progress of downloading and installing the software. 

### Step 3 - 

To do this, click the Start Menu and type: “Local Group Policy”.  In the window that appears, navigate to, “Local Computer Policy” > “Computer Configuration” > “Windows Settings” Right Click on the “Policy-based QoS” and select “Create new Policy”. 
 
#### Step 4 - Run the DNS Benchmark Application (Without Low Latency)
Back in the DNS Benchmark client - **click “Run Benchmark”**. Take note of the results in this [survey form](https://app.smartsheet.com/b/form/8266ec3c2c0a47c485334a7dc7461b07).

#### Step 2 - Install Group Policy Editor into Windows 10/11 Home Edition

 
#### Step 3 – Configure the Low Latency DNS Policy
- Name the policy “**DNS Low Latency**”
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
