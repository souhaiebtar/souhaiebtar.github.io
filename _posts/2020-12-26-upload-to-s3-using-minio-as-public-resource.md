---
layout: post
date: 2020-12-26 23:55:09
title: how to use pyton  minio library to upload file to s3 as public
description: >-
  a snippet about how to upload file to s3 using minio as public resource
main-class: 'tools'
color: '#7AAB13'
tags:
- tools
twitter_text: >-
  a snippet about how to upload file to s3 using minio as public resource
introduction: "a snippet about how to upload file to s3 using minio as public resource"
---

```python
minioClient.fput_object('photos', fileName, '/tmp/' + md5_hash, content_type=image.content_type, metadata={'x-amz-acl': 'public-read'})
```
