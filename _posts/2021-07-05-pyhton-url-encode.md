---
layout: post
title: Python url Encode
subheading: url에 한글 혹은 공백 사용시
author: limdongkyu
categories: python
banner:
video: https://vjs.zencdn.net/v/oceans.mp4
loop: true
volume: 0.8
start_at: 8.5
image: https://bit.ly/3xTmdUP
opacity: 0.618
background: "#000"
height: "100vh"
min_height: "38vh"
heading_style: "font-size: 4.25em; font-weight: bold; text-decoration: underline"
subheading_style: "color: gold"
tags: python
sidebar: []
---

가끔 url 만들 때 파일명의 공백이나 args 에 한글로 인해 삽질할때 사용되어 진다.

## section 1

### example for python


```python
from urllib.parse import urlsplit, quote, urlparse, parse_qs, urlencode
from urllib.request import Request, urlopen

url = 'https://limdongkyu.github.io/api/test?name=브라이언&greet=하잉~'
url_info = urlsplit(url)
print(url_info)

encoded_url = f'{url_info.scheme}://{url_info.netloc}{quote(url_info.path)}'
print(encoded_url)

if url_info.query:
    enc_params = list(map(lambda item: (item[0], quote(item[1][0])), parse_qs(url_info.query).items()))
    encoded_url = f'{encoded_url}?{urlencode(enc_params)}'

req = Request(encoded_url, headers={'User-Agent': 'Mozilla/5.0'})
res = urlopen(req)
if res.status == 200:
    print('성공')
else:
    print(f'실패코드 {res.status}')
```
