# Week 5 - Field Trial Instructions

This testing is OPTIONAL and requires a device running MacOS.  

## Two Actions Requested

## Run the Apple Network Quality Test - USING ETHERNET & SPECIAL SERVER FROM APPLE

1. Open the Terminal application.
2. In Terminal, type (easiest is copy & paste) "defaults write -g network_enable_l4s -bool true". This sets the OS to use low latency networking.
3. In Terminal, paste in this text: *networkQuality -russjc9-ve-vfe-006.aaplimg.com -s -f L4S* and hit enter. NOTE RESULT IN THE SURVEY
   IF YOU GET THE ERROR "illegal option" then paste in this text: *networkQuality -russjc9-ve-vfe-006.aaplimg.com -s* and hit enter. 

### Complete the Survey Form to Submit Results (for 1st test)
https://app.smartsheet.com/b/form/1d676cf10eb142948515ceb3d15819cd

## Run the Apple Network Quality Test - USING ETHERNET & SPECIAL SERVER FROM COMCAST

1. In the Terminal application window you have open from the previous test, paste in this text: *networkQuality -C https://rpm-nqtest-st.comcast.net/.well-known/nq -s -f L4S* and hit enter. NOTE RESULT IN THE SURVEY
   IF YOU GET THE ERROR "illegal option" then paste in this text: *networkQuality -C https://rpm-nqtest-st.comcast.net/.well-known/nq -s* and hit enter. 

### Complete the Survey Form to Submit Results (a 2nd time, for 2nd test)
https://app.smartsheet.com/b/form/1d676cf10eb142948515ceb3d15819cd

## Report Problems Here: 
https://app.smartsheet.com/b/form/c91c06bb97914742bdf54f25e294eb07
