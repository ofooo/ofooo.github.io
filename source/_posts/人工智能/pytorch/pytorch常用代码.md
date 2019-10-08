---
title: pytorch常用代码
toc: true
categories:
  - 人工智能
  - pytorch
date: 2019-06-05 09:35:55
tags:
---





pytorch版本: 1.1.0



## 张量

### 创建一个张量

```bash
# 通用注释: x表示其他张量     
# size0,size1表示张量维度, 数量不固定
# data 表示张量的数组值(python数组类型)

zeros = torch.zeros(
	size0, size1, dtype=x.dtype, device=x.device, requires_grad=True)

zeros = torch.zeros(data, dtype=torch.long) # 指定具体地数据类型

# 随机化生成
x = torch.rand(size0, size1)	# 默认 torch.float32
x = torch.rand(size0, size1, dtype=torch.float)
x = torch.rand(size=[size0, size1], dtype=torch.float)
t=torch.rand(t.size())    //均匀分布
t=torch.randn(t.size())   //标准正态分布
t=torch.normal(mean,std)  //size同t.Tensor()，每个数以对应的均值mean和标准差std[i,j,...]正态采样。

x = torch.randint(low=1, high=100, size=[12, 2], dtype=torch.long)
x = torch.LongTensor(size0, size1)	# 在pycharm中有错误提示

#均分区间生成Tensor、
t=T.arange(m,n,step_length) //[m,n)中m开始以步长step_length生成
t=T.range(m,n,step_length)  //[m,n-1]中m开始以步长step_length生成
t=T.linspace(m,n,step_num)  //[m,n]中以m为首项，n为末项，均分区间为step_num段

# 可以与list或numpy中的array互相转化：
t=T.Tensor(list)
t=T.Tensor(np.array)
t=T.from_numpy(np.array)
list=T.tolist(t)
array=t.numpy()

```

### 观察一个张量

```python
t.size()            //返回size类型
t.numel()          //返回总元素个数
t.view(d1,d2,d3....)//维度重整
t.unsqueeze(di)     //在di个维度处升维、
t.squeeze(di)       //若di维是1，压缩，否则不变。若无参数，压缩所有“1”维
torch.cat((t,t,...),dim=1) //按第di的维度按照tuple的格式复制t
torch.chunk(t,i,dim)     //在di维上将t分成i份，最后一份的维度不定（若不能整除）
```

采数据

```python
torch.index_select(t, di, indices)  //在第di维上将t的indices抽取出来组成新Tensor。
torch.masked_select(t, mask)        //按照0-1Tensor mask的格式筛选t，返回一维Tensor
torch.nonzero(t)                    //输出n×2维Tensor，非零元素的index
```









计算

| 功能                   | 代码                   |
| ---------------------- | ---------------------- |
| P范数（N方求和后开方） | torch.norm(input, p=2) |
|                        |                        |
|                        |                        |
|                        |                        |
|                        |                        |
|                        |                        |
|                        |                        |
|                        |                        |
|                        |                        |
|                        |                        |
|                        |                        |
|                        |                        |
|                        |                        |

指定GPU（3种方式）

```
torch.cuda.set_device(id)
os.environ["CUDA_VISIBLE_DEVICES"] = "2"
CUDA_VISIBLE_DEVICES=1 python main.py
```



网络层









## 参考资料
> - []()
> - []()
