---
layout:     post
title:      "NSURL"
subtitle:   "NSURL"
date:       2018-03-09
author:     "WTJ"
header-img: "img/post-bg-js-module.jpg"
catalog: true
tags:
    - 网页

---

## URL 格式

```
                    hierarchical part
        ┌───────────────────┴─────────────────────┐
                    authority               path
        ┌───────────────┴───────────────┐┌───┴────┐
  abc://username:password@example.com:123/path/data?key=value&key2=value2#fragid1
  └┬┘   └───────┬───────┘ └────┬────┘ └┬┘           └─────────┬─────────┘ └──┬──┘
scheme  user information     host     port                  query         fragment

  urn:example:mammal:monotreme:echidna
  └┬┘ └────────────┬───────────────┘
scheme              path

```



NSURL 根据 [RFC 2396](https://link.jianshu.com?t=http://www.ietf.org/rfc/rfc2396.txt) 的定义提供了只读属性用于获取 URL 每一部分的值：

- scheme，协议名，不带有连接内容的冒号，如“http”。
- user，解码后的用户名。
- password，解码后的 password。
- host，主机域名或 IP 地址。
- port ，端口号。
- path，authority(user，password，host，port)后的部分，如果 URL 对象是 file URL，该属性会去掉最后的/。
- query，解码后的 query 字符串，没有?，但包括连接多个键值对的&。
- fragment，解码后的片段，不包括#。
- parameterString，path 后由分号分隔的部分，如`file:///path/to/file;foo`中的 foo。
- lastPathComponent，path 部分的最后一段。
- pathExtension，path 指向资源的扩展名。
- pathComponents，由解码后的 path 各段组成的数组。
- resourceSpecifier，冒号后的全部内容。
- absoluteString，将 URL string 和相对的 Base URL 拼接成的完整 URL string。
- absoluteURL，返回一个 NSURL 对象，将 absoluteString 作为该 URL 对象的 string。
- baseURL，如果 URL 对象本身由完整 URL 字符串构成，那么该属性为 nil。
- relativeString，URL 对象的相对部分，即创建时传入的字符串部分。
- relativePath，只包含相对字符串中的 path，而不包括 Base URL 中的。
- standardizedURL，删除掉 path 中的.和..的新的 URL 对象。
- fileSystemRepresentation，c string 表示的文件资源路径。



### 参考：

​	1、[[iOS-Foundation] NSURL](https://www.jianshu.com/p/38f5f53dfbad)

