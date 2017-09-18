### Amazon connect notes

[Amazon Connect and Salesforce Integration ](http://docs.aws.amazon.com/connect/latest/adminguide/salesforce-integration.html)

```
The Amazon Connect CTI Adapter provides a WebRTC browser-based Contact Control Panel (CCP) within Salesforce. This integration enables your agents to leverage both inbound caller ID screen pop and outbound click to call/transfer/conferencing.

We recommend that you initially install the package into your Salesforce sandbox. After the package is installed, you can configure your Salesforce Call Center configuration within Salesforce. This configuration is a XML file that you import into your call center. It provides all the details required to enable the CTI.

The next step is to whitelist your Salesforce Visualforce domain within your Amazon Connect Application integration. This allows cross-domain access to your Amazon Connect instance.

Prerequisites

Salesforce Classic, Salesforce Console, or Lightning Experience
An Amazon Connect instance
A Firefox or Chrome browser
To integrate with Salesforce

In your Salesforce sandbox, install the following managed package: Amazon Connect CTI Adapter.

Download the AmazonConnectCallCenterConfig.xml file and import it into your Salesforce call center configuration.

Edit the call center configuration as follows:

For CTI Adapter URL, type the one of the following, based on your Salesforce interface:
/apex/amazonconnect__ACSFCCP_Classic
/apex/amazonconnect__ACSFCCP_Console
/apex/amazonconnect__ACSFCCP_Lightning
For Salesforce Compatibility Mode, choose Classic for the Salesforce Classic and Salesforce Console or Lightning for Lightning Experience.
For Amazon Connect CCP URL, type the CCP URL for your instance (for example, https://instance.awsapps.com/connect/ccp).
For Phone Number Formatting, Country, specify the appropriate 2-digit ISO country code.
To provide users with access to the CCP, choose Manage Call Center Users.
Whitelist your Salesforce Visualforce domain URL using the directions in Application Integration. This URL usually has the following format:

https://amazonconnect.instance.visual.force.com
To verify the URL, open the Visualforce page in setup.

Log in to your Amazon Connect instance.

Launch Salesforce. You should see the integrated CCP in the side panel (Salesforce Classic) or the phone toolbar (Salesforce Classic and Lightning Experience).
```
