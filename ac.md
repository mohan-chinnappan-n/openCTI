### Amazon connect notes

#### References:

1. [Amazon Connect and Salesforce Integration ](http://docs.aws.amazon.com/connect/latest/adminguide/salesforce-integration.html)

2. [Enabling Amazon Connect with Salesforce Service Cloud and Sales Cloud](https://aws.amazon.com/blogs/apn/enabling-amazon-connect-with-salesforce-service-and-sales-cloud/)


The Amazon Connect CTI Adapter provides a WebRTC browser-based Contact Control Panel (CCP) within Salesforce. This integration enables your agents to leverage both inbound caller ID screen pop and outbound click to call/transfer/conferencing.

We recommend that you initially install the package into your Salesforce sandbox. After the package is installed, you can configure your Salesforce Call Center configuration within Salesforce. This configuration is a XML file that you import into your call center. It provides all the details required to enable the CTI.

The next step is to whitelist your Salesforce Visualforce domain within your Amazon Connect Application integration. This allows cross-domain access to your Amazon Connect instance.

#### Prerequisites

1. Salesforce Classic, Salesforce Console, or Lightning Experience
2. An Amazon Connect instance
3. Firefox or Chrome browser
4. To integrate with Salesforce

In your Salesforce sandbox, install the following managed package: 
[Amazon Connect CTI Adapter](https://appexchange.salesforce.com/listingDetail?listingId=a0N3A00000EJH4yUAH)

Download the AmazonConnectCallCenterConfig.xml file and import it into your Salesforce call center configuration.

```xml
<!-- Please import this file into your call center config.  -->

<callCenter>
    <section sortOrder="0" name="reqGeneralInfo" label="Amazon Connect Salesforce CCP Adapter">
        <item sortOrder="0" name="reqInternalName"
              label="Internal Name">ACSFCCPAdapter</item>
        <item sortOrder="1" name="reqDisplayName"
              label="Display Name">Amazon Connect CCP Adapter</item>
        <item sortOrder="2" name="reqDescription"
              label="Description">Amazon Connect Call Center</item>
        <item sortOrder="3" name="reqAdapterUrl"
              label="CTI Adapter URL">/apex/amazonconnect__ACSFCCP_Classic</item>
        <item sortOrder="4" name="reqUseApi"
              label="Use CTI API">true</item>
        <item sortOrder="5" name="reqSoftphoneHeight"
              label="Softphone Height">400</item>
        <item sortOrder="6" name="reqSoftphoneWidth"
              label="Softphone Width">250</item>
        <item sortOrder="7" name="reqSalesforceCompatibilityMode"
              label=" Salesforce Compatibility Mode">Lightning</item>
    </section>
    <section sortOrder="1" name="reqConnectSFCCPOptions" label="Amazon Connect Information">

   <!-- change the CCP URL from Amazon here -->
        <item sortOrder="0" name="reqConnectURL"
              label="Amazon Connect CCP URL">https://yourinstancename.awsapps.com/connect/ccp</item>
        <item sortOrder="1" name="reqConnectCW"
              label="Console Phone Width">260</item>
        <item sortOrder="2" name="reqConnectCH"
              label="Console Phone Height">465</item>
        <item sortOrder="3" name="reqConnectCLCW"
              label="Classic Phone Width">195</item>
        <item sortOrder="4" name="reqConnectCLCH"
              label="Classic Phone Height">460</item>
        <item sortOrder="5" name="reqConnectLW"
              label="Lightning Container Width">260</item>
        <item sortOrder="6" name="reqConnectLH"
              label="Lightning Container Height">465</item>
        <item sortOrder="7" name="reqConnectLCW"
              label="Lightning Phone Width">266</item>
        <item sortOrder="8" name="reqConnectLCH"
              label="Lightning Phone Height">512</item>
        <item sortOrder="9" name="reqConnectPhoneFormat"
              label="Phone Number Formatting">{"OPF":"0","NPF":"1","Country":"US","NF":"International_plaintext","TNF":"(555) 123-4567"}</item>
    </section>
</callCenter>
```

------
Edit the call center configuration as follows:

For CTI Adapter URL, type the one of the following, based on your Salesforce interface:

/apex/amazonconnect__ACSFCCP_Classic
/apex/amazonconnect__ACSFCCP_Console
/apex/amazonconnect__ACSFCCP_Lightning


For Salesforce Compatibility Mode, choose Classic for the Salesforce Classic and Salesforce Console or Lightning for Lightning Experience.

#### Amazon Connect CCP URL

Your Amazon admin can provide this url. It is of the format https://<instance>.awapps.com/connect/cpp

For Amazon Connect CCP URL, type the CCP URL for your instance (for example, https://instance.awsapps.com/connect/ccp).


For Phone Number Formatting, Country, specify the appropriate 2-digit ISO country code.

To provide users with access to the CCP, choose **Manage Call Center Users** add the call-center user.


------


#### Important 

Whitelist your Salesforce Visualforce domain URL using the directions in Application Integration. This URL usually has the following format:

Documentation Url for th Application intergration is: http://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-instance.html#app-integration

[Application Integration](http://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-instance.html#app-integration)

```https://amazonconnect.instance.visual.force.com```
------

#### How to verify the URL is whitelisted?

To verify the URL, open the Visualforce page in setup.

-----


Log in to your Amazon Connect instance.

Launch Salesforce. 

You should see the integrated CCP in the side panel (Salesforce Classic) or the phone toolbar (Salesforce Classic and Lightning Experience).
