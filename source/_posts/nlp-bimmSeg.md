---
title: 自然语言处理 | 双向匹配中文分词 Python
date: 2021-10-05 00:28:22
img: http://www.west999.com/cms/images/2019-01-17/eustx1iuj4h.png
categories: 
- 自然语言处理
tags:
- 双向匹配法
- Python
---

## 理论描述
中文分词是指中文在基本文法上有其特殊性而存在的分词。

## 算法描述
本文实现双向匹配算法，具体算法描述如下：

**正向最大算法**
设MaxLen表示最大词长，D为分词词典。
（1）从待切分语料中按正向取长度为MaxLen的字串str，令Len=MaxLen；
（2）把str与D中的词相匹配；
（3）若匹配成功，则认为该字串为词，指向待切分语料的指针向前移Len个汉字（字节），返回到（1）；
（4）若不成功：如果Len>1，则将Len减2，从待切分语料中取长度为Len的字串str，返回到（2）。否则，得到长度为2的单字词，指向待切分语料的指针向前移1个汉字，返回（1）。

**反向最大算法**
设MaxLen表示最大词长，D为分词词典。
（1）从待切分语料中按反向取长度为MaxLen的字串str，令Len=MaxLen；
（2）把str与D中的词相匹配；
（3）若匹配成功，则认为该字串为词，指向待切分语料的指针向前移Len个汉字（字节），返回到（1）；
（4）若不成功：如果Len>1，则将Len减2，从待切分语料中取长度为Len的字串str，返回到（2）。否则，得到长度为2的单字词，指向待切分语料的指针向前移1个汉字，返回（1）。

## 详例描述
以“对外经济技术合作与交流不断扩大。”为例，详细描述算法如下：

窗口大小设为4，句子长度为16。 

首先是正向匹配。sub_str = ‘对外经济’与词典进行匹配，匹配失败，窗口大小减一。
sub_str = ‘对外经’与词典进行匹配，匹配失败，窗口大小减一。
sub_str = ‘对外’与词典进行匹配，匹配成功，窗口大小恢复为4，向右移动之前匹配词的长度，此时sub_str = ‘经济技术’，将其添加至列表words中。重复上述步骤。
当匹配到最后一个词时，算法停止。
正向匹配结果如下：对外/ 经济/ 技术/ 合作/ 与/ 交流/ 不断/ 扩大/ 。/
反向匹配如法炮制，结果如下：对外/ 经济/ 技术/ 合作/ 与/ 交流/ 不断/ 扩大/ 。/
正向与反向匹配结果相同，返回任意一个。

## 实验要求

请使用双向匹配算法对给定测试文本进行分词:

给定测试文本为: 实验1作业测试文本.txt

词典为: ChineseDic.txt

要求:编程实现，并显示分词时间。


实验1作业测试文本.txt 内容如下：
```
切分前测试文本串：
在这一年中，中国的改革开放和现代化建设继续向前迈进。国民经济保持了“高增长、低通胀”的良好发展态势。农业生产再次获得好的收成，企业改革继续深化，人民生活进一步改善。对外经济技术合作与交流不断扩大。


切分后用于计算P,R,F值的文本串：
在/  这/  一/  年/  中/  ，/  中国/  的/  改革/  开放/  和/  现代化/  建设/  继续/  向前/  迈进/  。/  国民经济/  保持/  了/  “/  高/  增长/  、/  低/  通胀/  ”/  的/  良好/  发展/  态势/  。/  农业/  生产/  再次/  获得/  好/  的/  收成/  ，/  企业/  改革/  继续/  深化/  ，/  人民/  生活/  进一步/  改善/  。/  对外/  经济/  技术/  合作/  与/  交流/  不断/  扩大/  。/  
```

## 代码

