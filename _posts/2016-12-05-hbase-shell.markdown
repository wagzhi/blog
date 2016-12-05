---
layout: post
title:  "HBase Shell Commands"
date:   2016-12-05 22:17:55 +0800
categories: hbase
---

## Create 
创建表命令
{% highlight scala %} 
create 'book' , 'info'
{% endhighlight %}

## Alter
修改表命令
```shell 
alter 'book' ,  {NAME=>'chapters',VERSIONS=>5}
```

## Put
添加、修改数据
```shell 
put 'book', '001_ISBN9781491941959','info:date', 12345678
put 'book', '001_ISBN9781491941959','info:author','Caleb Doxsey'
put 'book', '001_ISBN9781491941959','info:name','Introducing Go'

put 'book', '001_ISBN9781491941959','chapters:subject_001', 'Introduction'
put 'book', '001_ISBN9781491941959','chapters:subject_002', 'Getting Started'
put 'book', '001_ISBN9781491941959','chapters:subject_003', 'Types'
put 'book', '001_ISBN9781491941959','chapters:subject_004', 'Variables'


put 'book', '002_ISBN9781491940747','info:date', 12345679
put 'book', '002_ISBN9781491940747','info:author','Jon Manning,Paris Buttfield-Addison, Tim Nugent'
put 'book', '002_ISBN9781491940747','info:name','Learning Swift'

put 'book', '002_ISBN9781491940747','chapters:subject_001', 'Swift Basics'
put 'book', '002_ISBN9781491940747','chapters:subject_001', 'An OS X App'
put 'book', '002_ISBN9781491940747','chapters:subject_003', 'An IOS App'
put 'book', '002_ISBN9781491940747','chapters:subject_004', 'Extending Your App'


put 'book', '003_ISBN9781491915813','info:date', 12345680
put 'book', '003_ISBN9781491915813','info:author','Jean-Marc Spaggiari, Kevin O\'Dell'
put 'book', '003_ISBN9781491915813','info:name','Architecting HBase Applications'

put 'book', '003_ISBN9781491915813','chapters:subject_001', 'Introduction to Hbase'
put 'book', '003_ISBN9781491915813','chapters:subject_002', 'User Cases'
put 'book', '003_ISBN9781491915813','chapters:subject_003', 'Troubleshooting'
put 'book', '003_ISBN9781491915813','chapters:subject_004', 'Extending Your App'
put 'book','003_ISBN9781491915813' ,'chapters:content_001' ,'{"Content":"<html></html>"}'

```

## San
查询
PrefixFilter
ColumnPrefixFilter
FamilyFilter
QualifierFilter

```
scan 'book', {FILTER => " PrefixFilter ('001')", LIMITS=>2}

scan 'book', {FILTER => " (PrefixFilter ('00')) AND (FamilyFilter (=,'binary:info')) "}

scan 'book', {FILTER => "(PrefixFilter ('001')) AND (FamilyFilter (=,'binary:chapters')) AND(ColumnPrefixFilter ('subject'))"}

scan 'book', {FILTER => "(PrefixFilter ('003')) AND (FamilyFilter (=,'binary:chapters')) AND (QualifierFilter (>,'binary:subject_001'))"}

scan 'book', {FILTER => "(PrefixFilter ('003')) AND (FamilyFilter (=,'binary:chapters')) AND (QualifierFilter (>,'binary:subject_001')) AND (QualifierFilter (<=,'binary:subject_003'))"}

scan 'book', {FILTER => "ColumnRangeFilter ('subject_003', true, 'subject_003',false)"}

scan 'book', {FILTER => "(FamilyFilter (=,'binary:info')) OR (ColumnRangeFilter ('subject_001', true, 'subject_003',false))"}
```

## Truncate
 清空表数据
```shell
 truncate 'book'
```