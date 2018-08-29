# word2vec

实习期间接触到一些关于NLP的知识。其中一个常用的操作就是将中文词汇映射到词向量，对其中的原理却不太清晰。下面对word2vec的训练过程做一些简单的学习。<br>

## 什么是word2vec？
个人的理解是，word2vec是一种实现Word Embedding的一种方式，是无监督的。

## 训练依赖
* jieba <br>
```
pip3 install jieba
```
* gensim <br>
gensim是一款开源的第三方Python工具包，用于从原始的非结构化的文本中，无监督地学习到文本隐层的主题向量表达。它支持包括TF-IDF，LSA，LDA，和word2vec在内的多种主题模型算法，支持流式训练，并提供了诸如相似度计算，信息检索等一些常用任务的API接口。
```
pip3 install -U gensim
```

## 训练过程
1.训练语料获取

*由于word2vec是基于无监督学习训练的，所以语料一定越大越好。本文是基于维基百科的最新数据做测试的，数据可以在这里[下载](https://dumps.wikimedia.org/zhwiki/)，可以挑选最新语料。注意是下载pages-articles.xml.bz2结尾的文件。*

2.使用`wiki2txt.py`从下载的xml格式文件中提取出维基文章

*维基百科下载完成后是一份xml文件，里面布满了各种各样的标签，我们需要先去除掉这些不速之客，然而gensim早已看穿一些，直接调用wikiCorpus，可以很轻松的只取出文章的标题和内容。*
```
python3 wiki2txt.py zhwiki-20180820-pages-articles.xml.bz2
```
*请根据下载的文件适当更改上面的文件名。*

3.使用`jieba`对文分词，并去除停用词

```
python3 segment.py
```

4.使用`gensim`的word2vec模型进行训练

```
python3 train.py
```

5.测试训练出的模型
```
python3 demo.py
```
