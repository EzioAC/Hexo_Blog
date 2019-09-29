---
title: Oracle-如何区分dmp是由exp还是expdp导出的?
date: 2019-09-29 17:51:12
categories: Oracle # 分类只能有1个
tags: # 标签可以有多个
- Oracle
- 数据导入导出
---
区分dmp文件是来自exp还是expdp
<!-- more -->

# 区分dmp文件是来自exp还是expdp

## 使用语句:
```bash
xxd  -l 500 test1.dmp
```
>使用xxd查看dmp文件的编码
>用-l来限制长度
>less或more或vi也是可以查看的

![exp导出](/images/exp.png "exp")
如图为exp导出文件
文件开头为**0303**

---
![expdp导出](/images/expdp.png "expdp")
如图为expdp导出文件
文件开头为**0301**

---
>其实两者差别挺明显的(时间,字符编码,版本,导出用户,导出任务信息都有差异)
>爱怎么记怎么记 :P