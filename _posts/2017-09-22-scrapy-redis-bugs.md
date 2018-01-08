---
layout	:	post
title	:	分布式爬虫–scrapy-redis使用
---

## 1.AttributeError: ‘list’ object has no attribute ‘iteritems’

文件：settings.py

*ITEM_PIPELINES = [
‘scrapy_redis.pipelines.RedisPipeline’,
]*
改为
*ITEM_PIPELINES = {
‘scrapy_redis.pipelines.RedisPipeline’:300
}*
## 2.ValueError: (“Failed to instantiate dupefilter class ‘%s’: %s”, ‘scrapy.dupefilters.RFPDupeFilter’, TypeError(“__init__() got an unexpected keyword argument ‘key'”,))
文件：settings.py
添加 *DUPEFILTER_CLASS = “scrapy_redis.dupefilter.RFPDupeFilter”*

使用说明：<https://github.com/younghz/scrapy-redis>
