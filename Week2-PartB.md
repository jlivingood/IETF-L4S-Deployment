# Week 2 - Field Trial Instructions

This test only applies if you use MacOS.

This testing requires a device running the recently released **MacOS 14 Sonoma**.
If you haven’t upgraded to MacOS 14, SKIP THIS TEST.

## Run the Network Quality Test

### Step 1: Download Responsiveness with Low Latency OFF

Open the Terminal application and copy and paste in this text:

    networkQuality -C https://rpm-nqtest-st.comcast.net/.well-known/nq -k -s -f h2,noL4S

Hit enter.

Enter the RPM value for "Downlink Responsiveness" in the survey form.
Example - if you got the result below, enter `2156`.

> Downlink Responsiveness: High (27.829 milliseconds | `2156` RPM)

### Step 2: Download Responsiveness with Low Latency ON

Copy and paste the following text into your Terminal application:

    networkQuality -C https://rpm-nqtest-st.comcast.net/.well-known/nq -k -s -f h2,L4S

Hit enter.

Enter the RPM value for "Downlink Responsiveness" in the survey form.

### Step 3: Upload Responsiveness with Low Latency OFF

Copy and paste the following text into your Terminal application.  Note `h3` here for upload vs `h2` for download.

    networkQuality -C https://rpm-nqtest-st.comcast.net/.well-known/nq -k -s -f h3,noL4S

Hit enter.

Enter the RPM value for "Uplink Responsiveness" in the survey form.

### Step 4: Upload Responsiveness with Low Latency ON

Cut and paste the following text into your Terminal application:

    networkQuality -C https://rpm-nqtest-st.comcast.net/.well-known/nq -k -s -f h3,L4S

Hit enter.

Enter the RPM value for "Uplink Responsiveness" in the survey form.

### Complete the Survey Form to Submit Results
https://app.smartsheet.com/b/form/1d676cf10eb142948515ceb3d15819cd

## Report Problems Here:
https://app.smartsheet.com/b/form/c91c06bb97914742bdf54f25e294eb07
