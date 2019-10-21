# 第二期猫狗识别案例使用Xception、InceptionV3等神经网络尝试
## 1
[知乎上的猫狗识别案例](https://zhuanlan.zhihu.com/p/25978105) 这个作者说的非常好，但是我卡在了运用他训练的.h5文件参数等跑我们自己的猫狗数据集时，数据维度就对不上，只能按照他的（25000，,2048）这个维度来，行不通。不过这个尝试让我学会怎么把超过100MB的文件上传到Jupyter notebook中，就是先上传到OBS中，然后用MOdel.session把文件下载进来就ok（ps:速度确实是快）

## 2
做了好几天，发现在不使用'imagenet'预训练出的文件情况下，始终找不到办法提高准确率(Xception，InceptionV3)，Xception在几轮之后就开始过拟合，InceptionV3训练准确率一直提不上去[可能是我不会调节神经网络的层数或者参数。。][以后会了还会把猫狗识别这个案例调节上去的，等以后学的多了再过来看看吧]。做到最后有点沮丧，所以就拿三个Xception InceptionV3 还有VGG19三个模型的imagenet做训练，顺便还找了个VGG16的'imagenet’预训练文件试了试，做到最后还有有点小发现的。

## 3
因为cpu一直用不掉  用cpu做一次训练 发现速度真的是可以了(基本上一个epoch就要3,4个小时)，算了还是GPU吧

## 4
读取.h5文件的权重，因为Jupyter notebook我这里下载预训练文件很慢，我把他们下载到了本地，通过OBS服务上传到Jupyter notebook中(速度很快)

base_model = InceptionV3(weights=None, include_top=False,input_shape=(rows, cols, channels), pooling='avg')
base_model.load_weights('./inception_v3_weights_tf_dim_ordering_tf_kernels_notop.h5')
然后通过这两句话进行模型建立就好，看好.h5文件存放位置就可以

![image](https://user-images.githubusercontent.com/50792908/67177829-cf819a00-f402-11e9-9161-701f2b269bbd.png)


#  进入正题==============================

## Xception

使用Imagenet后在训练集上很好，但是测试集效果一般，过拟合现象，最后跑到测试集上啥用没有

![image](https://user-images.githubusercontent.com/50792908/67162047-0b7d1680-f393-11e9-909a-7764836fab21.png)

## InceptionV3
![image](https://user-images.githubusercontent.com/50792908/67162098-8e9e6c80-f393-11e9-9331-8d01ead2d2b9.png)

和XceptiXception一样，也是过拟合

## VGG19
在VGG19中，发现无参运行下，10轮下来，模型几乎没有提升，而在imagenet情况下，发现前几轮训练很差，但是7轮之后速度飞速上升，
这个是参数没有预训练的，

![image](https://user-images.githubusercontent.com/50792908/67162055-23549a80-f393-11e9-85d6-11fae57aba61.png)

这个是参数预训练的

![image](https://user-images.githubusercontent.com/50792908/67162065-35ced400-f393-11e9-9fad-0c0a4527983a.png)

很明显，没有预训练过的在10epoch之中几乎没有显现效果，预训练过的在前期也很low，但是7epoch下来之后开始飞速上涨。（小惊喜）。

## VGG16
这个是带预训练的，和VGG19很类似，前期比较low，但是后期涨得快，和不带预训练的有所差异。(图片上的标题写错了，是VGG16)

![image](https://user-images.githubusercontent.com/50792908/67162132-d0c7ae00-f393-11e9-8a2a-be2f586bbe75.png)

### 所有预训练的.h5文件我下载到本地了，各位想下载的可以[云盘](https://pan.baidu.com/s/1rcRwW46F2zYdpj9pj1CKnA&shfl=sharepset)
### 提取码：ssp0 

### 最后，[Github项目地址](https://github.com/JUSxuaxuan/cat_dog/blob/master/%E7%AC%AC%E4%BA%8C%E6%9C%9F%E6%89%A9%E5%B1%95%E7%8C%AB%E7%8B%97%E8%AF%86%E5%88%AB.ipynb)

[个人感觉，这16期活动，都能开个培训班了~~~~]

