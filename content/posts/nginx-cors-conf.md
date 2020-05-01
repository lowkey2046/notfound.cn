---
title: "Nginx CORS 配置"
date: 2020-05-01T12:23:24+08:00
tags: ["nginx", "cors"]
draft: true
---

```nginx wrap
add_header 'Access-Control-Allow-Origin' '*';
add_header 'Access-Control-Allow-Methods' 'GET,POST,OPTIONS';
add_header 'Access-Control-Allow-Headers' 'Authorization,Content-Type,Accept,Origin,User-Agent,DNT,Cache-Control,X-Mx-ReqToken,X-Requested-With';

if ($request_method = 'OPTIONS') {
	return 204;
}
```

## 参考

- [跨域资源共享 CORS 详解](https://www.ruanyifeng.com/blog/2016/04/cors.html)
- [HTTP访问控制（CORS）](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS)
- [nginx 配置add_header 'Access-Control-Allow-Origin' '*' 依然存在跨域问题](https://blog.csdn.net/xiojing825/article/details/83383524)
- [CORS on Nginx](https://enable-cors.org/server_nginx.html)