```python
class Segment:
    # 数据成员
    sentence = ""
    MaxLen = 0
    pos = 0
    len = 0
    MMResult = ""
    RMMResult = ""
    biMMResult = ""
    dict = []

    # 构造函数
    def __init__(self, Sentence, MaxLen):
        self.sentence = Sentence
        self.MaxLen = MaxLen
        self.pos = 0
        self.len = self.MaxLen
        self.MMResult = ""
        self.RMMResult = ""
        self.biMMResult = ""
        self.readDict()

    # 读字典
    def readDict(self):
        f = open("chineseDic.txt", "r", encoding="utf-8")
        lines = f.readlines()
        for line in lines:
            # print(line)
            words = line.split(",")
            self.dict.append(words[0])

    # 正向匹配算法
    def MM(self, nLen, nPos):
        if nPos > len(self.sentence):
            return

        substr = self.sentence[nPos : nPos + nLen]
        if substr in self.dict:
            self.MMResult = self.MMResult + substr + "/ "
            nPos = nPos + nLen
            nLen = self.MaxLen
            self.MM(nLen, nPos)
        elif nLen > 1:
            nLen = nLen - 1
            self.MM(nLen, nPos)
        else:
            self.MMResult = self.MMResult + substr + "/ "
            nPos = nPos + 1
            nLen = self.MaxLen
            self.MM(nLen, nPos)

    # 反向匹配算法
    def RMM(self, nLen, nPos):
        if nPos <= nLen:
            nLen = nPos
        subStr = self.sentence[nPos - nLen:nPos]
        if subStr != '':
            if subStr in self.dict:
                if nPos == len(sentence):
                    self.RMMResult = "/ " + subStr + self.RMMResult + "/ "
                    nPos = nPos - nLen
                    nLen = self.MaxLen
                    self.RMM(nLen, nPos)
                elif nPos == nLen:
                    self.RMMResult = subStr + self.RMMResult
                    nPos = nPos - nLen
                    nLen = self.MaxLen
                    self.RMM(nLen, nPos)
                else:
                    self.RMMResult = "/ " + subStr + self.RMMResult
                    nPos = nPos - nLen
                    nLen = self.MaxLen
                    self.RMM(nLen, nPos)
            elif nLen > 1:
                nLen = nLen - 1
                self.RMM(nLen, nPos)
            else:
                self.RMMResult = "/ " + subStr + self.RMMResult
                nPos = nPos - 1
                nLen = self.MaxLen
                self.RMM(nLen, nPos)

    def getMMResult(self):
        return self.MMResult

    def getRMMResult(self):
        return self.RMMResult

    def getbiMMResult(self):
        if self.MMResult == self.RMMResult:
            self.biMMResult = self.MMResult
            return self.biMMResult
        else:
            return

# 主函数
if __name__ == '__main__':
    # sentence = "对外经济技术合作与交流不断扩大。"
    sentence = "在这一年中，中国的改革开放和现代化建设继续向前迈进。国民经济保持了“高增长、低通胀”的良好发展态势。农业生产再次获得好的收成，企业改革继续深化，人民生活进一步改善。对外经济技术合作与交流不断扩大。"
    seg = Segment(sentence, 4)

    seg.MM(4, 0)
    print("MM：")
    print(seg.getMMResult())
    print("")

    seg.RMM(4, len(sentence))
    print("RMM：")
    print(seg.getRMMResult())
    print("")

    print("biMM：")
    print(seg.getbiMMResult())
    print("")
```

但是老师PPT中对于双向匹配法的描述是：

对同一个字符串分别采用MM和RMM两种方法进行切分处理，如果能够得到相同的切分结果，则认为切分成功，否则认为有疑点。

但是我不知道有疑点的情况下如何判别，于是我在网上搜到了下面的方法：

---

本次实验内容是基于词典的双向匹配算法的中文分词算法的实现。使用正向和反向最大匹配算法对给定句子进行分词，对得到的结果进行比较，从而决定正确的分词方法。

## 算法描述
### 正向最大匹配算法
先设定扫描的窗口大小maxLen（最好是字典最长的单词长度），从左向右取待切分汉语句的maxLen个字符作为匹配字段。查找词典并进行匹配。若匹配成功，则将这个匹配字段作为一个词切分出来，并将窗口向右移动这个单词的长度。若匹配不成功，则将这个匹配字段的最后一个字去掉，剩下的字符串作为新的匹配字段，进行再次匹配，重复以上过程，直到切分出所有词为止。

### 反向最大匹配算法
该算法是正向的逆向算法，区别是窗口是从后向左扫描，若匹配不成功，则去掉第一个字符，重复上述的匹配步骤。

### 双向最大匹配算法
双向最大匹配法是将正向最大匹配法得到的分词结果和逆向最大匹配法的到的结果进行比较，从而决定正确的分词方法。定义的匹配规则如下：

如果正反向匹配算法得到的结果相同，我们则认为分词正确，返回任意一个结果即可。
如果正反向匹配算法得到的结果不同，则考虑单字词、非字典词、总词数数量的数量，三者的数量越少，认为分词的效果越好。我们设定一个惩罚分数（score_fmm / score_bmm = 0），例如：正向匹配中单字词数量多于反向匹配，则正向匹配的分值score_fmm += 1。其他两个条件相同。可以根据实际的分词效果调整惩罚分数的大小，但由于没有正确分词的数据，因此惩罚分数都设为1。最后比较惩罚分数，返回较小的匹配结果。


