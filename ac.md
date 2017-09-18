### Amazon connect notes

[Amazon Connect and Salesforce Integration ](http://docs.aws.amazon.com/connect/latest/adminguide/salesforce-integration.html)


<div id="main-content">
                  <div id="main-col-body">
                     <table summary="Breadcrumbs">
                        <tbody><tr>
                           <td>
                              <div class="breadcrumb"><a href="http://aws.amazon.com/documentation">AWS Documentation</a> » <a href="http://aws.amazon.com/documentation/connect">Amazon Connect</a> » <a href="index.html">Administrator Guide</a> » <span class="breadcrumb">Amazon Connect and Salesforce Integration</span></div>
                           </td>
                        </tr>
                     </tbody></table>
                     <div></div>
                     <h1 class="topictitle" id="salesforce-integration">Amazon Connect and Salesforce Integration</h1>
                     <p>The Amazon Connect CTI Adapter provides a WebRTC browser-based Contact Control Panel
                        (CCP) within Salesforce.  
                        This integration enables your agents to leverage both inbound caller ID screen pop
                        and 
                        outbound click to call/transfer/conferencing.
                     </p>
                     <p>We recommend that you initially install the package into your Salesforce sandbox.
                        After the package  
                        is installed, you can configure your Salesforce Call Center configuration within Salesforce.
                        This 
                        configuration is a XML file that you import into your call center. It provides all
                        the details required 
                        to enable the CTI.
                     </p>
                     <p>The next step is to whitelist your Salesforce Visualforce domain within your Amazon
                        Connect Application integration. 
                        This allows cross-domain access to your Amazon Connect instance.
                     </p>
                     <div class="itemizedlist">
                        
                        <p class="title"><b>Prerequisites</b></p>
                        
                        
                        
                        
                        <ul class="itemizedlist" type="disc">
                           <li class="listitem">
                              <p>Salesforce Classic, Salesforce Console, or Lightning Experience</p>
                           </li>
                           <li class="listitem">
                              <p>An Amazon Connect instance</p>
                           </li>
                           <li class="listitem">
                              <p>A Firefox or Chrome browser</p>
                           </li>
                        </ul>
                     </div>
                     <p class="title"><b>To integrate with Salesforce</b></p>
                     <ol>
                        <li>
                           
                           <p>In your Salesforce sandbox, install the following managed package:
                              <a href="https://appexchange.salesforce.com/listingDetail?listingId=a0N3A00000EJH4yUAH" target="_top">Amazon Connect CTI Adapter</a>.
                           </p>
                           
                        </li>
                        <li>
                           
                           <p>Download the <a href="http://amazonconnect-sfdc-installation.s3-website-us-east-1.amazonaws.com/resources/24AC4F3F034E447BE9CEAEE5CA37BFC3.xml" target="_top">AmazonConnectCallCenterConfig.xml</a> file and import it into your Salesforce call center configuration.
                           </p>
                           
                        </li>
                        <li>
                           
                           <p>Edit the call center configuration as follows:</p>
                           
                           <div class="itemizedlist">
                              
                              
                              
                              
                              
                              
                              <ul class="itemizedlist" type="disc">
                                 <li class="listitem">
                                    
                                    <p>For <b>CTI Adapter URL</b>, type the one of the following, based on your Salesforce interface:
                                    </p>
                                    
                                    <div class="itemizedlist">
                                       
                                       
                                       
                                       
                                       <ul class="itemizedlist" type="disc">
                                          <li class="listitem">
                                             <p><strong class="userinput"><code>/apex/amazonconnect__ACSFCCP_Classic</code></strong></p>
                                          </li>
                                          <li class="listitem">
                                             <p><strong class="userinput"><code>/apex/amazonconnect__ACSFCCP_Console</code></strong></p>
                                          </li>
                                          <li class="listitem">
                                             <p><strong class="userinput"><code>/apex/amazonconnect__ACSFCCP_Lightning</code></strong></p>
                                          </li>
                                       </ul>
                                    </div>
                                    
                                 </li>
                                 <li class="listitem">
                                    
                                    <p>For <b>Salesforce Compatibility Mode</b>, choose <b>Classic</b> for the
                                       Salesforce Classic and Salesforce Console or <b>Lightning</b> for Lightning Experience.
                                    </p>
                                    
                                 </li>
                                 <li class="listitem">
                                    
                                    <p>For <b>Amazon Connect CCP URL</b>, type the CCP URL for your instance
                                       (for example, https://<em class="replaceable"><code>instance</code></em>.awsapps.com/connect/ccp).
                                    </p>
                                    
                                 </li>
                                 <li class="listitem">
                                    
                                    <p>For <b>Phone Number Formatting</b>, <b>Country</b>, specify the appropriate 
                                       2-digit <a href="https://countrycode.org/" target="_top">ISO country code</a>.
                                    </p>
                                    
                                 </li>
                                 <li class="listitem">
                                    
                                    <p>To provide users with access to the CCP, choose <b>Manage Call Center Users</b>.
                                    </p>
                                    
                                 </li>
                              </ul>
                           </div>
                           
                        </li>
                        <li>
                           
                           <p>Whitelist your Salesforce Visualforce domain URL using the directions in <a href="amazon-connect-instance.html#app-integration">Application Integration</a>. This URL usually has the following format:
                           </p>
                           <pre class="programlisting"><code class="nohighlight">https://amazonconnect.<em class="replaceable"><code class="">instance</code></em>.visual.force.com</code></pre>
                           <p>To verify the URL, open the Visualforce page in setup.</p>
                           
                        </li>
                        <li>
                           
                           <p>Log in to your Amazon Connect instance.</p>
                           
                        </li>
                        <li>
                           
                           <p>Launch Salesforce. You should see the integrated CCP in the side panel (Salesforce
                              Classic) or the
                              phone toolbar (Salesforce Classic and Lightning Experience).
                           </p>
                           
                        </li>
                     </ol>
                  </div>
                  <div id="main-col-footer">
                     <div id="doc-conventions"><a target="_top" href="/general/latest/gr/docconventions.html">Document Conventions</a></div>
                     <div id="next"><a class="awstoc" accesskey="p" href="connect-lambda-functions.html">« Previous </a><a class="awstoc" accesskey="n" href="doc-history.html">Next »</a></div>
                     <div id="copyright-main-footer">© 2017, Amazon Web Services, Inc. or its affiliates. All rights reserved.</div>
                  </div>
               </div>
