# Week 5 - Field Trial Instructions

This testing is OPTIONAL and requires a device running Windows.  

## Action Requested

### Download DNS Benchmark 
Get the application at https://www.grc.com/files/DNSBench.exe. 

### Configure DNS Benchmark
Open the DNS Benchmark application and click **ADD** and enter the IP address **96.113.158.206** - which is a beta testing DNS server 
on our network. Also please add 75.75.75.75, which is our standard DNS server. **All other DNS server IP addresses 
should be deleted.** Finally, please add two off-network public servers: 8.8.8.8 and 9.9.9.9.  
 
### Configure Windows
Next, we want you to configure Windows to mark outbound DNS traffic with the DSCP-45 marking.  
 
#### Step 1 - Access the “Local Group Policy” Editor
To do this, click the Start Menu and type: “Local Group Policy”.  In the window that appears, navigate to, “Local Computer Policy” > “Computer Configuration” > “Windows Settings” Right Click on the “Policy-based QoS” and select “Create new Policy”. 
 
#### Step 2 – Configure the Policy
- Name the policy “**DNS Low Latency**”
- Enter “**45**” into the “**Specify DSCP Value Field**”.
- Select “**All Applications**” and select next to continue.
- Select **Any** source and **Any** destination IP address, then select next to continue. 
- Select **UDP** from the “Select the protocol this QoS policy applies to” drop box.
- Select “From this source port” and enter **53**.
- Next, select “To this destination port” and enter **53**.
- Then select “Finish” 

#### Step 3 - Run the DNS Benchmark Application 
Back in the DNS Benchmark client - **click “Run Benchmark”**. Take note of the results.

## Complete the Survey Form to Submit Results
Link TBD

## Report Problems Here: 
https://app.smartsheet.com/b/form/c91c06bb97914742bdf54f25e294eb07
