---
layout: page
title: About
description: 明天会更好
keywords: swety
comments: true
menu: 关于
permalink: /about/
---

**我是SwetyCore**

此页面正在建设ing...





## 兴趣

{% for skill in site.data.skills %}
### {{ skill.name }}
<div class="btn-inline">
{% for keyword in skill.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}
