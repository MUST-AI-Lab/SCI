SimCLR 做单分类 跑出的结果


## 1. Datasets 
    CIFAR-10

## 2. Training
    batch size = 32 （文章里用的是512）
    单张卡跑的

## 3. resultsr 

simclr这个方法， 文章给出的没有 每个类的结果，只给出了一个最终的 10个类 的平均结果

| Method        | Dataset           |  AUROC (Mean) |
| --------------|------------------ | --------------|
| 文章给的结果    | CIFAR-10          |      87.9%    |
| 复现出的结果    | CIFAR-10          |      89.79%   |


| class         |    0   |   1    |   2    |   3    |   4    |   5    |   6    |   7    |   8    |   9    | AUROC (Mean)|
| --------------|--------|--------|--------|--------|--------|--------|--------|--------|--------|--------|-------------|
| 复现           | 0.8702 | 0.9896 | 0.9043 | 0.8359 | 0.8621 | 0.8814 | 0.8832 | 0.9372 | 0.9344 | 0.8807 |    0.8979   |



### 欧氏距离跑出的结果：

在做欧氏距离之前，做归一化 ---> 这样的话，这时候的欧氏距离 和 余弦相似度 成 线性相关

    通过 对欧氏距离，即 Eulidean（x1， x2） 判断 x1 和 x2的相关性：
    | class          |    0   |   1    |   2    |   3    |   4    |   5    |   6    |   7    |   8    |   9    | AUROC (Mean)|
    | ---------------|--------|--------|--------|--------|--------|--------|--------|--------|--------|--------|-------------|
    | 余弦相似度做测试 | 0.8687 | 0.9884 | 0.9022 | 0.8389 | 0.8826 | 0.8835 | 0.8941 | 0.9564 | 0.9454 | 0.8843 |    0.9044    |
    | 欧式距离做测试   | 0.9076 | 0.9898 | 0.9017 | 0.8346 | 0.8792 | 0.8950 | 0.8967 | 0.9563 | 0.9365 | 0.9039 |    0.9101    |

    通过 对欧氏距离 的平方，即 Eulidean（x1， x2）^2 判断 x1 和 x2的相关性：
    | class         |    0   |   1    |   2    |   3    |   4    |   5    |   6    |   7    |   8    |   9    | AUROC (Mean)|
    | --------------|--------|--------|--------|--------|--------|--------|--------|--------|--------|--------|-------------|
    | 余弦相似度做测试 | 0.8991 | 0.9878 | 0.8966 | 0.8286 | 0.8683 | 0.8877 | 0.8853 | 0.9510 | 0.9290 | 0.8923 |    0.9025   |
    | 欧式距离做测试   | 0.9076 | 0.9898 | 0.9017 | 0.8346 | 0.8792 | 0.8950 | 0.8967 | 0.9563 | 0.9365 | 0.9039 |    0.9101   |


在做欧氏距离之前，不做归一化 ---> 只用 欧氏距离 判断两个样本之间的相关性
    通过 对欧氏距离，即 Eulidean（x1， x2） 判断 x1 和 x2的相关性：
| class          |    0   |   1    |   2    |   3    |   4    |   5    |   6    |   7    |   8    |   9    | AUROC (Mean)|
| ---------------|--------|--------|--------|--------|--------|--------|--------|--------|--------|--------|-------------|
| 余弦相似度做测试 | 0.6985 | 0.7330 | 0.7288 | 0.5853 | 0.7397 | 0.5688 | 0.5814 | 0.6760 | 0.7548 | 0.5235 |    0.6590    |
| 欧式距离做测试   | 0.6590 | 0.7276 | 0.6940 | 0.5394 | 0.7190 | 0.5251 | 0.5140 | 0.6425 | 0.7193 | 0.5083 |    0.6248    |


欧氏距离 的结果 明显不如 余弦相似度的 结果好





## Citation
```
@inproceedings{tack2020csi,
  title={CSI: Novelty Detection via Contrastive Learning on Distributionally Shifted Instances},
  author={Jihoon Tack and Sangwoo Mo and Jongheon Jeong and Jinwoo Shin},
  booktitle={Advances in Neural Information Processing Systems},
  year={2020}
}
```
