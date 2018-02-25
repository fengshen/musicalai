---
title: musical.ai API 参考 

includes:
  - errors

search: true
---

#简介

欢迎使用musical.ai API服务。您可以使用本文档介绍的API来生成音乐旋律。

#授权
在使用前，您需先申请密钥（API Key），同时请阅读并遵守musical.ai使用条款和用户授权许可协议。目前musical.ai API还在测试中，申请试用请发送邮件联系api@musical.ai。

# musicalai API 

基本URL http://54.183.117.137/

## 获取歌曲风格列表

获取音乐风格列表，包含中英文命名.

### HTTP 请求

`GET /data/style`

###请求代码示例.
curl -i http://54.183.117.137/data/style?apikey=your_api_key

### 回传JSON属性

属性 | 描述 
--------- | -------
style |	风格（英文）
style\_cn |	风格（中文）
mood |	情绪（英文）
mood\_cn |	情绪（中文）
descriptor |	此风格情绪下的唯一描述符
###代码示例.
{   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'style': 'Sci-Fi',    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'style_cn': '科幻',    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'mood': 'Charming',    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'mood_cn': '迷人',    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'descriptor': 'sciFiCharming'    
}   
## 创作音乐

创作特定风格与情绪的新音乐。


###HTTP请求

`POST /compose`

###请求代码示例.
curl -i -H "Content-Type: application/json" -X POST -d '{"style":"sciFiDark", "duration": "50"}' http://54.183.117.137/compose?apikey=your_api_key

###URL参数
 
参数 |	描述
--------- | -----------
style |	音乐创作的风格情绪，通过/data/style来获得其对应的描述符
duration |	音乐创作的长度，用秒作为单位

### 回传JSON属性
属性 |	描述
--------- | -----------
music_id |	创作音乐的唯一id
style\_id |	风格
percent |	音乐创作状态的百分比
done |	创作是否完成。True为完成，False为未完成

###代码示例.
{   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"done": false,     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"music_id": "2018-02-25_02:32:33.905653.mp3",     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"percent": "0",    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"style_id": "sciFiDark"   
}   

##获取音乐创作信息 

通过音乐id来获取音乐创作状态.

###HTTP请求

`GET /song/<music_id>`

###请求代码示例.
curl -i http://54.183.117.137/song/2018-02-25_03:17:55.841332.mp3?apikey=your_api_key

###URL参数

参数 |	描述
--------- | -----------
music\_id |	音乐的唯一id

###回传JSON属性
属性 |	描述
--------- | -----------
music_id |	音乐唯一id
style\_id |	风格情绪的类型
percent |	音乐创作状态的百分比
done |	创作是否完成。True为完成，False为未完成
download\_link |	下载链接

###代码示例.

### 创作未完成:
{                                                                                                                                                               
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"done": true,     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"music_id": "2018-02-25_03:17:55.841332.mp3",     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"percent": "10",    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"style_id": "sciFiDark"     
}    

### 创作完成:
{     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"done": true,     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"download_link": "http://54.183.117.137/download/2018-02-25_03:17:55.841332.mp3",     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"music_id": "2018-02-25_03:17:55.841332.mp3",     
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"percent": "100",    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"style_id": "sciFiDark"     
}    

##下载歌曲
下载特定歌曲.

### HTTP Request

`GET /download/<music_id>`

###请求代码示例.
curl -O http://54.183.117.137/download/2018-02-25_03:17:55.841332.mp3?apikey=your_api_key

###URL参数

参数 |	描述
--------- | -----------
music\_id	| 音乐的唯一id

<aside class="notice">
也可直接使用音乐状态查询中的下载链接.
</aside>
