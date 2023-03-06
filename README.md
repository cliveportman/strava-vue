# strava

Visit this page to authorize with your Strava account. Change the client_id if using a different app
[https://www.strava.com/oauth/authorize?client_id=17771&response_type=code&redirect_uri=http://localhost/exchange_token&approval_prompt=force&scope=read]

The resulting page will be an error. Ignore that and get the code from the URL.

Using Postman, make a POST request using:
https://www.strava.com/oauth/token?client_id=17771&client_secret=[client_secret from the app settings]&code=[code from the previous step]&grant_type=authorization_code

That will return an access_token as part of the response.
Use that within App.Vue to make the requests.


https://www.strava.com/oauth/token?client_id=17771&client_secret=5828df4ff9eda72dd55e58769fcc4ce988ca9afe&code=7317a8ef0f15cd0818a0cc98814509d553a954b6&grant_type=authorization_code
