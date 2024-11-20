# **Settings for Microsoft Teams to take advantage of LL marking:**

## QoS for Audio
new-NetQosPolicy -Name "Teams Audio" -AppPathNameMatchCondition "ms-teams.exe" -IPProtocolMatchCondition Both -IPSrcPortStartMatchCondition 50000 -IPSrcPortEndMatchCondition 50019 -DSCPAction 45 -NetworkProfile All
new-NetQosPolicy -Name "Classic Teams Audio" -AppPathNameMatchCondition "Teams.exe" -IPProtocolMatchCondition Both -IPSrcPortStartMatchCondition 50000 -IPSrcPortEndMatchCondition 50019 -DSCPAction 45 -NetworkProfile All

## QoS for Video
new-NetQosPolicy -Name "Teams Video" -AppPathNameMatchCondition "ms-teams.exe" -IPProtocolMatchCondition Both -IPSrcPortStartMatchCondition 50020 -IPSrcPortEndMatchCondition 50039 -DSCPAction 45 -NetworkProfile All
new-NetQosPolicy -Name "Classic Teams Video" -AppPathNameMatchCondition "Teams.exe" -IPProtocolMatchCondition Both -IPSrcPortStartMatchCondition 50020 -IPSrcPortEndMatchCondition 50039 -DSCPAction 45 -NetworkProfile All

## QoS for Sharing
new-NetQosPolicy -Name "Teams Sharing" -AppPathNameMatchCondition "ms-teams.exe" -IPProtocolMatchCondition Both -IPSrcPortStartMatchCondition 50040 -IPSrcPortEndMatchCondition 50059 -DSCPAction 18 -NetworkProfile All
new-NetQosPolicy -Name "Classic Teams Sharing" -AppPathNameMatchCondition "Teams.exe" -IPProtocolMatchCondition Both -IPSrcPortStartMatchCondition 50040 -IPSrcPortEndMatchCondition 50059 -DSCPAction 18 -NetworkProfile All

## QoS for Signaling
new-NetQosPolicy -Name "Teams Calling-Meeting Signaling" -AppPathNameMatchCondition "ms-teams.exe" -IPProtocolMatchCondition UDP -IPSrcPortStartMatchCondition 50070 -IPSrcPortEndMatchCondition 50089 -DSCPAction 45 -NetworkProfile All
new-NetQosPolicy -Name "Classic Teams Calling-Meeting Signaling" -AppPathNameMatchCondition "Teams.exe" -IPProtocolMatchCondition UDP -IPSrcPortStartMatchCondition 50070 -IPSrcPortEndMatchCondition 50089 -DSCPAction 45 -NetworkProfile All

# References:

https://learn.microsoft.com/en-us/microsoftteams/meetings-real-time-media-traffic

https://learn.microsoft.com/en-us/microsoftteams/qos-in-teams

https://learn.microsoft.com/en-us/microsoftteams/cqd-what-is-call-quality-dashboard

https://learn.microsoft.com/en-us/microsoftteams/qos-in-teams-clients
