# Week 2 - Field Trial Instructions

This test only applies if you use MacOS.

This testing requires a device running the recently released **MacOS 14 Sonoma**.
If you haven’t upgraded to MacOS 14, SKIP THIS TEST.

## Two Actions Requested

## 1. Run the Apple Network Quality Test - USING SPECIAL SERVER FROM APPLE

### Step 1

Open the Terminal application and cut and paste in this text:

    networkQuality -russjc9-ve-vfe-006.aaplimg.com -s -f h3,noL4S
    
Hit enter.

Enter numerical value for "Uplink Responsiveness"  
Example - if you got the result below, enter 2156  
Uplink Responsiveness: High (27.829 milliseconds | **2156** RPM)

### Step 2

Cut and paste the following text into your Terminal application:

    networkQuality -russjc9-ve-vfe-006.aaplimg.com -s -f h3,L4S
    
Hit enter.

Enter numerical value for "Uplink Responsiveness"  
Example - if you got the result below, enter 2156  
Uplink Responsiveness: High (27.829 milliseconds | **2156** RPM)

### Complete the Survey Form to Submit Results (for 1st test)
https://app.smartsheet.com/b/form/d3ca6000600044219862dfcb9324742e

## 2. Run the Apple Network Quality Test - USING SPECIAL SERVER FROM COMCAST

### Step 1: Responsiveness Before Turning on Low Latency

Open the Terminal application and cut and paste in this text:

    networkQuality -C https://rpm-nqtest-st.comcast.net/.well-known/nq -k -s -f h3,noL4S

Hit enter.

Enter numerical value for "Uplink Responsiveness"   
Example - if you got the result below, enter 2156  
Uplink Responsiveness: High (27.829 milliseconds | **2156** RPM)

### Step 2: Responsiveness After Turning on Low Latency

Cut and paste the following text into your Terminal application:

    networkQuality -C https://rpm-nqtest-st.comcast.net/.well-known/nq -k -s -f h3,L4S

Hit enter.

Enter numerical value for "Uplink Responsiveness"
Example - if you got the result below, enter 2156
Uplink Responsiveness: High (27.829 milliseconds | **2156** RPM)

### Complete the Survey Form to Submit Results (for 2nd test)
https://app.smartsheet.com/b/form/1d676cf10eb142948515ceb3d15819cd

## Report Problems Here: 
https://app.smartsheet.com/b/form/c91c06bb97914742bdf54f25e294eb07
