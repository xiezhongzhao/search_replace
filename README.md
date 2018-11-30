### 将儿话音的文本转化为书面语程序模块
**任务简介: 对文本中儿话音分词进行定位,然后用书面语替换原来的儿话分词**
___

### 1. 算法的设计流程
#### 1.1 提取引号的内容
    对于文本中引号中的内容不予处理
#### 1.2 将引号内容加入结巴词典
    将引号内容加入结巴词典,避免将引号的内容进行分词
#### 1.3 将文本进行分词操作
    使用jieba将预处理完的文本,进行分词
#### 1.4 搜索带儿的分词
    搜索文本中带儿的所有分词
#### 1.5 读取带儿的非儿话词典
    读取文件voc2.txt,里面是带儿的分词,如'体育健儿','儿孙满堂'等分词
#### 1.6 剔除带儿分词中的非儿话字典中分词
    对带儿分词剔除引号中带儿的分词和非儿话词典中分词
#### 1.7 替换儿话分词的候选词
    用`ppl`选取替换儿话分词的替换词
#### 1.8 获得最终同义替换后的样本
    将所有需要替换的儿话分词进行替换后,输出替换后的文本,以及相应替换词和原始文本中所在位置
___

### 2. 运行环境
* Ubuntu 16.04LTS    
* Python 3.5.2    
* PPL     
* jieba    
___
### 3. 算法实现的效果
* 输入形式: 文本输入    
* 输出形式: 对儿话音同义替换后的文本,和原始文本中替换词以及它的位置      
* 代码示例:    
```
from Synonyms import erSynonyms
test_sent = input("请输入文本：")
strText, er_replace_index = erSynonyms(test_sent).text_synonyms()
print(strText)
print(er_replace_index)
```
* 输出
```
输入：卖的是酱油、火柴和烟卷儿、草纸、还有关东烟儿；
输出: 卖的是酱油、火柴和烟卷、草纸、还有关东烟草；
[('烟儿', 20, 21, '烟草')]

输入：昨儿天气很好，今儿要下雨，明儿又是好天气，交通方面儿比较理想； 
输出: 昨晚天气很好，今天要下雨，明天又是好天气，交通方面比较理想；
[('儿', 25, ''), ('昨儿', 0, 1, '昨晚'), ('明儿', 13, 14, '明天'), ('今儿', 7, 8, '今天')]

输入：2008年奥运健儿创辉煌，让中国站在世界舞台上；
输出: 2008年奥运健儿创辉煌，让中国站在世界舞台上；
[]

输入：删除带“儿”分词，冰糖葫芦一串儿又一串儿，瓜子儿还有酸杏干儿；
输出: 删除带“儿”分词，冰糖葫芦一串又一串，瓜子还有酸杏干；
[('儿', 15, ''), ('儿', 18, ''), ('儿', 27, '')]
```







