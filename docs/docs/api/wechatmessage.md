# WechatMessage API

目前此开发包提供以下几种消息类：``TextMessage`` (文本消息类), ``ImageMessage`` (图片消息类), ``VideoMessage`` (视频消息类), ``LocationMessage`` (位置消息类), ``LinkMessage`` (链接消息类), ``EventMessage`` (事件消息类), ``VoiceMessage`` (语音消息类)，它们都继承自 ``WechatMessage`` (公共消息类)

这些消息类都在 ``wechat_sdk.messages`` 中定义。

## WechatMessage 公共基类

下面所有的消息类均有此处的公共属性

|name|value|
|----|-----|
|`id`|消息ID|
|`target`|目标用户 OpenID|
|`source`|来源用户 OpenID|
|`time`|信息发送时间，一个UNIX时间戳|
|`raw`|信息的原始 XML 格式|

## 文本消息类 TextMessage

|name|value|
|----|-----|
|`type`|'text'|
|`content`|信息的内容|

## 图片消息类 ImageMessage

|name|value|
|----|-----|
|`type`|'image'|
|`picurl`|图片网址，可以从这个网址访问到图片|

## 视频消息类 VideoMessage

|name|value|
|----|-----|
|`type`|'video'|
|`media_id`|视频消息媒体 ID|
|`thumb_media_id`|视频消息缩略图的媒体 ID|

## 小视频消息类 ShortVideoMessage

|name|value|
|----|-----|
|`type`|'shortvideo'|
|`media_id`|视频消息媒体 ID|
|`thumb_media_id`|视频消息缩略图的媒体 ID|

## 链接消息类 LinkMessage

|name|value|
|----|-----|
|`type`|'link'|
|`title`|消息标题|
|`description`|消息描述|
|`url`|消息链接|

## 地理位置消息类 LocationMessage

|name|value|
|----|-----|
|`type`|'location'|
|`location`|一个元组(纬度, 经度)|
|`scale`|地图缩放大小|
|`label`|地理位置信息|

## 语音消息类 VoiceMessage

|name|value|
|----|-----|
|`type`|'voice'|
|`media_id`|语音消息媒体 ID|
|`format`|声音格式|
|`recognition`|语音识别结果(如未开通语音识别功能，则值为 `None` )|

## 事件消息类 EventMessage

### 关注事件

|name|value|
|----|-----|
|`type`|'subscribe'|
|`key`|`None`|
|`ticket`|`None`|

请注意，普通的关注事件和扫描二维码造成的关注事件的 type 均为 `subscribe` ，如果是普通的关注事件，则 `key` 和 `ticket` 均为 `None` ，可以通过判断它们来识别是普通关注事件还是扫描二维码造成的关注事件。

### 取消关注事件

|name|value|
|----|-----|
|`type`|'unsubscribe'|

### 二维码事件

|name|value|
|----|-----|
|`type`|'subscribe' 或 'scan'|
|`key`|事件 key 值<br/>当用户未关注时(type = 'subscribe')，qrscene_为前缀，后面为二维码的参数值；<br/>当用户已关注时(type = 'scan')，是一个32位无符号整数，即创建二维码时的二维码scene_id|
|`ticket`|二维码 Ticket，可用来换取二维码图片|

### 上报地理位置事件

|name|value|
|----|-----|
|`type`|'location'|
|`latitude`|地理位置纬度|
|`longitude	`|地理位置经度|
|`precision	`|地理位置精度|

### 自定义菜单事件

|name|value|
|----|-----|
|`type`|'click'<br/>'view'<br/>'scancode_push'<br/>'scancode_waitmsg'<br/>'pic_sysphoto'<br/>'pic_photo_or_album'<br/>'pic_weixin'<br/>'location_select'<br/>|
|`key`|事件 key 值<br/>当 type = 'click' 时，它与自定义菜单接口中KEY值对应；<br/>当 type = 'view' 时，它是设置的跳转URL<br/>当 type 为其他取值时，它是事件KEY值，由开发者在创建菜单时设定|
|`ScanCodeInfo`|扫描信息，当且仅当 type = 'scancode_push' 或 'scancode_waitmsg' 时存在|
|`SendPicsInfo`|发送的图片信息，当且仅当 type = 'pic_sysphoto' 或 'pic_photo_or_album' 或 'pic_weixin' 时存在|
|`SendLocationInfo`|发送的位置信息，当且仅当 type = 'location_select' 时存在|

### 模板消息事件

|name|value|
|----|-----|
|`type`|'templatesendjobfinish'|
|`status`|发送状态|

