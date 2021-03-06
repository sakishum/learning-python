## 爬取历年排列三的中奖号码

### Requirements
* python 2.7
* BeautifulSoup4
* pandas 0.16.2
* matplotlib 1.4.3

### 介绍
* 第一次运行程序，会爬取所有期数的中奖号码，存入数据库。以后再次运行程序，程序首先判断是否存在数据库文件，如果存在，则找出上一次插入的最大期数，然后补插后面新出的中奖号码
```python
try:
    self.cursor.execute('SELECT max(id) FROM lottery')
    self.max_id_inserted = self.cursor.fetchall()[0][0]
except:
    self.cursor.execute(create_table)
    self.max_id_inserted = None
```

* 分析中奖号码  
  每一期的中奖号码为三个0-9的数字，统计每一期中奖号码的和值，应该符合正态分布，的确如此：
![normal distribution](http://i.imgur.com/wrZgWqx.jpg "正态分布")

  统计0-9出现的次数，如下图：

  ![等概率事件](http://i.imgur.com/0nqP72C.jpg)

  出现次数最少的是1，最多的是4，总体上还是符合理论的。
* 根据需求，筛选出最近n期的中奖号码，并以表格的形式打印出来
```	
最近10期的中奖号码：
    期号    百位  十位  个位 
+---------------------------+
|  16214  |  8  |  2  |  8  |
+---------------------------+
|  16213  |  6  |  5  |  8  |
+---------------------------+
|  16212  |  6  |  9  |  3  |
+---------------------------+
|  16211  |  4  |  6  |  3  |
+---------------------------+
|  16210  |  3  |  0  |  5  |
+---------------------------+
|  16209  |  2  |  9  |  9  |
+---------------------------+
|  16208  |  2  |  8  |  4  |
+---------------------------+
|  16207  |  7  |  7  |  5  |
+---------------------------+
|  16206  |  7  |  8  |  8  |
+---------------------------+
|  16205  |  4  |  3  |  5  |
+---------------------------+
```