## 详例描述
以“对外经济技术合作与交流不断扩大。”为例，详细描述算法如下：
窗口大小设为4，句子长度为16，分词列表words = []。

首先是正向匹配。sub_str = ‘对外经济’与词典进行匹配，匹配失败，窗口大小减一。
sub_str = ‘对外经’与词典进行匹配，匹配失败，窗口大小减一。
sub_str = ‘对外’与词典进行匹配，匹配成功，窗口大小恢复为4，向右移动之前匹配词的长度，此时sub_str = ‘经济技术’，将其添加至列表words中。重复上述步骤。
当匹配到最后一个词时，算法停止。
正向匹配结果如下：[‘对外’, ‘经济’, ‘技术’, ‘合作’, ‘与’, ‘交流’, ‘不断’, ‘扩大’, ‘。’]
反向匹配如法炮制，结果如下：[‘对外’, ‘经济’, ‘技术’, ‘合作’, ‘与’, ‘交流’, ‘不断’, ‘扩大’, ‘。’]
正向与反向匹配结果相同，返回任意一个。


## 代码
### 加载字典

```python
def read_dict(path):
    words_dict = []
    with open(path, 'r') as r:
        line = r.readlines()
        # print(line)
        for i in line:
            word = i.split(',')
            words_dict.append(word[0])
    return words_dict


window_size = 4
```
### 正向匹配算法

```python
def fmm(source, words_dict):
    len_source = len(source)  # 原句长度
    index = 0
    words = []  # 分词后句子每个词的列表

    while index < len_source:  # 如果下标未超过句子长度
        match = False
        for i in range(window_size, 0, -1):
            sub_str = source[index: index+i]
            if sub_str in words_dict:
                match = True
                words.append(sub_str)
                index += i
                break
        if not match:
            words.append(source[index])
            index += 1
    return words
```
### 反向匹配算法

```python
def bmm(source, word_dict):
    len_source = len(source)  # 原句长度
    index = len_source
    words = []  # 分词后句子每个词的列表

    while index > 0:
        match = False
        for i in range(window_size, 0, -1):
            sub_str = source[index-i: index]
            if sub_str in words_dict:
                match = True
                words.append(sub_str)
                index -= i
                break
        if not match:
            words.append(source[index-1])
            index -= 1
    words.reverse()  # 得到的列表倒序
    return words
```
### 双向匹配算法

```python
def bi_mm(source, word_dict):
    forward = fmm(source, words_dict)
    backward = bmm(source, words_dict)
    # 正反向分词结果
    print("FMM: ", forward)
    print("BMM: ", backward)
    # 单字词个数
    f_single_word = 0
    b_single_word = 0
    # 总词数
    tot_fmm = len(forward)
    tot_bmm = len(backward)
    # 非字典词数
    oov_fmm = 0
    oov_bmm = 0
    # 罚分，罚分值越低越好
    score_fmm = 0
    score_bmm = 0
    # 如果正向和反向结果一样，返回任意一个
    if forward == backward:
        return backward
    # print(backward)
    else:  # 分词结果不同，返回单字数、非字典词、总词数少的那一个
        for each in forward:
            if len(each) == 1:
                f_single_word += 1
        for each in backward:
            if len(each) == 1:
                b_single_word += 1
        for each in forward:
            if each not in words_dict:
                oov_fmm += 1
        for each in backward:
            if each not in backward:
                oov_bmm += 1
        # 可以根据实际情况调整惩罚分值
        # 这里都罚分都为1分
        # 非字典词越少越好
        if oov_fmm > oov_bmm:
            score_bmm += 1
        elif oov_fmm < oov_bmm:
            score_fmm += 1
        # 总词数越少越好
        if tot_fmm > tot_bmm:
            score_bmm += 1
        elif tot_fmm < tot_bmm:
            score_fmm += 1
        # 单字词越少越好
        if f_single_word > b_single_word:
            score_bmm += 1
        elif f_single_word < b_single_word:
            score_fmm += 1

        # 返回罚分少的那个
        if score_fmm < score_bmm:
            return forward
        else:
            return backward
```
### 主函数
测试了分词的时间，包括加载词典的时间

```python
if __name__ == '__main__':
    start = time.time()
    words_dict = read_dict('chineseDic.txt')
    # print(bmm("我正在上自然语言处理课。", words_dict))
    # print("result: ", result)
    print("BiMM: ", bi_mm("对外经济技术合作与交流不断扩大。", words_dict))
    end = time.time()
    print("running time: " + str(end - start) + "s")
```
参考资料：[分词 | 双向匹配中文分词算法 python 实现](https://my.oschina.net/u/4344316/blog/3361167)