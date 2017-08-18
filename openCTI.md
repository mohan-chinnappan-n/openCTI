


### Open CTI

Ref:

[Open CTI Developer Guide](https://developer.salesforce.com/docs/atlas.en-us.api_cti.meta/api_cti/sforce_api_cti_intro.htm)

![](https://developer.salesforce.com/docs/resources/img/en-us/208.0?doc_id=help%2Fimages%2FCTI_arch_overview.png&folder=api_cti)

What is Open CTI ?

Build and integrate third-party computer-telephony integration (CTI) systems with **Salesforce Call Center** using a **browser-based JavaScript API**.


Browser is used as clients (instead of desktop fat-clients)

With Open CTI:

1. you can make calls from a **softphone directly** in Salesforce without installing CTI adapters on your machines. 

2. Create customizable softphones (call-control tools) that function as fully integrated parts of Salesforce and the Salesforce console.

3. Provide users with CTI systems that are browser and platform agnostic


**What is Desktop CTI (aka CTI Toolkit)?**

Desktop CTI, also known as the CTI Toolkit, is the predecessor to Open CTI. Desktop CTI required adapters to be installed on **each call center user’s machine**. 

With Open CTI, those user-side adapters are a **thing of the past**.

Desktop CTI is **retired** and you must **migrate** to Open CTI. Work with your partners to create an Open CTI implementation.


**What is  Salesforce Voice ?**

Salesforce Voice provides a way to provision numbers and make calls directly from Salesforce. 

However, if you already have **a telephony system in place**, Open CTI is the way to go since it **integrates to that existing system**.


 If your organization may have complex business processes that are **unsupported by Open CTI** functionality:
 
 You can use Force.com platform to implement custom functionality
 
 1. SOAP API
 2. Visualforce
 3. Console API
 4. Apex


**Versions**

Open CTI matches the API version for any given release. For example, if the current version of **SOAP API** is 40.0, then there’s also a version 40.0 of Open CTI.





#### UI

Separate Open CTI APIs for **Salesforce Classic** and **Lightning Experience**.

In Salesforce Classic

- If you want to make calls using a **softphone in Salesforce Classic**
- You want to make calls using a **softphone in a Salesforce Classic console app**



```
// script:
/support/api/40.0/interaction.js

// method call example
sampleMethod(var1,var2…)


```

In Lightning Experience

- You want to make calls using a softphone in **Lightning Experience**
- You want to make calls using a softphone in a **Lightning Experience console app**




```

// script:
/support/api/40.0/lightning/opencti_min.js

// method call example
sampleMethod({
	arg1 : value1,
	arg2 : value2,
	...
})


```


### Setup

1. Create a Lightning app 
2. add the Open CTI Softphone to your utility bar
3. In the call center definition file:
     the ``` reqSalesforceCompatibilityMode ``` item must be set to ```Lightning or Classic_and_Lightning```.




### Salesforce Call Center
![SF call center](./img/SF-Call-Center.png)

How to Get Started:

  1.  Define a call center
        Specify the call center's name, IP address, port, and any other connection information.
  
 2.   Enter dialing options for international, long distance, and external calls.
    Manage users
        Select the users you want to be members of the call center.
 3. Update the call center directory
        Add useful phone numbers beyond the call center user extensions that salesforce.com automatically includes.
        
 4. Configure softphone layouts
        Select the call details and **Salesforce objects that are automatically displayed with inbound, outbound, and internal calls**.
        Assign a softphone layout to any user profile.
        
        

What is Salesforce Call Center?

A call center corresponds to a **single** computer-telephony integration (CTI) system already in place at your organization. 

Salesforce.com **users** must be **assigned** to a **call center** before they can use any Call Center features.



![SF call center setup](./img/call-center-setup.png)

![SF call center adding users](./img/adding-users.png)


Note:

If you want your Open CTI implementation to work in **Lightning Experience** and in a **console in Salesforce Classic**, develop a **unique implementation** that uses both Open CTI for Salesforce Classic and Lightning Experience.



Methods:

***Same/similar in - Classic and LX***

1. ```enableClickToDial()```
2. ```disableClickToDial()```
3. ```onClickToDial()```
4. ```getCallCenterSettings()```
5. ```getPageInfo()```
6. ```getSoftphoneLayout()```
7. ```isVisible()```  in  lx: ```isSoftphonePanelVisible()```
8. ```onFocus()```    in  lx: ```onNavigationChange()```
9. ```refreshPage()``` in lx: ```refreshView()```
10. ```refreshRelatedList()``` in lx ```refreshView()```
11. ```reloadFrame()``` in lx: ```refreshView()```
12. ```runApex()```
13. ```saveLog()```
14. ```screenPop()```
15. ```searchAndScreenPop()```
16. ```setSoftphoneHeight()``` in lx: ```setSoftphonePanelHeight()```
17. ```setSoftphoneWidth()```  in lx: ```setSoftphonePanelWidth()```
18. ```setVisible()``` in lx: ```setSoftphonePanelVisibility()```

***Different in - Classic and LX***

1. ```searchAndGetScreenPopUrl()``` in lx: use ```searchAndScreenPop()```
2. ```isInConsole()``` in lx: NA
3. ```getDirectoryNumbers()	``` in lx: NA




### Call Center Definition Files

- specifies a set of fields and values that are used to define a call center in Salesforce for a particular softphone

- Salesforce uses call center definition files to support the integration of Salesforce CRM Call Center with **multiple CTI system vendors**.

- If you build a custom softphone with Open CTI, you must write a call center definition file to support it. 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<CallCenter xmlns="http://soap.sforce.com/2006/04/metadata">
    <adapterUrl>/apex/demoAdapterPage</adapterUrl>
    <customSettings>{&quot;reqTimeout&quot;:&quot;10000&quot;,&quot;reqStandbyUrl&quot;:&quot;/apex/demoAdapterPage2&quot;,&quot;reqSoftphoneHeight&quot;:&quot;550&quot;,&quot;reqSoftphoneWidth&quot;:&quot;400&quot;,&quot;reqUseApi&quot;:&quot;true&quot;,&quot;reqSalesforceCompatibilityMode&quot;:&quot;Classic_and_Lightning&quot;}</customSettings>
    <displayName>Demo Call Center Adapter</displayName>
    <displayNameLabel>Display Name</displayNameLabel>
    <internalNameLabel>InternalName</internalNameLabel>
    <sections>
        <items>
            <label>CTI Adapter URL</label>
            <name>reqAdapterUrl</name>
            <value>/apex/demoAdapterPage</value>
        </items>
        <items>
            <label>CTI Adapter URL2</label>
            <name>reqStandbyUrl</name>
            <value>/apex/demoAdapterPage2</value>
        </items>
        <items>
            <label>Timeout</label>
            <name>reqTimeout</name>
            <value>10000</value>
        </items>
        <items>
            <label>Use CTI API</label>
            <name>reqUseApi</name>
            <value>true</value>
        </items>
        <items>
            <label>Softphone Height</label>
            <name>reqSoftphoneHeight</name>
            <value>550</value>
        </items>
        <items>
            <label>Softphone Width</label>
            <name>reqSoftphoneWidth</name>
            <value>400</value>
        </items>
        <items>
            <label>Salesforce Compatibility Mode</label>
            <name>reqSalesforceCompatibilityMode</name>
            <value>Classic_and_Lightning</value>
        </items>
        <label>General Information</label>
        <name>reqGeneralInfo</name>
    </sections>
    <sections>
        <items>
            <label>Outside Prefix</label>
            <name>reqOutsidePrefix</name>
            <value>9</value>
        </items>
        <items>
            <label>Long Distance Prefix</label>
            <name>reqLongDistPrefix</name>
            <value>1</value>
        </items>
        <items>
            <label>International Prefix</label>
            <name>reqInternationalPrefix</name>
            <value>01</value>
        </items>
        <label>Dialing Options</label>
        <name>reqDialingOptions</name>
    </sections>
    <sections>
        <items>
            <label>Simulated Incoming Phone Number</label>
            <name>reqIncomingNumber</name>
            <value>(415) 555-1212</value>
        </items>
        <items>
            <label>CTI Provider</label>
            <name>reqProvider</name>
            <value>DummyProvider</value>
        </items>
        <items>
            <label>Provider Account</label>
            <name>reqProviderAccount</name>
            <value>AXXXXXXXXXXXXXXXXX</value>
        </items>
        <items>
            <label>Provider Auth Token</label>
            <name>reqProviderAuthToken</name>
            <value>YYYYYYYYYYYYYYYYYY</value>
        </items>
        <items>
            <label>Provider Caller Number</label>
            <name>reqProviderCallerNumber</name>
            <value>415555555</value>
        </items>
        <label>Phone Demo Settings</label>
        <name>reqPhoneDemoSettings</name>
    </sections>
</CallCenter>

```









#### Open CTI Lightning Demo Adapter
This CTI demo adapter package lets you test drive Open CTI for Lightning Experience. The package provides a demo softphone that highlights and demonstrates the main features of Open CTI for Lightning Experience without even connecting to a phone system.

[open cti demo adapter](https://github.com/developerforce/open-cti-demo-adapter)


----

###IVR, ACD, Auto-Attendant, Voicemail. What’s The Difference?




**IVR – Interactive Voice Response**
Interactive Voice Response (IVR) is a technology that allows a computer to interact with humans using voice commands or tones from a telephone keypad (DTMF, or Dual Tone Multifrequency, the beeps your phone makes when you dial). Technically, IVR lets the caller enter an “ID” or account code, then provides access to a database. This is where the “interactive” part comes in. Banks and Credit Unions often have “phone bank” systems that allow you to conduct transactions. This is IVR.


**ACD — Automatic Call Distribution**
ACD Systems answer incoming calls and allow the caller to choose a menu, group of extensions or singular extension to which the call is routed. The term is used in large call centers to describe the system of organizing incoming calls into queues of callers waiting to speak with an operator or service person.

**Automated Attendant**
The term Automated attendant is essentially the same as ACD. The incoming call is answered automatically, then allows callers to choose where the call is routed. Automated Attendant is also called Auto-Attendant, AA or Virtual Receptionist. Typically a simple menu such as, “press 1 to speak with our parts department, press 2 for directions to our store…” is offered. Callers can be routed to an extension, an outside line or a recording. Some Auto Attendant Systems are a part of a business phone system, while many are “add-on” systems (sometimes part of the Voicemail System).

**Voicemail**
A Voicemail System is designed specifically for recording a message from the caller’s voice (leaving a message for the intended party). Voicemail Systems can be operated by simple devices such as answering machines, remotely operated as with your cell phone voicemail, or added to a business phone system. Examples are Nortel Call Pilot, Star Flash and various systems by Avaya, Cisco, 3com, Mitel and others. Such systems are often “add-ons” to a PBX system As more businesses move into I.P. telephony (hosted PBX solutions), Voicemail is likely part of a Unified Messaging System, which can combine cell phone, email, voicemail and other types of messaging.

**CCR Tree**
A Custom Call Routing (CCR) Tree refers to the part of a Voicemail, IVR or Automated Attendant system that designates the departments and extensions to which callers are routed. Callers are prompted at each stage in the routing process by a recorded voice. CCR Trees can contain multiple menus and sub-menus to allow callers to obtain more specific information. Often, business callers complain about being “trapped in a call center loop” or “voicemail hell”. This is what happens when a CCR Tree is not well planned. Frequently-used pathways should be considered, as well as the length of voiced prompts. 

  
***Tips***

If you are considering setting up a voice response or voicemail system for your company, here are a few tips to consider:

Consider the length of each message (callers can be impatient).
Use consistent language (all department and extension names must be accurate in every menu).
Take time to write out every word that you want callers to hear. Test it by speaking it aloud.
Talk to your I.T. or telephony consultant to be sure you understand time/memory limits your system may have.
Discuss call routing architecture with the equipment provider as well as your tech and marketing teams.
Consider using professional voice talent with experience in voicemail and IVR recording. Your callers will notice the difference.


Ref:

[IVR, ACD](http://easyonhold.com/blog/ivr-acd-auto-attendant-voicemail-whats-the-difference/)




	











 



