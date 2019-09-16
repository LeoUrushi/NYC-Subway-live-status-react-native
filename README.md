# NYC-Subway-live-status-react-native
This is a working example of a React Native live status app for New York Subway. 


## New York Subway Live Status: 

New York’s Metropolitan Transportation Authority (MTA) does have a website where they provide API data feeds. However, their log-in and account management system are very tricky to navigate. I’ve never managed to get passed the initial log-in stage. If you’d like to try your luck, be my guest: 
https://datamine.mta.info/

Luckily, MTA also maintains another resource which requires no log-ins. The following page lists out live status of Subway lines in plain .txt format. It seems to be updated in real time. 
http://web.mta.info/status/serviceStatus.txt

The first couple of lines of this file looks like this as of this writing. 

````
…
<line>
<name>123</name>
    <status>PLANNED WORK</status>
    <text> … (some more text strings here that tells the nature of engineering work, location and other details)…</text>
    <Date>09/15/2019</Date>
    <Time> 5:45AM</Time>
  </line>
…
````

This is telling us the line 123 (the red one) is currently experiencing disruption due to a planned engineering work. And the structure of the file seems consistent i.e., there is another block that looks pretty much like this for the line 456, 7, ACE and so on. 
That means we can parse the text in this URL to manually find the status text for each line. You can use a combination of a few basic string manipulation commands of javascript to find strings that are observed after X number of characters after <name>123</name>. 
Repeat the process for <name>456</name> and you get the next one. It is a tedious string manipulation, but it does the job. 



## Making API requests: 
We are using react-native-axios to make multiple requests in one batch. This will allow us to pool the requests for all the Subway lines and execute at the same time. 

Follow the instruction here to install: 
https://www.npmjs.com/package/react-native-axios



## Styling: 
NY Subway lines are often depicted as big circles with line name in them. 
Here is how you draw a circle in React Native. 


````

circle: {
    width: 25,
    height: 25,	
    borderRadius: 25 / 2,
    backgroundColor: 'grey',
  },

````

The description text is either black (“GOOD SERVICE”) or orange (everything else). The conditional styling is done like this: 


````
{color:  text01 == "GOOD SERVICE" ? 'black' : 'orange'}
````


For official colour palette of MTA Subway lines, see the link below. 
http://web.mta.info/developers/resources/line_colors.htm



The result should look like this: 
![Image description]( https://github.com/LeoUrushi/assets/blob/master/Screen_NewYorkSubwayAPI_sample.png)



Editable example: 
https://snack.expo.io/@leourushi/api-demo_ny-subway

Working example: 
https://apps.apple.com/us/app/new-york-subway-map/id1463337846











