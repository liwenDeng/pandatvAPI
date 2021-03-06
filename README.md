Table of Contents
=================

  * [Table of Contents](#table-of-contents)
  * [PandatvAPI](#pandatvapi)
    * [Requests](#requests)
      * [Retrive frontpage'ish channels](#retrive-frontpageish-channels)
      * [Retrive channels from all categories](#retrive-channels-from-all-categories)
      * [Retrive channels from a category](#retrive-channels-from-a-category)
      * [Retrive game categories](#retrive-game-categories)
      * [Get channel info](#get-channel-info)
      * [Search on roomid](#search-on-roomid)
      * [Get account info](#get-account-info)
      * [Get stream](#get-stream)


#Unofficial PandatvAPI

##Requests

###Retrive frontpage'ish channels 首页数据
Returns two lists containing channels data.

adsdata - List with premium/paid channels(?)

hotdata - Lists the channels with most views

```
http://static.api.m.panda.tv/android_hd/androidhdindex.json
```
[Sample output](/jsonsample/androidhdindex.json)

###Retrive channels from all categories
Returns a list with 10 channels

Field  |Description
----|----
pageno   | Page number. eg. pageno=1 will return first 10 and pageno=2 will return the next batch of 10.

```
http://static.api.m.panda.tv/android_hd/alllist_.json?pageno=1
```
[Sample output](/jsonsample/alllist_.json)

###Retrive channels from a category
Returns a list with 10 channels from a category.

Field  |Description
----|----
cate   | Game category. You can use "ename" from [cate.json](#retrive-game-categories)
pageno   | Page number. eg. pageno=1 will return first 10 and pageno=2 will return the next batch of 10.

```
http://static.api.m.panda.tv/android_hd/catelist_.json?cate=yzdr&pageno=1
```
[Sample output](/jsonsample/catelist_.json)

Another way:

Field  |Description
----|----
cate   | Game category. You can use "ename" from [cate.json](#retrive-game-categories)
pageno   | Page number. eg. pageno=1 will return first 10 and pageno=2 will return the next batch of 10.
pagenum  | Number of channels to retrive
__plat| (android, android_hd, pc_web)
__version| "1.0.1.1303" from client

```
http://api.m.panda.tv/ajax_get_live_list_by_cate?cate=dota2&pageno=1&pagenum=4&__version=1.0.1.1303&__plat=android_hd
```
[Sample output](/jsonsample/ajax_get_live_list_by_cate.json)

###Retrive game categories 栏目分类列表
```
http://static.api.m.panda.tv/android_hd/cate.json
```
[Sample output](/jsonsample/cate.json)

Another way:

Same as cate.json + one extra category "cartoon". Might return different things depending on version and platform.

Field  |Description
----|----
__plat| (android, android_hd, pc_web)
__version| "1.0.1.1303" from client
```
http://api.m.panda.tv/ajax_get_all_subcate
```
[Sample output](/jsonsample/ajax_get_all_subcate.json)

###Get channel info
Note: Seems like this response breaks the json RFC 4627 format. (At "details")

Field  |Description
----|----
roomid| Unique id. Same number in the url (eg. panda.tv/3331). Refered as "id" or "roomid" in the responses.
```
http://www.panda.tv/api_room?roomid=3331
```
[Sample output](/jsonsample/api_room.json)

Another way:

Field  |Description
----|----
roomid| Unique id. Same number in the url (eg. panda.tv/3331). Refered as "id" or "roomid" in the responses.
method| (?)
__plat| (android, android_hd, pc_web)
__version| "1.0.1.1303" from client
```
http://room.api.m.panda.tv/index.php?method=room.getinfo&roomid=3331&__plat=android_hd&&__version=1.0.1.1303
```
[Sample output](/jsonsample/getinfo_room.json)

###Search on roomid
Field  |Description
----|----
roomid| Unique id. Same number in the url (eg. panda.tv/3331). Refered as "id" or "roomid" in the responses.
```
http://api.m.panda.tv/ajax_search?roomid=3331
```
[Sample output](/jsonsample/ajax_search.json)

###Get account info

Field  |Description
----|----
option | Get option value (bamboos, .. (?) )
2Cishost|Check if you are host over given roomid
2Cisbanned| -
2Cexp| -
roomid| Unique id. Same number in the url (eg. panda.tv/3331). Refered as "id" or "roomid" in the responses.
```
http://www.panda.tv/ajax_get_myinfo?option=bamboos%2Cishost%2Cisbanned%2Cexp&roomid=3331
```
[Sample output](/jsonsample/ajax_get_myinfo.json)

###Get stream
Field  |Description
----|----
plflag| Can be obtained through [the channel info](#get-channel-info)(if for example "2_3" then you are interested in the 3 for stream)
room_key| Can be obtained through [the channel info](#get-channel-info)

```
http://pl[plflag].live.panda.tv/live_panda/[room_key].flv
http://pl3.live.panda.tv/live_panda/3331.flv
```

m3u8 files to ts streams

Field  |Description
----|----
plflag| Can be obtained through [the channel info](#get-channel-info)(if for example "2_3" then you are interested in the 3 for stream)
room_key| Can be obtained through [the channel info](#get-channel-info)
```
http://pl-hls[plflag].live.panda.tv/live_panda/[room_key].m3u8
http://pl-hls11.live.panda.tv/live_panda/81b481611b4bce2518657eceb52612bc.m3u8
```
