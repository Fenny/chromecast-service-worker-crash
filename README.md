## Reproduce Chromecast Receiver Crash with Service Workers
I have created this page to help out the people who are trying to fix the service worker bug on cast devices.
[https://bugs.chromium.org/p/chromium/issues/detail?id=1018902](https://bugs.chromium.org/p/chromium/issues/detail?id=1018902)

Service workers worked before, people used them in custom cast apps ( mostly games ).
But more people reported that service workers causes unknown crashes on many devices.
We can confirm that the following firmwares crash on calling service workers:

Chromecast (1st gen)    — **1.36.157768**
Chromecast (2nd gen)    — **1.42.172094**
Chromecast (Ultra)      — **1.42.172094**
Chromecast (Android TV) — **1.36.154871**
Chromecast (Android TV) — **1.36.140076**

To reproduce or debug the crash please follow the following steps:

### 1. Register cast application
We need to register a custom cast application so we use our application ID to run our app.
Visit [https://cast.google.com/publish/](https://cast.google.com/publish/) to register 
