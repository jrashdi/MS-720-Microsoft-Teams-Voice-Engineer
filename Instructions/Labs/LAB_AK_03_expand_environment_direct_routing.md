---
lab:
    title: 'Lab: Expand your Teams Voice Environment to use Direct Routing'
    type: 'Answer Key'
    module: 'Module 1: Plan and configure Teams Phone'
---

# Lab 03: Expand your Teams Voice Environment to use Direct Routing
# Student lab answer key

## Lab scenario

As part of the expanding business the organization has an existing SIP trunk into their primary data center. The contractual obligations mean that it’s more cost effective to utilise the SIP trunk and move to Microsoft Calling Plans later. As part of the move Megan will be moved from the old telephone system to the new Microsoft Phone System solution. 

## Lab Setup

  - **Estimated Time**: 255 minutes

## Instructions

## Exercise 1: Configure the session border controller

### Exercise Duration

  - **Estimated Time to complete**: 90 minutes

In this exercise, you will configure the session boarder controller, install the services needed to ensure the custom domain and SBC work as expected.

### Task 1 – Add the SBC to the tenant

In this task you will verify add your SBC to your tenant.

1. You are still on CLIENT01 and signed in as “Lab User”.

2. Open a new tab in Microsoft Edge and then browse to **[https://admin.teams.microsoft.com](https://admin.teams.microsoft.com/).**

3. Sign in as **MOD Administrator** with the credentials provided to you.

4. In the left navigation select **Voice**, select **Direct Routing** and select **Add**.

5. Add the FQDN **sbc01.Lab&lt;customlabnumber&gt;.O365Ready.com** and select **Save**.

6. Leave the browser open at the end of this task.

You have successfully verified that your custom domain and added SBC to the to the tenant.

### Task 2 - Retrieve your public certificate file

In the following task you will download the DigiCert certificate you requested earlier in the lab so you can use it for your SBC. This step is required to upload the certificate in the compressed archive container in the next task.

1. You are still on CLIENT01 where you are still signed in as “Lab User” 

2. Open Microsoft Edge and then browse to **Outlook on the web** [**https://outlook.office.com**](https://outlook.office.com/), where you should still be signed in as the **MOD Administrator**.

3. In the message list, locate and select the email from **DigiCert** with the zip file attachment. The message may arrive in the Focused or Other folder and should arrive within 2-5 minutes.

4. Download the **sbc01_Lab&lt;customlabnumber&gt;.O365Ready.com**XXXXXXX.**zip** file attachment and save it to **C:\LabFiles**.

5. Close the browser window to end the task.

You have successfully downloaded the certificate you requested in an earlier exercise and it is now available to certify your SBC.

**Warning**: Download the file as is. Do not compress the already compressed zip file. Some web-based email systems allow you to compress or zip your download. This will cause the already compressed file to be compressed again and will cause the script in this lab to fail.

### Task 3 - Run the ImportLabCert script located in C:\Scripts

In the following task you will import the certificate to the machine running the SBC.

1. You are still on CLIENT01 where you are still signed in as “Lab User”.

2. Switch to File Explorer and then browse to **C:\Scripts**.

3. Select **ImportLabCert.exe**.

4. In the **User Account Control** dialog box, select **Yes**.

5. In the window, select **Import lab certificate**.

6. When the script completes, select **Finish**.

7. Close File Explorer.

You have successfully imported the certificate to the SBC.

### Task 4 - Upload the Session Border Controller (SBC) configuration

In the following task you will update the existing configuration file to your SBC to set it up.

1. You are still on CLIENT01 where you are still signed in as “Lab User”.

2. Open a new Microsoft Edge browser window and navigate to **http://192.168.0.200**.

3. On the Web Login page, sign in as **Admin** with password **Admin**.

4. In the top navigation menu, select **ADMINISTRATION**.

5. In the left navigation, select **MAINTENANCE &gt; Configuration File**.

6. In the Configuration File window, under **INI FILE**, under **Load INI file to the device**, select **Choose File**.

7. Browse to **C:\LabFiles**, select **Lab&lt;customlabnumber&gt;-SBC01-Config.ini**, and then select **Open**.

8. To the right of the configuration file path, select **Load INI file**.

9. Review the dialog box and then select **OK**.

10. Leave the browser window open for the next task.

Wait for the SBC to restart. When finished restarting, the browser will refresh to the sign in page. You have successfully setup the SBC.

### Task 5 - Upload root certificates to the SBC

In the following task you will add the root certificate to the session border controller.

1. You are still on CLIENT01 where you are still signed in as “Lab User” and on the SBC configuration website as **Admin**.

2. On the top menu, select **IP NETWORK**.

3. In the left navigation, select **SECURITY &gt; TLS Contexts**.

4. In the results pane, in the **TLS Contexts** table, select **Teams-TLSContext**.

5. Scroll down, and below the Teams-TLSContext information, select **Trusted Root Certificate**.

6. In the Trusted Root Certificates window, select **Import**.

7. In the **Import New Certificate** dialog box, select **Choose File**.

8. Browse to **C:\LabFiles**, select **BaltimoreTrustedRootCA.cer**, and then select **Open**.

9. In the **Import New Certificate** dialog box, select **Ok**.

10. Review the information for the selected root certificate that was installed.

11. Perform the steps above and load the following root certificates:

	- **DigicertTrustedRoot.cer**

	- **DigicertTrustedRootIntermediate.cer**

12. When complete, in the Trusted Root Certificates window, to the left of **TLS Context[#1]**, select the back arrow icon.

13. Leave the browser window open for the next task.

You have successfully uploaded the root certificate to your SBC and can now continue uploading the lab certificate in the chain.

### Task 6 - Upload the lab certificate to the SBC

In the following task you will upload the lab certificate you requested earlier.

1. You are still on CLIENT01 where you are still signed in as “Lab User” and on the SBC configuration website as **Admin**.

2. In the TLS Contexts window, in the **TLS Contexts** table, select **Teams-TLSContext**.

3. Scroll down, and below the Teams-TLSContext information, select **Change Certificate**.

4. In the Change Certificates window, scroll down to the **UPLOAD CERTIFICATE FILES FROM YOUR COMPUTER** section.

5. In the **Private key pass-phrase (****optional****)** box, enter **labpass@word1**.

6. Under **Send Private Key file from your computer to the device**, select **Choose File**.

7. In the Open window, browse to **C:\LabFiles**, select **Labcert.pfx**, and then select **Open**.

8. To the right of the lab certificate file path, select **Load File**.

9. Review the banner and verify that the certificate was loaded.

10. Leave the browser window open for the next task.

You have successfully uploaded the lab certificate and prepared your SBC to sign its communication.

### Task 7 - Update the outbound manipulation set

In the following task you will upload two message manipulations that were already created for the lab and updated by the directrouting.exe script.

1. You are still on CLIENT01 where you are still signed in as “Lab User” and on the SBC configuration website as **Admin**.

2. In Microsoft Edge, browse to **http://192.168.0.200/AdminPage**.

3. In the left navigation, select **ini** **Parameters**.

4. In the **Parameter Name** box, enter **GWOutboundManipulationSet**.

5. In the **Enter Value** box, enter **0**.  
‎This is the manipulation set ID value.

6. Select **Apply New Value**.

7. Review the information in the **Output Window**.

8. In the left navigation, select **Back to Main**.

9. In the top navigation menu, select **Save**.

10. In the **Save Configuration** dialog box, select **Yes**.

11. Close the browser window open to end this task.

You have successfully uploaded the already existing message manipulations for your SBC. This will transform user input into the required formats.

You have successfully configured the AudioCodes SBC to receive requests from the Microsoft 365 Direct Route service. 

## Exercise 2: Configure direct routing settings

### Exercise Duration

  - **Estimated Time to complete**: 120 minutes

In this exercise, you will create a direct route routing policy, PSTN Usage policy, and voice route to enable Megan Bowen to perform voice calls over the SBC. Megan resides in a location where the telephone number assigned to her has a long-standing contract and requires her to continue to use the telephone service provider telephone number rather than moving to a calling plan from Microsoft. Long term the plan is to move the telephone number over to a calling plan, however, currently this is cost prohibitive. 

### Task 1 - Create a voice routing policy with one PSTN usage

In the following task you will create your first voice routing policy and PSTN usage so you can later assign this policy to your users.

1. You are still on CLIENT01 where you are still signed in as “Lab User”.

2. Select the Windows symbol in the task bar, type **PowerShell** and open a regular PowerShell window.

3. In Windows PowerShell, enter the following cmdlet to connect to Teams in your tenant:

```powershell
Connect-MicrosoftTeams
```

4. In the prompt sign in as **Katie Jordan** with the credentials provided to you.

5. In Windows Powershell, enter the following and then press Enter. By running the command you will see that the existing PSTN usages in place. You can see what is in place and what usage plans are being assigned to the identity. 

```powershell
Get-CsOnlinePstnUsage
```

6. Review the output of the command.

If you have several usages defined, the names of the usages might truncate. Use the command, (Get-CSOnlinePSTNUsage).Usage, to display a list of the defined PSTN usages. An online PSTN usage links an online voice policy to a route. The output will show if there is an identity that can be used or possibly reused, or also excluded from being used. For example there may be a PSTN usage called Seattle, that can cover all of the Pacific North West of the United States. The overall goal is to keep your PSTN Usage rules to a minimum and keep them simple as it will reduce the overall administration effort later. We want to validate that the information we have in the tenant is relevant and also ensure we do not duplicate any existing PSTN usages. 

7. Run the Set-CSOnlinePSTNUsage cmdlet is used to add or remove phone usages to or from the usage list. This list is global so it can be used by policies and routes throughout the tenant:

```powershell
Set-CsOnlinePstnUsage -Identity Global -Usage @{Add="US and Canada"}
```

8. Run the New-CSOnlineVoiceRoutingPolicy to create a new online voice routing policy. Online voice routing policies are used in Microsoft Phone System Direct Routing scenarios. Assigning your Teams users an online voice routing policy enables those users to receive and to place phone calls to the public switched telephone network by using your on-premises SIP trunks:

```powershell
New-CsOnlineVoiceRoutingPolicy "North America" -OnlinePstnUsages "US and Canada"
```

9. Run the New-CsOnlineVoiceRoute command - Creates a new online voice route. Online voice routes contain instructions that tell Microsoft Teams how to route calls from Office 365 users to phone numbers on the public switched telephone network (PSTN) or a private branch exchange (PBX):

```powershell
New-CsOnlineVoiceRoute -Identity "10 Digit Dialing" -NumberPattern "^\+1(\d{10})$" -OnlinePstnGatewayList lab<customlabnumber>.o365ready.com -OnlinePstnUsages "US and Canada"
```

10. Run the Get-CSOnlineVoiceRoute command, this command returns information about the online voice routes configured for use in your tenant. Online voice routes contain instructions that tell Microsoft Teams how to route calls from Office 365 users to phone numbers on the public switched telephone network (PSTN) or a private branch exchange (PBX):

```powershell
Get-CsOnlineVoiceRoute
```

11. Review the output of the command and verify that your new voice route has been added.

12. Leave the PowerShell window open for the next task.

You have successfully created a voice routing policy with a PSTN Usage.

### Task 2 - Create a new voice routing policy named North America and assign it to Megan Bowen

In the following task you will create another voice routing policy with the PSTN usage you created in an earlier task and assign this policy to your users.

1. You are still on CLIENT01 where you are still signed in as “Lab User”, and you have an open **Teams PowerShell** session signed in as **Katie Jordan**.

2. Run the Grant-CsOnlineVoiceRoutingPolicy, the command assigns a per-user online voice routing policy to one or more users. Online voice routing policies manage online PSTN usages for Phone System users:

```powershell
Grant-CsOnlineVoiceRoutingPolicy -Identity MeganB@Lab<customlabnumber>.O365ready.com -PolicyName "North America"
``` 

If you receive an error stating that the **Policy "North America" is not a user policy. You can assign only a user policy to a specific user**., wait 2-3 minutes and then retry the command. You may need to retry the command several times before it is successful and it may take up to 15 minutes before it becomes available. If the policy is still not updated in the service, you continue to the next lab and return later.

3. Run the Get-CsOnlineUser command, the command returns information about users who have accounts homed on Microsoft Teams:

```powershell
Get-CsOnlineUser MeganB | select OnlineVoiceRoutingPolicy
```

4. Review the output of the command. If the policy is empty, try the command again.

5. Leave the PowerShell window open for the next task.

You have successfully used PowerShell to assign your voice routing policy to your users.

### Task 3 - Enable users for Direct Routing, voice, and voicemail

In the following task you will enable the end user for voice services through the direct route, assign the telephone number, and enable the user for dial pad service.

1. You are still on CLIENT01 where you are still signed in as “Lab User” and you have an open **Teams PowerShell** session signed in as **Katie Jordan**.

2. Run the Set-CSUser command, the command modifies Microsoft Teams properties for an existing user account. Properties can be modified only for accounts that have been enabled for use with Microsoft Teams:

```powershell
Set-CsUser -Identity MeganB@Lab<customlabnumer>.O365ready.com -OnPremLineURI tel:+14255551234 -EnterpriseVoiceEnabled $true
```

3. The cmdlet does not provide any output. When you are back on the command prompt, leave the window open for the next task.

You have successfully assigned a telephone number to the end user and you have enabled the end user for the dial pad.

### Task 4 - Configure voice routing

In the following task you will assign a voice route to a user, this will grant the user the ability to make calls to the policy applied. 

1. You are still on CLIENT01 where you are still signed in as “Lab User” and you have an open **Teams PowerShell** session signed in as **Katie Jordan**.

2. In Windows PowerShell, enter the following and then press Enter, this will assign the policy to the identified user, in this instance the identity is **Megan Bowan**, we will be assigning her the **North American** Policy. 

```powershell
Grant-CsOnlineVoiceRoutingPolicy -Identity MeganB@Lab<customlabnumer>.O365ready.com -PolicyName "North America"
```

3. The cmdlet does not provide any output. Close the PowerShell window to end this task.

You have successfully assigned a telephone number to the end user and you have enabled the end user for the dial pad.

### Task 5 - Translate numbers to an alternate format

In the following task you will create a normalization record for a 4-digit dial plan

1. You are still signed in to CLIENT01 as “Lab User”.

2. Open Microsoft Edge and then browse to the **Microsoft Teams admin center** at https://admin.teams.microsoft.com.

3. Sign in with **Katie Jordans** credentials, who is your Teams Administrator in this lab.

4. In the left navigation pane select **Voice,** select **Dial Plans** and select **Global (Org-wide default).**

5. Under **Normalization** **rules** select **Add.**

6. Under **Name** enter **4 Digit Extension** and under Description **4-digit extension dialing.**

7. Select “**The length of the number being dialed is”** set to **4** and select **Exactly.**

8. Under **Then do this** select **Add this number to the beginning** and enter **+1425555.**

9. Verify functionality by typing **1234** into the test box and pressing **Test –** Output should be +14255551234.

10. Select **Save.**

11. Leave the browser window open for the end of this task.

You have successfully you have assigned a 4-digit extension dial to the global group.

### Task 6 - Configure Emergency Location Identification Number (ELIN)

In the following task you will assign the Emergency Location Identification number to a location existing in Microsoft Teams Admin center already. 

1. You are still signed in to CLIENT01 as “Lab User” and signed into the **Microsoft Teams admin center** as **Katie Jordan**.

2. In the left navigation pane select the three dashes, select **Locations** and select **Emergency addresses.**

3. Select **Bellevue Office Address.**

4. Leave **Organization name** as **Contoso**, Add **ELIN** as **425-555-1200.**

5. Select **Save.**

6. Leave the browser window open.

You have successfully assigned the ELIN number to the location for emergency addresses.

### Task 7 - Deploy Location-Based Routing based off of subnets

In the following task you will configure location-based routing to allow connectivity to the local SBC to the end user depending upon subnet IP address allocated. 

1. You are still signed in to CLIENT01 as “Lab User” and signed into the **Microsoft Teams admin center** as **Katie Jordan**.

2. Select the three dashes, select **Locations**, then **Network topology.**

3. Select **Add**, give the Network Site a name of **Washington** and description as **Washington Network.** Select **Location based routing** to **On.**

4. Select **Add subnets,** for **IP address** enter **192.168.0.0** and a **Network Range** of **32,** select **Apply,** select **Save**

5. Within the Teams Admin Center select **Voice**, then **Direct Routing.**

6. Select **sbc01,** select **settings** and **edit SBC**

7. Under **Location based routing and media optimization**, turn **on Location based routing**, select **Gateway site ID** to **Washington,** then select **Save.**

8. Leave the browser window open.

You have successfully implemented the Location based routing which will route your calls dependent upon the machines local subnet which it is registered to. 

## Exercise 3: Test direct routing configuration

### Exercise Duration

  - **Estimated Time to complete**: 45 minutes

In this exercise, you will verify that you can receive a phone call from a softphone to Microsoft Teams via the SBC.

### Task 1 - Open the 3CX softphone

In the following task you will use a preconfigured softphone to log the 3cx client on. 

1. You are still signed in to CLIENT01 as “Lab User” 

2. Select **Start** and then enter **3CX Phone** and select it

3. In the softphone, on the top right side of the screen, select **Lab User***.

4. Verify that on the **Account windows, the Hook** is displayed on the screen for the LabUser. The softphone has already been configured to connect to the AudioCodes Mediant VE SBC.

5. Select **OK** to close the Account window.

You have successful signed into the 3CX Phone.

### Task 2 - Sign into Microsoft Teams and test calling from a direct routing user

In the following task you will test your calling functionality from the Teams desktop app to the Softphone. For this task we will sign into **Microsoft Teams** as **Megan Bowen**.

1. You are still signed in to CLIENT01 as “Lab User” with the password provided to you.

2. Open **Microsoft Teams** from the Desktop to start the client.

3. Select **Get started** and on the **Sign in** page, enter the username of Megan Bowen **MeganB@Lab&lt;customlabnumber&gt;.O365ready.com** and sign in with the password provided.

4. Close any the introduction windows and any other notifications.

5. In the app bar on the left, select **Calls**.

6. Dial 12065559876 this will then route to the AudioCodes Registered 3CX phone. However, the device is natively off the hook and will not answer.

7. Successful outbound call will show in the outgoing call history. If the **Calls** option is not available, sign out of Microsoft Teams, wait 2-3 minutes, and then sign in again. You may need to repeat this if the option is not available after your first retry.

8. Leave the Teams Desktop client open.

You have successfully tested an outbound call from the Teams desktop app to a softphone connected to your SBC.

### Task 3 - Test calling to a direct routing user

In the following task you test if the inbound connection for your Direct Routing configuration works.

1. You are still signed in to CLIENT01 as “Lab User” with the password provided to you.

2. In the softphone, using the dial pad, call **14255551234**.

3. Answer the call using the Teams client and verify the call has connected.

4. Switch to the softphone and hang up the call.

You have successfully verified that your Teams users can receive calls.

### Task 4 - Review calls in the AudioCodes SBC

In the following task you will check the SBC logs to find the calls you used to test functionality and review them.

1. You are still signed in to CLIENT01 as “Lab User” with the password provided to you.

2. In Microsoft Edge, browse to **http://192.168.0.200/AdminPage**.

3. Sign in as **Admin** with password **Admin**.

4. On the AudioCodes page, at the top, select **MONITOR**.

5. In the left navigation, select **VOIP STATUS** > **SBC CDR HISTORY**.

6. In the table, review the incoming and outgoing calls. Locate the calls from the Office 365 to the softphone.

7. After reviewing the logs, close the browser window, the Teams Desktop client and the softphone client.

You have successfully reviewed the call history for the calls you placed earlier in the exercise.

Continue with the next lab.
