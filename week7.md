## 提高OCNLI任务准确率

roberta_large(acc: 74-76?)

### 尝试架构 Siamese network

使用 Bert_chinese_base:

结构如下

![image-20240513143923344](C:/Users/wyd/AppData/Roaming/Typora/typora-user-images/image-20240513143923344.png)



acc 大约50

结果并不理想，有可能是因为学不到推理的语义

### 论文 StructBERT: Incorporating Language Structures into Pre-training for Deep Language Understanding

https://arxiv.org/abs/1908.04577

ICLR 2020：

结果：

without finetune：

![image-20240513131659202](C:/Users/wyd/AppData/Roaming/Typora/typora-user-images/image-20240513131659202.png)

with finetune：

![image-20240513131626602](C:/Users/wyd/AppData/Roaming/Typora/typora-user-images/image-20240513131626602.png)

在损失函数构建时增加任务：

打乱句中单词顺序

![image-20240513112404336](C:/Users/wyd/AppData/Roaming/Typora/typora-user-images/image-20240513112404336.png)



![image-20240513112426668](C:/Users/wyd/AppData/Roaming/Typora/typora-user-images/image-20240513112426668.png)

psp（previous sentence prediction）： 预测是否为前句

Rsp（random sentence prediction）： random s2, 查看是否不是连续出现

与nsp区别：处理较为断裂或无序的文本信息时的鲁棒性，例如，在网络抓取的内容或多来源文本聚合时，内容间可能不具有直接的逻辑关系。



下周任务：

尝试论文

### Logical Reasoning with Span-Level Predictions for Interpretable and Robust NLI Models （EMNLP2022）

![image-20240513153400022](C:/Users/wyd/AppData/Roaming/Typora/typora-user-images/image-20240513153400022.png)

这些表示随后被送入中立检测层，以计算出与每个跨度相关的值和损失。

输出每个跨度的中立值（an,i）和跨度损失（Ln,i）

span loss + sequence loss 
