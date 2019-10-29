## Reproduce Chromecast Receiver Crash with Service Workers
I have created this page to help out the people who are trying to fix the service worker bug on cast devices.
[https://bugs.chromium.org/p/chromium/issues/detail?id=1018902](https://bugs.chromium.org/p/chromium/issues/detail?id=1018902)

A lot of cast apps use the [Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API), mostly games for the chromecast.
In 2019 people started reported that service workers causes unknown crashes on many devices.

Chromecast (1st gen)    — **1.36.157768**  
Chromecast (2nd gen)    — **1.42.172094**  
Chromecast (Ultra)      — **1.42.172094**  
Chromecast (Android TV) — **1.36.154871**  
Chromecast (Android TV) — **1.36.140076**  

To reproduce or debug the crash please follow the following steps:

### 1. Register cast application
We need to register a custom cast application so we use our application ID to run our app.  
Visit [https://cast.google.com/publish/](https://cast.google.com/publish/) to register your application.  
![](https://i.imgur.com/HC9l6mV.png)  

Don't forget to register your chromecast device under the "Cast Receiver Devices" so it's whitelisted to use your unpublished application.  
![](https://i.imgur.com/Cxfo2Ww.png)  

### 2. Host files on https
Download both sender.html, receiver.html and sw.js from this repository.  
If you cannot host these files on a https enabled web server, you can do the following with nodejs.

Install the following node modules:  
[http-server](https://www.npmjs.com/package/http-server)  
[ngrok](https://www.npmjs.com/package/ngrok)  

Run the following commands:  
```
http-server -c-1 -p 8080 --cors
ngrok http 8080
```

### 3. Change receiver application url
Visit [https://cast.google.com/publish/](https://cast.google.com/publish/) and edit your application.  
Change the application url with your website or ngrok url we just created.  
![](https://i.imgur.com/zI0MP6K.png)  
You might want to restart your chromecast ( Remove power for 10 seconds ) to avoid caching.

### 4. Test your receiver
Change your application ID inside the sender.html.  
Navigate to http://localhost:8080/sender.html or ngrok endpoint and click the "Launch cast application" button.  

Enjoy the crash!

![](crash.gif)  
The above gif was running on cast firmware ***1.42.172094***

PS: It works in any other browser, just go to http://localhost:8080/receiver.html directly
