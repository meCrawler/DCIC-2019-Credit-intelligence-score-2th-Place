# DCIC-2019-Credit-intelligence-score-2th-Place
2019数字中国创新大赛 消费者人群画像 亚军<br>
首先非常感谢队友neil和gotcha几个月的合作，最终拿了几个周冠军和线上第一的成绩，最终答辩第二，再接再厉<br>

## 感想
NLP队伍不完整代码（只包含我这部分,后面会链接到队友gotcha的代码）。<br>
关于此次赛题，数据上来说可挖掘潜力并不是那么大，因此各个队伍能挖掘到的特征基本都很相似<br>
于是只能拼数据，拼模型，拼骚操作了<br>

## 赛题理解与特征工程
本次赛题有些数据已经被主办方处理过，有些缺失值被用0来填充，导致一些特定的数据难以分辨是空值还是0值， 还有一些数据被主办方取整和分箱了，因此适当处理源数据会有一定提升<br>
对于特征工程本团队主要构建了以下特征：<br>
    前五个月消费总费用 = 6 * 近六个月消费总费用 - 当月费用<br>
    当月费用 - 前六个月平均费用<br>
    当月费用 - 前五个月消费总费用/5<br>
    入网月份 = 网龄 mod 12<br>
    布尔型特征相加<br>
    年龄、网龄分箱<br>
    是否998折<br>
    count_最近一次缴费金额<br>
    count_当月总费用<br>
    count_前六个月平均费用<br>
    count_费用差<br>
    count_（当月总费用，前六个月平均费用）<br>

## 模型
对于模型本团队采用的模型有lightGBM，xgboost，catboost，GBDT，RandomForest<br>
其他的很多模型也都有尝试<br>
至于损失函数则有mse，mae，huber和自定义介于mse与mae之间的损失函数<br>
模型融合采用了huber_regressor作为学习器，可以很大的克服异常值带来的影响，鲁棒性很强，其他团队基本都采用线性加权和分段融合，其实这些融合都要根据不同数据来进行权重参数调整鲁棒性没有那么强<br>
之前也尝试过很多种融合方法，加权和分段融合也都采用过，stacking第二层的模型也进行过很多种尝试大部分都是收效甚微<br>
但是这也并不代表都没有价值，只要多去尝试总能发现好东西，尝试真的很重要<br>

## 注意事项
关于第三方包的版本：<br>
panda==0.23.4<br>
numpy==1.15.0<br>
catboos==0.11.2<br>
lightgb==2.2.2<br>
scipy==1.0.0<br>
sklearn==0.19.1<br>
xgboost==0.71<br>
plotly==3.4.2<br>
还有一个有意思的点是训练的时候线程数有时会有很大的影响，本次模型默认的都是八线程<br>

gotcha开源地址：https://github.com/PanJianning/DCIC-2019-Credit-2th-Place<br>
