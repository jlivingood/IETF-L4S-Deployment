# Week 2 - Field Trial Instructions

**DRAFT** - Need to enable QUIC/HTTP3 on the servers for these tests. 

This testing is OPTIONAL and requires a device running **MacOS 14 Sonoma**.
You might consider upgrading the OS with Setting -> General -> Software Update.

## Two Actions Requested

## Run the Apple Network Quality Test - USING SPECIAL SERVER FROM APPLE

1. Identify your Mac's connection type to router: Ethernet or Wi-Fi.
2. Open the Terminal application.
3. In Terminal, paste in this text: `networkQuality -russjc9-ve-vfe-006.aaplimg.com -s -f h3,noL4S` and hit enter.  NOTE RESULT IN THE SURVEY
4. Next, paste in this text: `networkQuality -russjc9-ve-vfe-006.aaplimg.com -s -f h3,L4S` and hit enter.  NOTE RESULT IN THE SURVEY

### Complete the Survey Form to Submit Results (for 1st test)
https://app.smartsheet.com/b/form/d3ca6000600044219862dfcb9324742e

## Run the Apple Network Quality Test - USING SPECIAL SERVER FROM COMCAST

1. In the Terminal application window you have open from the previous test, paste in this text: `networkQuality -C https://rpm-nqtest-st.comcast.net/.well-known/nq -s -f h3,noL4S` and hit enter. NOTE RESULT IN THE SURVEY
2. Next, paste in this text: `networkQuality -C https://rpm-nqtest-st.comcast.net/.well-known/nq -s -f h3,L4S` and hit enter. NOTE RESULT IN THE SURVEY

### Complete the Survey Form to Submit Results (for 2nd test)
https://app.smartsheet.com/b/form/1d676cf10eb142948515ceb3d15819cd

## Report Problems Here: 
https://app.smartsheet.com/b/form/c91c06bb97914742bdf54f25e294eb07
