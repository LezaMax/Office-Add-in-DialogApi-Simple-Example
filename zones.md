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
####Part A. Locate the Security Zone where the Office Online application is located. 
1. Look at the address bar of your browser and note the first part of the URL. In the example below that path is: http://msft-my.spoppe.com
2. While in Internet Explorer go to **Internet Options>Settings>Security**
3. Select the **Local Intranet** zone and click on **Sites**. Then click **Advanced**.  If you see the URL that you noted on step 1, proceed to Part B.
4. If the site you are looking for is not on the intranet zone, repeat the steps for the trusted sites zone. 

####Part B. 
Once you have located in which internet zone the Office online application is you need to add the URL of the add-in dialog to the same zone.
**Important Security Reminder** Do not add sites of Add-ins you don't trust
1. Copy the Add-in URL that the warning gave you. In this example that is: https://dialog-test.azurewebsites.net
2. Add the URL to the corresponding security Zone. While on the dialog for the corresponding zone, enter the URL and click on "Add" 

###Developers: Use displayInFrame
The issue depicted in this article only occurs when the Dialog API is used in pop-up mode. Use the displayInFrame flag to avoid hitting this complication. For example:

```
Office.context.ui.displayDialogAsync(startAddress, {displayInFrame:true}, callback);
```

##Additional Technical information
Internet Explorer has a security feature called "Security Zones". Websites on different security zones cannot communicate with each other via the browser. 

When developers use the Dialog API in pop-up mode, a new window is created and navigated to the URL. If the domain of the dialog URL is in a different security zone as the domain of the website hosting the Office Online aplication, the dialog cannot communicate back with Office. 
