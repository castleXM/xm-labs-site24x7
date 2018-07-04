# Site24x7.com
Site24x7.com by Zoho.com provides an array of monitoring capabilities including cloud, server and app monitoring; global speed and availability checks for websites, APIs, mail servers; etc. This xM Labs Integration allows you to connect a Site24x7 monitor to an xMatters On Demand account to showcase the ease of passing alerts to xMatters.
They have a free level where they only support sending alerts through email, and a free month trial where all the integration options work.

Check out the video:

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/YG7_1T4aP44/0.jpg)](https://www.youtube.com/watch?v=YG7_1T4aP44)


---------

<kbd>
  <img src="https://github.com/xmatters/xMatters-Labs/raw/master/media/disclaimer.png">
</kbd>

---------


# Pre-Requisites
* Site24x7 account (https://www.site24x7.com/) or willingness to create a trial account
* xMatters account

# Files -- TO UPDATE
* [Site24x7.zip](Site24x7.zip) - The comm plan
* [media/Logz-io.mp4](Logz-io.mp4) - Video example of the integration in action

# Installation

## xMatters set up

1. Load in the [Site24x7.zip](Site24x7.zip) Comm Plan
2. Review the Form's (Site24x7 monitor) configuration - add a default group or user in the recipients section
3. In the Integration Builder, look up the URL for the inbound integration "24x7 inbound"

## Application (Site24x7) set up

1. If you don't yet have a monitor defined in Site24x7:
1b. Go to Monitors and click ADD MONITOR, pick a monitor type (for the purposes of this recipe, chose "Website")
1c. Give the new monitor a Display Name (for example "BBC") , fill in the Webpage URL you want to monitor (e.g. http://www.bbc.com/), set the "Accepted HTTP status codes" to 200, accept the defaults for the rest of the options, and save the monitor
1d. Site24x7 will suggest a bunch of extra things to monitor about the website (page load time, DNS, etc.) but we don't need them, so click "Cancel" to adding them
2. Go to "Third Party Integration" in the main menu, click "Add Third Party Integration", and choose "Webhooks"
3. Give the integration a name, for example "xMatters"
4. Add in the Integration URL from the Comm Plan's Inbound Integration
5. Select POST Method
6. Make sure both "Post as JSON" and "Send Incident Parameters" are selected
7. For Authentication Method, pick "Basic / NTLM" and supply the user name and password for the xMatters user corresponding to the inbound integration URL
8. For "Integration level" you can specify "All Monitors" to have all alerts be sent to xMatters, or just "Monitors" if you only want to send some of your 24x7 monitors' alerts to xMatters (you can then pick them in the next control that shows up in the UI)
9. Save the Third Party Integration definition
   
# Testing
To test, create an error situation that will trigger your monitor in Site24x7. For example for the Website type monitor, you can edit the monitor definition to look for a URL you know doesn't exist, e.g. http://www.bbc.com123).
Your monitor will switch to an error state within a few minutes (or less if your monitor has a short value for "check frequency"), and the third party integration should fire sending the monitor alert to xMatters (where you can monitor the IB Activity Stream or Reports tab to see what's happening, or not happening)

# Troubleshooting
If no event is created in xMatters, go to the inbound integration's Activity Stream and check that there was a recent request from Site24x7.

If the activity stream does not contain errors, check to see if an event was created and check the event log for more details.