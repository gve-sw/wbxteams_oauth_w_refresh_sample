# Webex Teams oAuth with refresh sample

This sample shows how to use an Webex Integration (https://developer.webex.com/docs/integrations) to implement an oAuth flow with refresh tokens 
for Webex Teams. 
To show a complete example of authenticating and performing Webex REST API calls, the sample application allows a user to 
authenticate with Webex teams if they had not done so previously. If they have, it will look for a locally stored auth token and refresh it with 
the refresh token if needed. If the refresh token has also expired, it will launch the full oAuth flow from the beginning. 

Once the user is authenticated, it retrieves the most recent space with activity they belong to and from that it retrieves 
the most recent message and displays it in a generated HTML page alongside the name and id of the logged in user.  


## Contacts
* Gerardo Chaves

## Solution Components
* Webex Teams

## Coding Guides used
 
Downgrading the requests-oauthlib library to version 0.0.0 to avoid the OAuth error I was getting:
https://github.com/requests/requests-oauthlib/issues/324

Example Oauth with Webex Teams:
https://github.com/CiscoDevNet/webex-teams-auth-sample

Waltkthrough including how to refresh tokens:
https://developer.webex.com/blog/real-world-walkthrough-of-building-an-oauth-webex-integration

Refresh token example:
https://stackoverflow.com/questions/27771324/google-api-getting-credentials-from-refresh-token-with-oauth2client-client



## Installation/Configuration

Once you clone the repository, edit the .env file to fill out the following configuration variables:

**CLIENT_ID**     
Set this variable to the Client ID from your integration. See the [Webex Integrations](https://developer.webex.com/docs/integrations) documentation for more details.

**CLIENT_SECRET**
Set this variable to the Client Secret from your integration. See the [Webex Integrations](https://developer.webex.com/docs/integrations)  documentation for more details.

Also, in the main.py file, configure the following variable:

**PUBLIC_URL**
Set PUBLIC_URL to the URL where your instance of this Flask application will run. If you do not change the parameters 
of app.run() at the end of the main.py file, this should be the same value of 'http://0.0.0.0:5000' that is set by default 
in the sample code.  
NOTE: This URL does not actually have to map to a public IP address out on the internet. 


## Usage

    $ python main.py

Once the flask app is running, use a browser to go to value you used for PUBLIC_URL which will re-direct to a Webex Teams 
authentication page if the first time using it so you can log in using your Webex Teams account credentials. 

Once authenticated, you will be presented with the name and id of the logged in user alongside the latest message in the most recent Space that the 
logged in user belongs to which has had activity. 

Since the authentication and refresh tokens are stored locally in the **tokens.json** file, you can use the application without having to 
re-authenticate for as long as you want as long as you refresh any expired tokens at least once every 60 days. This refresh is done 
automatically when you try to use the application to access the main page with the Spaces dropdown, but you can also use 
the /refresh route to force refreshing of the token. 

NOTE: clear out the **tokens.json** file when you are done using the sample so they are not left insecured in the test server. 
When creating production code using this sample as a reference, be sure to store in a more secure manner and fully encrypted. 



### LICENSE

Provided under Cisco Sample Code License, for details see [LICENSE](LICENSE.md)

### CODE_OF_CONDUCT

Our code of conduct is available [here](CODE_OF_CONDUCT.md)

### CONTRIBUTING

See our contributing guidelines [here](CONTRIBUTING.md)

#### DISCLAIMER:
<b>Please note:</b> This script is meant for demo purposes only. All tools/ scripts in this repo are released for use "AS IS" without any warranties of any kind, including, but not limited to their installation, use, or performance. Any use of these scripts and tools is at your own risk. There is no guarantee that they have been through thorough testing in a comparable environment and we are not responsible for any damage or data loss incurred with their use.
You are responsible for reviewing and testing any scripts you run thoroughly before use in any non-testing environment.