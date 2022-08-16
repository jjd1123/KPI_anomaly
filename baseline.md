# 异常检测主要流程
1. ### 将数据从数据库中提取出来：
    - 搞一个类专门用来操作数据库，需求是要能够提取数据并将检测的数据存储(将处理好的数据储存起来以及提取出来)
2. ### 处理数据：数据处理类
   - 排序、去除重复数据
   - 转化为timestamp、value、label格式
   - 填补缺失数据：label设为1，value设为0
   - 储存
   - 转化为one-hot编码：60代表分钟+24代表小时+7代表天
3. ### 制作数据集：
    - framedata：窗长为120(可以自己选择)，timedata：取窗内最后一个点的时间戳(on-hot)
4. ### 搭建网络：
   - coder类
   - CVAE类：包含encoder、decoder和采样用到了重参数技巧(reparametrization trick)
   - 损失函数：modified-ELBO或者ELBO均可
5. ### train：
   - batchsize：64
   - epoch：<100(视具体情况而定)
6. ### detection：
   - 以重建误差为标准，**具体找阈值方案待定** 注：需要自己重写detection函数，模型中给的detection函数需要标签。

# Citation
Li, Zeyan, Wenxiao Chen, and Dan Pei. "Robust and Unsupervised KPI Anomaly Detection Based on Conditional Variational Autoencoder." 2018 IEEE 37th International Performance Computing and Communications Conference (IPCCC). IEEE, 2018.