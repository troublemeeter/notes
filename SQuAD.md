# [SQuAD2.0](ttps://rajpurkar.github.io/SQuAD-explorer/)
## top1: BERT + DAE + AoA
* AoA: attention over attention [1]
* DAE: DA Enhanced
	* Data Augmentation 
	* Domain Adaptation

![AoA](https://img2018.cnblogs.com/blog/1237161/201809/1237161-20180925183754022-1457033139.png)

<https://www.infoq.cn/article/M7NpCAAMrPzRo-RViOKs>  
<https://zhuanlan.zhihu.com/p/27361305>

	[1] Cui Y, Chen Z, Wei S, et al. Attention-over-attention neural networks for reading comprehension[J]. arXiv preprint arXiv:1607.04423, 2016.

## top2: BERT + ConvLSTM + MTL + Verifier
* MTL: 多任务学习
	* <del>预测一个问题是否可答</del>
	* <del>预测该问题在篇章中的答案</del>
* Verifier: 验证器 [1]
* convLSTM [2]

<https://msd.misuland.com/pd/12136984602514128>  
<https://blog.csdn.net/maka_uir/article/details/83650978>

	[1] Hu M, Peng Y, Huang Z, et al. Read+ verify: Machine reading comprehension with unanswerable questions[J]. arXiv preprint arXiv:1808.05759, 2018.
	[2] Shi X , Chen Z , Wang H , et al. Convolutional LSTM Network: A Machine Learning Approach for Precipitation Nowcasting[J]. 2015.



## top3: BERT + N-Gram Masking + Synthetic Self-Training
* N-Gram Masking: 类似百度的ERNIE模型
* Synthetic Self-Training: BERT官方PPT  

(这个方法全部在预训练上做改进，没有对bert上层模型做什么改进)  
Unclear if adding things on top of BERT really helps by very much.  

<https://zhuanlan.zhihu.com/p/63126803>  
<https://nlp.stanford.edu/seminar/details/jdevlin.pdf>

## 其他

<http://web.stanford.edu/class/cs224n/posters/15845024.pdf>

	[1] Ensemble BERT with Data Augmentation and Linguistic Knowledge on SQuAD2.0
