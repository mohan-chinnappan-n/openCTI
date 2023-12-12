### Amazon connect setup notes

#### References:

1. [Amazon Connect and Salesforce Integration ](http://docs.aws.amazon.com/connect/latest/adminguide/salesforce-integration.html)

2. [Enabling Amazon Connect with Salesforce Service Cloud and Sales Cloud](https://aws.amazon.com/blogs/apn/enabling-amazon-connect-with-salesforce-service-and-sales-cloud/)

3. [Salesforce Announces Service Cloud Einstein and Amazon Connect Integration](https://www.salesforce.com/company/news-press/press-releases/2017/03/170328-3.jsp)

The Amazon Connect CTI Adapter provides a WebRTC browser-based Contact Control Panel (CCP) within Salesforce. This integration enables your agents to leverage both inbound caller ID screen pop and outbound click to call/transfer/conferencing.

We recommend that you initially install the package into your Salesforce sandbox. After the package is installed, you can configure your Salesforce Call Center configuration within Salesforce. This configuration is a XML file that you import into your call center. It provides all the details required to enable the CTI.

The next step is to :
**whitelist your Salesforce Visualforce domain within your Amazon Connect Application integration**. This allows cross-domain access to your Amazon Connect instance.
 
#### Prerequisites

1. Salesforce Classic, Salesforce Console, or Lightning Experience
2. An Amazon Connect instance
3. Firefox or Chrome browser
4. To integrate with Salesforce

In your Salesforce sandbox, install the following managed package: 
[Amazon Connect CTI Adapter](https://appexchange.salesforce.com/listingDetail?listingId=a0N3A00000EJH4yUAH)

![AppExchange app](https://d2908q01vomqb2.cloudfront.net/77de68daecd823babbb58edb1c8e14d7106e83bb/2017/09/06/Connect2.png)


After the package has been installed, the next step is to set up your Salesforce call center configuration. This configuration is a XML file you import into your call center, which provides all the details required to enable the Amazon Connect CTI Adapter. First, download the call center XML configuration and import it into your Lightning call center configuration:



Download the AmazonConnectCallCenterConfig.xml file and import it into your Salesforce call center configuration.

![callcenter setup](https://d2908q01vomqb2.cloudfront.net/77de68daecd823babbb58edb1c8e14d7106e83bb/2017/09/06/Connect3.png)


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

![editing setup](https://d2908q01vomqb2.cloudfront.net/77de68daecd823babbb58edb1c8e14d7106e83bb/2017/09/06/Connect4.png)




For CTI Adapter URL, type the one of the following, based on your Salesforce interface:

/apex/amazonconnect__ACSFCCP_Classic
/apex/amazonconnect__ACSFCCP_Console
/apex/amazonconnect__ACSFCCP_Lightning


For Salesforce Compatibility Mode, choose Classic for the Salesforce Classic and Salesforce Console or Lightning for Lightning Experience.


Note:

1. The suffix for the Amazon Connect CTI Adapter URL is set to Lightning. If you were configuring the Amazon Connect CTI Adapter for Classic or Console, those suffixes would be used instead.
2. Salesforce Compatibility Mode is set for Lightning. This would be set to Classic if you were configuring for Classic or Console.
3. The Amazon Connect CCP URL is set to your Amazon Connect instance name. (replace YOURINSTANCENAME with your Amazon Connect instance name).
4. If you are using this in another country (i.e. Great Britain), set the appropriate two digit ISO country code.
5. Provide access to users (i.e. admins, supervisors, agents) who will be using the CCP.


#### Amazon Connect CCP URL

Your Amazon admin can provide this url. It is of the format https://<instance>.awapps.com/connect/cpp

For Amazon Connect CCP URL, type the CCP URL for your instance (for example, https://mysinstance.awsapps.com/connect/ccp).


For Phone Number Formatting, Country, specify the appropriate 2-digit ISO country code.

To provide users with access to the CCP, choose **Manage Call Center Users** add the call-center user.


------


#### Important 


**whitelist your Salesforce Visualforce domain within your Amazon Connect Application integration**

![Whitelisting](https://d2908q01vomqb2.cloudfront.net/77de68daecd823babbb58edb1c8e14d7106e83bb/2017/09/06/Connect5.png)

Whitelist your Salesforce Visualforce domain URL using the directions in **Amazon Connect Application Integration**. This URL usually has the following format:

Documentation Url for th Application intergration is: http://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-instance.html#app-integration

[Application Integration](http://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-instance.html#app-integration)

```https://amazonconnect.<instance>.visual.force.com```

instance : your Amazon Connect instance name.

------

#### How to verify the URL is whitelisted?

To verify the URL, open the Visualforce page in setup.

![Verfiy whitelisting](https://d2908q01vomqb2.cloudfront.net/77de68daecd823babbb58edb1c8e14d7106e83bb/2017/09/06/Connect6.png)


-----


Log in to your Amazon Connect instance.

URL for this :https://YOURINSTANCENAME.awsapps.com/connect/login

Open another tab and log into your Salesforce:

You should see the integrated CCP in the side panel (Salesforce Classic) or the phone toolbar (Salesforce Classic and Lightning Experience).

You will see similar to this:

![Setup complete](https://d2908q01vomqb2.cloudfront.net/77de68daecd823babbb58edb1c8e14d7106e83bb/2017/09/06/Connect7.png)

**Click to Dial**

You should notice that all numbers have a phone icon next to them in Salesforce pages with phone number fields.

![Click to dial](https://d2908q01vomqb2.cloudfront.net/77de68daecd823babbb58edb1c8e14d7106e83bb/2017/09/06/Connect8.png)

It will make an outbound call via the Amazon Connect CCP and connect to the customer when they answer the call.


![outbound call](https://d2908q01vomqb2.cloudfront.net/77de68daecd823babbb58edb1c8e14d7106e83bb/2017/09/06/Connect9.png)

**AfterTheCall**

![after the call](https://d2908q01vomqb2.cloudfront.net/77de68daecd823babbb58edb1c8e14d7106e83bb/2017/09/06/Connect10.png)


Once you complete the call, the Amazon Connect CCP will go into AfterCallWork status where the agent can perform any follow up activities (e.g. logging a call). After these activities are completed, they can make themselves available to take more calls.



**Inbound calls**

If the agent is in an available state and they receive a call, the inbound call will screen pop the Amazon Connect CCP and any matching records for the caller ID.

![inbound calls](https://d2908q01vomqb2.cloudfront.net/77de68daecd823babbb58edb1c8e14d7106e83bb/2017/09/06/Connect11.png)


**Screen pop behavior setup**

You can also configure the screen pop behavior in the Softphone layouts under your Salesforce call center configuration.


![Screenpop](https://d2908q01vomqb2.cloudfront.net/77de68daecd823babbb58edb1c8e14d7106e83bb/2017/09/06/Connect12.png)

## Videos
[Salesforce and Amazon Connect](https://pages.awscloud.com/apn-tv-this-is-my-architecture-ep-050.html)






