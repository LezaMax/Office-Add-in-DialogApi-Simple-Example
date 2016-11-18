##Troubleshoot: An Office Add-in Dialog cannot be displayed
##Affected applications and Symptoms
**Applicable Office Applications**: 
- Affected: Online(Web) versions of Word, Excel, PowerPoint, OneNote, Outlook. 
- Not affected: Windows, Mac and IPad versions of Office

**Applicable Browsers**: 
- Affected: Internet Explorer and Edge. 
- Not affected: Chrome, Firefox and Safari. 

**Symptoms**: 
When using an Office add-in, you are asked to allow a dialog to be displayed. Upon allowing the dialog your receive the following message: 

```
The security settings in your browser prevent us from creating a dialog box. Try a different browser, or configure your browser, so that [URL] and the domain shown in your address bar are in the same security zone
```
[Add screenshot]

##Resolution
###End users and Administrators: Configure Internet Explorer Zones
Step 1. Locate the Security Zone where the Office Online application is located. 
1. Look at the address bar of your browser and note the first part of the URL. In the example below that path is: http://msft-my.spoppe.com
2. While in Internet Explorer go to **Internet Options>Settings>Security**
3. Select the **Local Intranet** zone and click on **Sites**. Then click **Advanced**. 

Step 2. 

###Developers: Use displayInFrame


##Additional Technical information
Internet Explorer has a security feature called "Security Zones". Websites on different security zones cannot communicate with each other via the browser. 

When developers use the Dialog API in pop-up mode, a new window is created and navigated to the URL 
