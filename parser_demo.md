
# Hanlp

pip install pyhanlp 安装即可  
项目地址：https://github.com/hankcs/pyhanlp

**基于神经网络的高性能依存句法分析器**

输出为CONLL格式中，每个词语占一行，无值列用下划线代替，列的分隔符为制表符'\t'，行的分隔符为换行符'\n'；句子与句子之间用空行分隔。  
CONLL标注格式包含10列，分别为：  

|ID|FORM|LEMMA|CPOSTAG|POSTAG|FEATS|HEAD|DEPREL|PHEAD|PDEPREL|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|

只用到前８列，其含义分别为：  

|id|name|含义|
|:--:|:--:|:--:|
|1   | ID      |当前词在句子中的序号，１开始.|
|2   | FORM    |当前词语或标点|
|3   | LEMMA   |当前词语（或标点）的原型或词干，在中文中，此列与FORM相同|
|4   | CPOSTAG |当前词语的词性（粗粒度）|
|5   | POSTAG  |当前词语的词性（细粒度）|
|6   | FEATS   |句法特征，在本次评测中，此列未被使用，全部以下划线代替。|
|7   | HEAD    |当前词语的中心词|
|8   | DEPREL  |当前词语与中心词的依存关系|





```python
from pyhanlp import *
```


```python
print(HanLP.parseDependency("徐先生还具体帮助他确定了把画雄鹰、松鼠和麻雀作为主攻目标。"))
```

    1	徐先生	徐先生	nh	nr	_	4	主谓关系	_	_
    2	还	还	d	d	_	4	状中结构	_	_
    3	具体	具体	a	ad	_	4	状中结构	_	_
    4	帮助	帮助	v	v	_	0	核心关系	_	_
    5	他	他	r	r	_	4	兼语	_	_
    6	确定	确定	v	v	_	4	动宾关系	_	_
    7	了	了	u	u	_	6	右附加关系	_	_
    8	把	把	p	p	_	15	状中结构	_	_
    9	画	画	v	v	_	8	介宾关系	_	_
    10	雄鹰	雄鹰	n	n	_	9	动宾关系	_	_
    11	、	、	wp	w	_	12	标点符号	_	_
    12	松鼠	松鼠	n	n	_	10	并列关系	_	_
    13	和	和	c	c	_	14	左附加关系	_	_
    14	麻雀	麻雀	n	n	_	10	并列关系	_	_
    15	作为	作为	v	v	_	6	动宾关系	_	_
    16	主攻	主攻	v	vn	_	17	定中关系	_	_
    17	目标	目标	n	n	_	15	动宾关系	_	_
    18	。	。	wp	w	_	4	标点符号	_	_
    



```python
sentence = HanLP.parseDependency("徐先生还具体帮助他确定了把画雄鹰、松鼠和麻雀作为主攻目标。")
for word in sentence.iterator():  # 通过dir()可以查看sentence的方法
    print("%s --(%s)--> %s" % (word.LEMMA, word.DEPREL, word.HEAD.LEMMA))
```

    徐先生 --(主谓关系)--> 帮助
    还 --(状中结构)--> 帮助
    具体 --(状中结构)--> 帮助
    帮助 --(核心关系)--> ##核心##
    他 --(兼语)--> 帮助
    确定 --(动宾关系)--> 帮助
    了 --(右附加关系)--> 确定
    把 --(状中结构)--> 作为
    画 --(介宾关系)--> 把
    雄鹰 --(动宾关系)--> 画
    、 --(标点符号)--> 松鼠
    松鼠 --(并列关系)--> 雄鹰
    和 --(左附加关系)--> 麻雀
    麻雀 --(并列关系)--> 雄鹰
    作为 --(动宾关系)--> 确定
    主攻 --(定中关系)--> 目标
    目标 --(动宾关系)--> 作为
    。 --(标点符号)--> 帮助



