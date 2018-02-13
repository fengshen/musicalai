---
title: musicalai API Reference

includes:
  - errors

search: true
---

# Introduction

Welcome to the musicalai API!

# musicalai API 

Base URL http://54.183.117.137/

## Retrieve style list(获取歌曲风格列表)

This endpoint retrieves all styles supported.

### HTTP Request

`GET /data/style`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------

### Return JSON Format
see code on the right side.

```
    {
      'style': 'Sci-Fi',

      'style_cn': '科幻',

      'mood': 'Charming',

      'mood_cn': '迷人',

      'descriptor': 'sciFiCharming'
    }
```

## Compose music (创作歌曲) 

This endpoint compose a new song.


### HTTP Request

`POST /compose`

### URL Parameters

Parameter | Description
--------- | -----------
style | unique style id which is descriptor returned in /data/style request.
duration | length of the new composed music in seconds. (e.g. 50s)

### Return JSON Format
see code on the right side.

```
task = {

        'id': song_id, #unique id for each song

        'style_id':style,

        'percent' : '0', #progress of composing song

        'done': False

    }
```

## Retrieve song information (获取歌曲创作信息). 

This endpoint retrieve information about a specific song.

### HTTP Request

`GET /song/<song_id>`

### URL Parameters

Parameter | Description
--------- | -----------
song_id | The ID of the song to retrieve. 

### Return JSON content.
see code on the right.

```
### Return JSON if song is in process of composing.
        task = {
        'id': music_id, #unique id for each song
        'style_id':style,
        'percent' : '0', #progress of composing song
        'done': False
        }
```


```
### Return JSON if song is done composing.
        "task": {

          "done": True,

          "download_link": "http://54.183.117.137/download/2018-01-26_17:04:09.232480.mp3",

          "id": "2018-01-26_17:04:09.232480.mp3",

          "percent": "100",

          "style_id": "sciFiCyberpunk"

        }
```

## Download song (下载歌曲)
This endpoint downloads a specific song.

### HTTP Request

`GET /download/<song_id>`

### URL Parameters

Parameter | Description
--------- | -----------
song_id | The ID of the song to retrieve. 


<aside class="notice">
song_id is the 'id' returned from compose request or you can use the 'download_link' in returned JSON from song information request.
</aside>
