# OSINT Challenge - Fall of 2022  

## Challenge Description  

*"It was a peaceful time — schools were over, college admissions were delayed, and COVID was slowly on the decline. It seemed like the perfect time to relax and check my phone for her txts.*  

*The funny thing is, I never got any. So I considered it just another gloomy year.*  

*Anyways, here’s the domain for this CTF: **acectf.tech***  

*What? You already knew this domain? Oh, I guess you’ll have no trouble finding the flag then.*  

**Good Luck!**  

## Solution Approach  

The key hint in this challenge is the phrase **"check my phone for her txts"**, which suggests looking into **TXT records** of the given domain: `acectf.tech`.  

### Step 1: Query DNS TXT Records  

DNS **TXT (Text) records** often contain additional metadata, which can sometimes be used for challenges like this. We can retrieve these records using the **dig** command:  


```dig TXT acectf.tech +short```

### Step 2: Extract the Flag
Running the above command will return the TXT record, which contains the flag for this challenge.
