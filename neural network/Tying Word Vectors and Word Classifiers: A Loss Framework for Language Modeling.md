#### note:
&emsp;&emsp;作者指出,使用RNN结构实现语言模型,loss方程的设计仅使用了one hot,即仅使用正确的word对应的损失.作者提出使用方程分布的形式添加额外的loss, 考虑如下情况: "高兴"和"开心"是相似词, 如果output layer的target word是"高兴", 那"开心"也很可能是正确的target,而one hot设计没有考虑这部分相似信息. paper使用了预训练得到的word embedding来描述词与词这种相似性, 设为groundtruth(其包含了每个词与其它词之间的相似度, 假定该相似关系构成了分布Q), 在projection layer部分,为了使target word下,其余词的分布P与Q相等, 可推得input embedding(即为word embedding)和output projection相等. 判断分布P与分布Q的差异使用了KL散度.

#### comment:
  1. 文章背后提出的逻辑有依据, 从最初的loss设计考虑分布出发,到推得input embedding和output projection相等的关系,逐步深入.同时,在该论文之前,已有[实验](https://github.com/xwzhong/papernote/blob/master/neural%20network/Using%20the%20Output%20Embedding%20to%20Improve%20Language%20Models.md)证明连接input embedding和output embedding能改进语言模型和翻译模型;
  2. 分布loss(文中也叫augment loss)结果的好坏很大程度上取决于预训练得到的word embedding质量,因作者假定word embedding为groundtruth, 由P取拟合Q;
  3. [图文解说及代码](https://github.com/icoxfog417/tying-wv-and-wc).
