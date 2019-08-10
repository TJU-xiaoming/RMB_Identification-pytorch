# TinyMind_RMB_Identification
具体比赛网址：https://www.tinymind.cn/competitions/47#overview
# A、热身赛描述
识别人民币的面值，采用的训练集train_data 39620张图片，测试集public_test_data 20000张图片，以及.csv标签文件

    思路:直接将每种面值视为一类，抽象成9分类问题
    
    具体流程：先使用fine-tune微调一个ImageNet上训练过得分类网络，在测试集上进行TTA，基础网络采用resnet18网络。
# B、正式赛描述
人民币冠字号编码识别，训练人民币冠字号编码识别模型，使得该模型能自动根据输入的任意人民币图片识别对应人民币的编码。采用的训练集train_data 39620张图片，
使用验证数据（public_test_data），将训练好的模型得出的编码识别结果。再使用测试集private_test_data得出分数。
    
    思路：人民币编码定为+人民币编码识别
    
    具体流程：先使用Faster-RCNN对所有图片进行编码定位，然后再进行切割，只保留十位字符部分。对于编码识别部分，采用两个模型：
    
    （1）CNN+RNN+CTC
    
    （2）Multi-CNN，使用1个CNN同时对1张图片进行10次分类操作
    
    将上述两个模型进行结果的融合，如果CNN+RNN+CTC的结果存在问题，则使用Multi-CNN的结果进行代替，以修正误差。
