---
layout:     post
title:      "Python的lxml库的使用"
date:       2021-03-26 12:00:00
author:     "swetycore"
tags:
    - Python
---

# 前言：
在开发自动健康打卡的过程中，因为post不止提交有当日体温，还带有最近动态等个人信息，最初是用json文件来存储信息，但是这样每次信息更新都要重新手动更新json文件很不方便，而且只能自己一个人用。

# 用法：
<small>这里贴上一个我当时看的教程连接：[>点我传送<](https://www.w3school.com.cn/xml/index.asp)</small>
+ 需要提取的信息大致分为以下这几类  
 1.input/number类型：`<input id="ykt" class="weui_input" type="text" name="ykt" placeholder="请输入学号" value="1234567890" readonly="readonly"> </div>`   
  `<input class="weui_input" type="number" id="nl" name="nl" placeholder="请输入年龄" maxlength="3" required="" value="18">`   
  2.radio类型： `<input class="weui-check" name="xb" type="radio" disabled="disabled" value="女">&nbsp;女Female</div>`  
  3.select_type：`<select id="qtyc" class="select_type" name="qtyc"><option value="" selected="selected"></option><option value="无">无 None</option><option value="不发烧但咳嗽">不发烧但咳嗽 No fever but cough</option><option value="不发烧但腹泻">不发烧但腹泻 No fever but diarrhea</option></select>`  
 + 解决方案  
   1.导入lxml  
   `from lxml import etree`  
   2.利用etree.HTML，将字符串解析为HTML文档
   `html = etree.HTML(text)`  
   3.xpath匹配  
    ```
    result=html.xpath('//input[@type="text"]')
    html.xpath('//input[@type="number"]')
    html.xpath('//input[@type="radio" and @checked="checked"]') # 多个属性匹配（类型是radio并且被选中）
    # 上面几个返回的是所有匹配到的结果【list】可以用for遍历。
   
    for i in result:
        key = i.xpath('./@name')[0]
        value = i.xpath('./@value')[0]
   
    这样就获取到了表单所需要的key和对应的value。
    下面是select_type的：
    selects = html.xpath('//select[@class="select_type"]')
        for select in selects:
            option = select.xpath('./option[@selected="true"]')[0]
   
            key = option.xpath('../@name')[0]
            value = option.xpath('./@value')[0]
    ```

至此，自动提取已经填过的表单项目的任务已经完成。
