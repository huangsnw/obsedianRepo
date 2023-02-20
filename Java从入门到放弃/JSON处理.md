# JSON转List
```java
// HttpRequest 用的是 hutool 
respBody1 = HttpRequest.get("https://" + accessToken.getIpaddr() + ":" + accessToken.getPort() + "/device/channelDevInfo") .cookie(TokenBuilder.tokenHashmap.get("token")) .setConnectionTimeout(600) .execute().body(); 
log.info("responseBody转化为List<ChannelDevInfo>"); 

// JSONObject 用的是 fastjson 
JSONObject json = (JSONObject) JSON.parseObject(respBody1).get("channelDevList"); 
JSONArray jsonObject = json.getJSONArray("channelDevInfo"); 
List<ChannelDevInfo> list = JSONObject.parseArray(jsonObject.toJSONString(), ChannelDevInfo.class);
```