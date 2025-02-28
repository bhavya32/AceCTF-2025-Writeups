```Go to login page

Intercept with burp suite you will be provided with jwt token as follows

eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoiZ3Vlc3QifQ.JT3l4_NkVbkQuZpl62b9h8NCZ3cTcypEGZ1lULWR47M

You will find this is for guest

Now we need a token with admin privilage and valid signature we can forge a dummy jwt token from above

Now use curl with the modified jwt```