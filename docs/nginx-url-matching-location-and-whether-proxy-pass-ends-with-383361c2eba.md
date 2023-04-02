# Nginx URL 匹配、位置以及 proxy_pass 是否以/结尾

> 原文：<https://javascript.plainenglish.io/nginx-url-matching-location-and-whether-proxy-pass-ends-with-383361c2eba?source=collection_archive---------17----------------------->

![](img/2539c5cabd47b245bcd4b816c06cfefb.png)

本文用来记录 nginx 和 proxy_pass 的位置是否以/结尾的匹配规则

## 1.位置

位置仅确定它是模糊匹配还是精确匹配

```
1) When there is no "/" at the end, location /abc/def can match the request of /abc/defghi, or match /abc/def/ghi......
2) When there is "/" at the end, the location /abc/def/ cannot match the request of /abc/defghi, it can only match the request of /abc/def/ghi exactly
```

## 2.代理 _ 通行证

```
1.When there is / at the end of the url in the proxy_pass configuration, the content of the original uri except the location matching expression will be spliced after the url in the proxy_pass

2.
```

访问网址:[**http://blog.com/proxy/login.html**](http://blog.com/proxy/login.html)

```
#Case 1
location /proxy/ {
 proxy_pass http://myblog.com:8000/;
}
# The final address of proxy_pass is: http://myblog.com:8000/login.html Because proxy_pass ends with / and represents an absolute path, no proxy matching the location will be added

#Case 2
location /proxy/ {
 proxy_pass http://myblog.com:8000;
}
#proxy_pass proxy to http://myblog.com:8000/proxy/login.html

#Case 3
location /proxy/ {
 proxy_pass http://myblog.com:8000/disquz/;
}
#proxy_pass proxy to http://myblog.com:8000/disquz/login.html

#Case 4
location /proxy/ {
 proxy_pass http://myblog.com:8000/disquz;
}
#proxy_pass proxy to http://myblog.com:8000/disquzlogin.html
```

## **总结:**

**当 proxy_pass 配置中的 url 末尾有/时**

```
1\. the content of the original uri except the location matching expression will be spliced after the url in the proxy_pass
```

**当 proxy_pass 配置中的 URL 末尾没有/时**

```
 1\. If the url does not contain a path, the original url is directly spliced after the url in proxy_pass
2\. If the url does not contain a path, the content of the original uri except the location matching expression is spliced after the url in proxy_pass
```

***更多内容看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ， [***领英***](https://www.linkedin.com/company/inplainenglish/) ***，***[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***，以及****[***不和***](https://discord.gg/GtDtUAvyhW) *对成长黑客感兴趣？检查出* [***电路***](https://circuit.ooo/) ***。******