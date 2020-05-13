# Site24x7
Site24x7 by Zoho provides an array of monitoring capabilities including cloud, server and app monitoring; global speed and availability checks for websites, APIs, mail servers; etc. This xM Labs Integration allows you to connect one or more Site24x7 monitor to an xMatters On Demand instance to showcase the ease of passing alerts to xMatters.

Check out the video:

[![Intro video by Site24x7](https://img.youtube.com/vi/YG7_1T4aP44/0.jpg)](https://www.youtube.com/watch?v=YG7_1T4aP44)


---------

<kbd>
<a href="https://support.xmatters.com/hc/en-us/community/topics">
   <img src="https://github.com/xmatters/xMatters-Labs/raw/master/media/disclaimer.png">
</a>
</kbd>

---------


# Pre-Requisites
* Site24x7 account (https://www.site24x7.com/) or willingness to create a trial account
* xMatters account

# Files
* [Site24x7.zip](Site24x7.zip) - The Workflow

# Installation

## xMatters set up

1. Load in the [Site24x7.zip](Site24x7.zip) Workflow
2. Review the Form's (Site24x7 monitor) configuration - add a default group or user in the recipients section. Alternatively, create a [Subscription Form](https://help.xmatters.com/OnDemand/xmodwelcome/communicationplanbuilder/subscriptionforms.htm?cshid=SubscriptionFormListPlace) to allow users to subscribe to Site24x7 events. 
3. In the Integration Builder, look up the URL for the inbound integration "24x7 inbound"

## Application (Site24x7) set up

1. If you already have a monitor defined in Site24x7, skip to step 5, otherwise continue with step 2
2.  Go to Monitors and click ADD MONITOR, pick a monitor type (for the purposes of this recipe, chose "Website")
3. Give the new monitor a Display Name (for example "BBC"); fill in the Webpage URL you want to monitor (e.g. http://www.bbc.com/); set the "Accepted HTTP status codes" to 200; accept the defaults for the rest of the options; and save the monitor
4. Site24x7 will suggest a bunch of extra things to monitor about the website (page load time, DNS, etc.) but we don't need them, so click "Cancel" to adding them
5. Go to "Third Party Integration" in the main menu, click "Add Third Party Integration", and choose "Webhooks"
6. Give the integration a name, for example "xMatters"
7. Add in the Integration URL from the Comm Plan's Inbound Integration
8. Select POST Method
9. Make sure both "Post as JSON" and "Send Incident Parameters" are selected
10. For Authentication Method, pick "Basic / NTLM" and supply the user name and password for the xMatters user corresponding to the inbound integration URL
11. For "Integration level" you can specify "All Monitors" to have all alerts be sent to xMatters, or just "Monitors" if you only want to send some of your 24x7 monitors' alerts to xMatters (you can then pick them in the next control that shows up in the UI)
12. Save the Third Party Integration definition
13. The integration also uses Site24x7's API, so we need to get your authorization token into the commplan in xMatters:
14. Obtain an authtoken by logging in to your Site24x7 account and then go to this URL: https://accounts.zoho.com/apiauthtoken/create?SCOPE=Site24x7/site24x7api
15. Put the token value into the constant "Zoho Authorization" defined in the plan. The constant should look something like this: "Zoho-authtoken 41e2249adce96840c70fea19cd26cd38"
   
# Testing
1. To test, create an error situation that will trigger your monitor in Site24x7. For example for the Website type monitor, you can edit the monitor definition to look for a URL you know doesn't exist, e.g. http://www.bbc.com123).
2. Your monitor will switch to an error state within a few minutes (or less if your monitor has a short value for "check frequency"), and the third party integration should fire sending the monitor alert to xMatters (where you can monitor the IB Activity Stream or Reports tab to see what's happening, or not happening).
3. You can test the response option to Suspend Site24x7 Monitor and see that the monitor switches to a suspended state. Reactivate it by clicking "Activate" in the Site24x7 UI.
4. You can remove the error condition (e.g. change the URL back) and Site24x7 will send another integration request to xMatters, which will see that it's for the same monitor which is now in a good state ("UP"), so it will terminate the xMatters event.

# Troubleshooting
If no event is created in xMatters, go to the inbound integration's Activity Stream and check that there was a recent request from Site24x7. You might find an authorization error which indicates either an error in the credentials copied over to the Site24x7 Third Party Integration, or a permissions issue in xMatters (for example that the indicated user doesn't have sender permissions to the form).

If the activity stream does not contain errors, check to see if an event was created and check the event log for more details.