```python
print(dir(sentence))
```

    ['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__javaclass__', '__javaobject__', '__le__', '__lt__', '__metaclass__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'edgeArray', 'equals', 'findChildren', 'forEach', 'getClass', 'getEdgeArray', 'getWordArray', 'getWordArrayWithRoot', 'hashCode', 'iterator', 'notify', 'notifyAll', 'spliterator', 'toString', 'wait', 'word', 'wordArray', 'wordArrayWithRoot']



```python
word_array = sentence.getWordArray()
# print(word_array[0])
for word in word_array:
    print("%s --(%s)--> %s" % (word.LEMMA, word.DEPREL, word.HEAD.LEMMA))
```

    徐先生 --(主谓关系)--> 帮助
    还 --(状中结构)--> 帮助
    具体 --(状中结构)--> 帮助
    帮助 --(核心关系)--> ##核心##
    他 --(兼语)--> 帮助
    确定 --(动宾关系)--> 帮助
    了 --(右附加关系)--> 确定
    把 --(状中结构)--> 作为
    画 --(介宾关系)--> 把
    雄鹰 --(动宾关系)--> 画
    、 --(标点符号)--> 松鼠
    松鼠 --(并列关系)--> 雄鹰
    和 --(左附加关系)--> 麻雀
    麻雀 --(并列关系)--> 雄鹰
    作为 --(动宾关系)--> 确定
    主攻 --(定中关系)--> 目标
    目标 --(动宾关系)--> 作为
    。 --(标点符号)--> 帮助



```python
# 还可以直接遍历子树，从某棵子树的某个节点一路遍历到虚根
CoNLLWord = JClass("com.hankcs.hanlp.corpus.dependency.CoNll.CoNLLWord")
head = word_array[15]
while head.HEAD:
    head = head.HEAD
    if (head == CoNLLWord.ROOT):
        print(head.LEMMA)
    else:
        print("%s --(%s)--> " % (head.LEMMA, head.DEPREL))
```

    目标 --(动宾关系)--> 
    作为 --(动宾关系)--> 
    确定 --(动宾关系)--> 
    帮助 --(核心关系)--> 
    ##核心##


# StanfordNLP

pip install stanfordnlp 安装即可  
项目地址：https://github.com/stanfordnlp/stanfordnlp  
依存句法关系符号解释：https://www.cnblogs.com/sherry-yang/p/9061341.html


```python
import stanfordnlp
```


```python
nlp = stanfordnlp.Pipeline(lang='zh')
```

    Use device: gpu
    ---
    Loading: tokenize
    With settings: 
    {'model_path': '/home/haha/stanfordnlp_resources/zh_gsd_models/zh_gsd_tokenizer.pt', 'lang': 'zh', 'shorthand': 'zh_gsd', 'mode': 'predict'}
    ---
    Loading: pos
    With settings: 
    {'model_path': '/home/haha/stanfordnlp_resources/zh_gsd_models/zh_gsd_tagger.pt', 'pretrain_path': '/home/haha/stanfordnlp_resources/zh_gsd_models/zh_gsd.pretrain.pt', 'lang': 'zh', 'shorthand': 'zh_gsd', 'mode': 'predict'}
    ---
    Loading: lemma
    With settings: 
    {'model_path': '/home/haha/stanfordnlp_resources/zh_gsd_models/zh_gsd_lemmatizer.pt', 'lang': 'zh', 'shorthand': 'zh_gsd', 'mode': 'predict'}
    Building an attentional Seq2Seq model...
    Using a Bi-LSTM encoder
    Using soft attention for LSTM.
    Finetune all embeddings.
    [Running seq2seq lemmatizer with edit classifier]
    ---
    Loading: depparse
    With settings: 
    {'model_path': '/home/haha/stanfordnlp_resources/zh_gsd_models/zh_gsd_parser.pt', 'pretrain_path': '/home/haha/stanfordnlp_resources/zh_gsd_models/zh_gsd.pretrain.pt', 'lang': 'zh', 'shorthand': 'zh_gsd', 'mode': 'predict'}
    Done loading processors!
    ---



```python
doc = nlp("徐先生还具体帮助他确定了把画雄鹰、松鼠和麻雀作为主攻目标。")
doc.sentences[0].print_dependencies()
```

    ('徐', '2', 'nmod')
    ('先生', '4', 'nsubj')
    ('还', '4', 'mark')
    ('具体', '0', 'root')
    ('帮助', '4', 'obj')
    ('他', '7', 'nsubj')
    ('确定', '4', 'ccomp')
    ('了', '7', 'case:aspect')
    ('把', '15', 'aux:caus')
    ('画雄鹰', '15', 'obj')
    ('、', '12', 'punct')
    ('松鼠', '10', 'conj')
    ('和', '14', 'cc')
    ('麻雀', '10', 'conj')
    ('作', '7', 'ccomp')
    ('为', '15', 'mark')
    ('主攻', '18', 'nmod')
    ('目标', '16', 'obj')
    ('。', '4', 'punct')


# HIT LTP
项目地址：  
* https://github.com/HIT-SCIR/pyltp  
* https://pyltp.readthedocs.io/zh_CN/latest/  

安装步骤：
* pip install pyltp
* 下载模型文件：[七牛云](http://ltp.ai/download.html)，当前模型版本 3.4.0

输出：
* arc.head 表示依存弧的父节点词的索引。ROOT节点的索引是0，第一个词开始的索引依次为1、2、3…  
* arc.relation 表示依存弧的关系。  

标注集请参考: https://ltp.readthedocs.io/zh_CN/latest/appendix.html#id5



```python
from pyltp import Parser
from pyltp import Segmentor
from pyltp import Postagger

def dependency_parser(sentences):
    output = []
    for sentence in sentences:
        parser = Parser()
        parser.load('./ltp_data_v3.4.0/parser.model')
        segmentor = Segmentor() 
        segmentor.load('./ltp_data_v3.4.0/cws.model')
        postagger = Postagger() 
        postagger.load('./ltp_data_v3.4.0/pos.model')

        words = segmentor.segment(sentence)
        postags = postagger.postag(words)
        arcs = parser.parse(words, postags)
        output.append({'words':words,
                       'postags':postags,
                       'arcs':arcs
                      })
#         print(' '.join(output[0]['words']))
#         print(' '.join(output[0]['postags']))

    segmentor.release() 
    postagger.release()
    parser.release()
    return output
```


```python
sentences = ['徐先生还具体帮助他确定了把画雄鹰，松鼠和麻雀作为主攻目标。']
output = dependency_parser(sentences)
Arcs = [each['arcs'] for each in output]
[" ".join("%d:%s" % (arc.head, arc.relation) for arc in arcs) for arcs in Arcs]
```




    ['2:ATT 5:SBV 4:ADV 5:ADV 0:HED 5:DBL 5:VOB 7:RAD 10:ADV 7:VOB 10:VOB 5:WP 16:SBV 15:LAD 13:COO 5:COO 18:ATT 16:VOB 5:WP']



# FudanNLP (FNLP)
https://github.com/FudanNLP/fnlp  
java 接口，且不再更新，现在已经推出FastNLP


```python

```
