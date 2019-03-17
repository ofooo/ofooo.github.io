---
title: python读写ini配置文件
tags: [python]

---

```python
import configparser
cfg = configparser.ConfigParser()    #创建对象
cfg.read('../data/system_config4.ini')     #读取ini配置文件
cfg.sections()  # 所有节点名称,元组
cfg.options("Register")   # 读取某一节点参数, 一维元组
cfg.items("Register")    # 读取某一节点参数, 二维元组
get('section','option')      # 得到section中的option的值，注意返回的都是str, 其他格式自己转
getint('section','option')    # 取得int
cfg.set("Register","serial","abc")     # 修改参数（第一个参数为节点名称）
cfg.remove_option("Register", "serial")    #删除节内参数
cfg.remove_section("Register")       #删除节
with open('write.ini', 'w') as fw:       # 写入配置文件
	cfg.write(fw)
```





```ini
# 用井号注释

# 每个中括号包裹一个sections(节)
[T1]
# 参数： 键=值 name = value 
path_to_search = data/BRATS_examples/HGG, data/BRATS_examples/LGG
#keywords in input file names, matched filenames will be used
filename_contains = T1
#keywords in input file names, negatively matches filenames
filename_not_contains = T1c
#specify the spatial size of the input data (ndims <= 3)
spatial_window_size = (19, 144, 144)
#labels for positive end of voxel axes, possible labels are ('L','R'),('P','A'),('I','S')
#see also nibabel.orientations.ornt2axcodes
axcodes=(L,P,S)
#interpolation order of the input images
interp_order = 3

[T2]
path_to_search = data/BRATS_examples/HGG, data/BRATS_examples/LGG
filename_contains = T2
filename_not_contains =
spatial_window_size = (19, 144, 144)
axcodes=(L,P,S)
interp_order = 3

[T1c]
path_to_search = data/BRATS_examples/HGG, data/BRATS_examples/LGG
filename_contains = T1c
filename_not_contains =
spatial_window_size = (19, 144, 144)
axcodes=(L,P,S)
interp_order = 3

[Flair]
path_to_search = data/BRATS_examples/HGG, data/BRATS_examples/LGG
filename_contains = Flair
filename_not_contains =
spatial_window_size = (19, 144, 144)
axcodes=(L,P,S)
interp_order = 3

[label]
path_to_search = data/BRATS_examples/HGG, data/BRATS_examples/LGG
filename_contains = Label
filename_not_contains =
spatial_window_size = (11, 144, 144)
axcodes=(L,P,S)
interp_order = 0

############################## system configuration sections
[SYSTEM]     ##Application_args
cuda_devices = ""
num_threads = 2
num_gpus = 1
##Directory to save/load intermediate training models and logs 模型保存路径
model_dir = models/anisotropic_nets_brats_challenge/model_whole_tumor_axial
#Set size of preprocessing buffer queue,默认为5
queue_length = 20

[NETWORK]
#Choose a net from NiftyNet/niftynet/network/ or from user specified module string         
name = anisotropic_nets_brats_challenge.wt_net.WTNet
#激活函数类型  
#  {'relu': tf.nn.relu,
#                'relu6': tf.nn.relu6,
 #               'elu': tf.nn.elu,
 #               'softplus': tf.nn.softplus,
 #               'softsign': tf.nn.softsign,
 #               'sigmoid': tf.nn.sigmoid,
 #               'tanh': tf.nn.tanh,
 #               'prelu': prelu,
 #               'selu': selu,
 #               'leakyrelu': leaky_relu,
 #               'dropout': tf.nn.dropout}
activation_function = prelu
#[Training only] Set weight decay
decay = 1e-7
#[Training only] Specify regulariser type_str 默认为L2
reg_type = L2
#Set batch size of the net
batch_size = 1
#Set padding size of each volume (in all dimensions)
volume_padding_size=(4,15,15)
#A reference file of histogram for intensity normalisation  this file should in
#the model_dir
histogram_ref_file = label_mapping_whole_tumor.txt
#Indicates if the whitening of the data should be applied
whitening = True
#Indicates whether a foreground mask should be applied when normalising volumes
normalise_foreground_only = True
multimod_foreground_type = and
foreground_type = threshold_plus

[TRAINING]
#Choose an optimiser for computing graph gradients and applying，默认为adam
optimiser = adam
# Set number of samples to take from each image that was loaded in a given training epoch
#默认为1
sample_per_volume = 24
#Set learning rate，学习速率默认为0.01
lr = 1e-4
#Specify loss type_str，默认为Dice
loss_type = Dice
#Resume from iteration n 循环开始
starting_iter = 0
#Model saving frequency
save_every_n = 5000
#Total number of iterations
max_iter = 10000
#Maximum number of model checkpoints that will be saved
max_checkpoints = 20

[INFERENCE]
# Width of borders to crop for segmented patch
border = (4,0,0)
# Prediction directory name
save_seg_dir = ./pred_whole_tumor_axial
#interpolation order of the network output 网络输出的插值顺序
output_interp_order = 3
#Specify the spatial size of the input data (ndims <= 3)
spatial_window_size = (120, 144, 144)
#Use the checkpoint at this iteration for inference
inference_iter = 15000

############################ custom configuration sections
[SEGMENTATION]
image = Flair,T1,T1c,T2
label = label
output_prob = True
num_classes = 2
label_normalisation = True
```

