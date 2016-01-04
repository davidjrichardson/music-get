# music-get

One of the (many) music server implementations for UWCS. While the other options out there may be shinier, music-get is intended to be an easily maintainable alternative prioritising simplicity over extra features. Playing works on a round robin system - each bucket contains at most one item queued by a single IP.

##Documentation
See the [wiki](https://github.com/mcnutty26/music-get/wiki) for more information on how music-get works.

##Setup
* create config.ini in bin, and have it contain the admin password
* Create an apache virtualhost with the document root pointed at the music-get bin folder
* Add ```Header set Access-Control-Allow-Origin "*"``` to the apache virtualhost
* Run ```java -jar music-get.jar``` in bin
* If youtube downloading doesn't work, run ```./youtube-dl -U``` to get the latest version of youtube-dl

##API:
##### /list returns a JSON array representing the current queue 
```curl 127.0.0.1:8080/list```
##### /last returns a JSON array representing the played items in the current bucket
```curl 127.0.0.1:8080/last```
##### /current returns a string containing the name of the currently playing item
```curl 127.0.0.1:8080/current```
##### /add accepts a file via post and adds it to the queue
```curl -F "file=@/home/bob/path/to/file.mp3```
##### /url accepts a URL via post and attempts to download that file
```curl -F "url=https://www.youtube.com/watch?v=QcIy9NiNbmo"```
##### /downloading returns a JSON array representing the currently downloading videos from /url
```curl 127.0.0.1:8080/downloading```
##### /remove accepts a guid via post (from /list) and removes that guid from the queue if the requesting ip queued that item
```curl -F "guid=3c0a7a25-ffc5-4654-8e96-f8dc5dc70f5c" 127.0.0.1:8080/remove```
##### /admin/kill accepts a password via post and stops the currently playing item
```curl -F "pw=letmein123" 127.0.0.1:8080/admin/kill```
##### /admin/remove accepts a guid (from /list) and a password via post and removes that guid from the queue
```curl -F "guid=3c0a7a25-ffc5-4654-8e96-f8dc5dc70f5c" -F "pw=letmein123" 127.0.0.1:8080/admin/remove```
##Dependencies:
* Jetty (included in music-get.jar)
* JSON-java (included in music-get.jar)
* youtube-dl (included in music-get.jar)
* Java 8
* MPlayer
* Apache
* PHP
