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

An updated version of this integration is available, supporting the latest version of Site24x7 and based on xMatters Flow Designer so you can easily connect other tools to your toolchain. [Learn more](http://help.xmatters.com/integrations/#cshid=Site24x7).

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
3. In the Flow Designer, look up the URL for the HTTP Trigger "Inbound from site24x7"

## Application (Site24x7) set up

1. If you already have a monitor defined in Site24x7, skip to step 5, otherwise continue with step 2
2.  Go to Monitors and click ADD MONITOR, pick a monitor type (for the purposes of this recipe, chose "Website")
3. Give the new monitor a Display Name (for example "BBC"); fill in the Webpage URL you want to monitor (e.g. http://www.bbc.com/); set the "Accepted HTTP status codes" to 200; accept the defaults for the rest of the options; and save the monitor
4. Site24x7 will suggest a bunch of extra things to monitor about the website (page load time, DNS, etc.) but we don't need them, so click "Cancel" to adding them
5. Go to "Third Party Integration" in the admin menu, click "Add Third Party Integration", and choose "Webhooks"
6. Give the integration a name, for example "xMatters"
7. Add in the Integration URL from the Comm Plan's Inbound Integration
8. Select POST Method
9. Make sure both "Post as JSON" and "Send Incident Parameters" are selected
10. Optionally if you choose to use Basic Authentication, pick "Basic / NTLM" and supply the user name and password for the xMatters user corresponding to the inbound integration URL
11. For "Integration level" you can specify "All Monitors" to have all alerts be sent to xMatters, or just "Monitors" if you only want to send some of your 24x7 monitors' alerts to xMatters (you can then pick them in the next control that shows up in the UI)
12. Save the Third Party Integration definition
   
# Testing
Test by clicking the Test button on the integration. Check the Activity Log in Flow Designer if you are not alerted. Make sure to add recipients for the Event.

# Troubleshooting
If no event is created in xMatters, go to the Flow Designer's Activity Log and check that there was a recent request from Site24x7.

If the Activity Log does not contain errors, check to see if an event was created and check the event log for more details.
