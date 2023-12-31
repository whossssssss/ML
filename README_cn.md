## _传统中医药的识别_

传统中医作为世界医疗系统中不可或缺的医疗方法，目前越来越为人所知并被广泛使用。在此期间，传统中医也经历了飞速的发展。然而，中药材的种类繁多且复杂，普通人对于中药材的识别知识相对有限，这可能导致不当使用并带来不良后果。

- 由于不当使用而导致的中毒。
- 药效的丧失。
- 药物间的不良相互作用。
- 误导性的自我诊断，安全风险。
- ✨经济损失✨。

该模型的目的是帮助那些不了解或不熟悉传统中医的人，轻松识别传统中医药的种类，从而避免上述问题。

## 代码结构详解

> ─── read.py # 数据读取
>
> ─── split.py # 数据分类
>
> ─── images  # 图像文件
>
> ─── models # 模型
>
> ─── main.py # 用户界面
>
> ─── test.py # 模型测试
>
> ─── train.py # 模型训练
>
> ─── chat.py # 语言翻译

## read.py
该代码的主要功能是分析指定文件夹下每个子文件夹中的图像数量，并使用Matplotlib库来创建横向柱状图，直观显示每个子文件夹中图像数量的分布。主要步骤包括：

- 使用 read_flower_data 函数计算每个子文件夹中的图像数量。
- 使用 show_bar 函数创建柱状图，Y轴显示子文件夹名称，X轴显示相应的图像数量。
- 该代码的主要目的是帮助用户理解特定文件夹中的图像数据，以更好地了解不同子文件夹中的图像数量分布。

以下是图像输出示例：
![示例图片](https://github.com/whossssssss/ML/blob/google-colab/myplot.png)

## split.py
该代码的主要功能是将源数据文件夹中的图像数据集分割成训练集、验证集和测试集，并将它们复制到不同的目标文件夹中。

data_set_split 函数：
- src_data_folder：源数据文件夹，包含每个类别的图像数据。
- target_data_folder：目标文件夹，用于存储分割后的数据集。
- train_scale, val_scale, test_scale：训练集、验证集和测试集的比例，默认为0.8、0.1、0.1。

函数内部操作：
- 首先，它提取源数据文件夹中所有类别（以文件夹形式存在）。
- 然后，在目标文件夹中创建三个子文件夹：train、val 和 test，分别用于存储训练集、验证集和测试集的图像数据。
- 接下来，它遍历每个类别：
- 对于每个类别，它会随机打乱该类别的图像数据顺序。
- 根据设定的比例将图像复制到训练集、验证集或测试集文件夹中。
- 最后，函数输出每个类别的详细信息，包括文件夹路径和每个数据子集中的图像数量。

## train.py
此代码通过使用预训练的 MobileNetV2 模型作为基础模型进行迁移学习来选择模型。以下是模型的主要信息：
- 使用的预训练模型：MobileNetV2。
- 固定基础模型权重：`base_model.trainable = False`，意味着预训练模型 MobileNetV2的权重被冻结，不进行微调。
- 自定义层：在 MobileNetV2 模型上添加的全局平均池化层和输出层。

以下是训练模型的图形输出：
![训练图像1](https://github.com/whossssssss/ML/blob/google-colab/train_1.png)
![训练图像2](https://github.com/whossssssss/ML/blob/google-colab/train_2.png)

在未来的模型改进计划中，我们会使用自定义的卷积神经网络（CNN）模型，但该模型在上传时尚未完成。

## test.py
加载训练好的模型并进行测试，以评估模型在测试数据上的表现。测试结果包括损失和准确率，这些指标衡量了模型对新的、以前未见过的数据的性能。

以下是测试集的输出数据：
```sh
Found 176 files belonging to 5 classes.
Using 35 files for validation.
Model: "sequential"
_________________________________________________________________
 Layer (type)                Output Shape              Param #   
=================================================================
 rescaling (Rescaling)       (None, 224, 224, 3)       0         
                                                                 
 mobilenetv2_1.00_224 (Func  (None, 7, 7, 1280)        2257984   
 tional)                                                         
                                                                 
 global_average_pooling2d (  (None, 1280)              0         
 GlobalAveragePooling2D)                                         
                                                                 
 dense (Dense)               (None, 5)                 6405      
                                                                 
=================================================================
Total params: 2264389 (8.64 MB)
Trainable params: 6405 (25.02 KB)
Non-trainable params: 2257984 (8.61 MB)
_________________________________________________________________
9/9 [==============================] - 2s 72ms/step - loss: 0.0044 - accuracy: 1.0000
Test accuracy : 1.0
```

## chat.py

ChatTranslator 是一个使用 googletrans 库进行文本翻译和语言检测的 Python 类。

### 功能

- **文本翻译**：将指定文本翻译成目标语言。
- **语言检测**：检测指定文本的语言。
- **处理查询**：处理文本查询，包括语言检测和翻译。

这段代码定义了一个 ChatTranslator 类，它使用 googletrans 库进行文本翻译和语言检测，并使用 mimix 模块中的 run_interactive 函数获取医疗诊断结果。这段代码的主要功能是将用户输入的内容翻译成中文，获取诊断结果后再将其翻译回用户的原始语言。

当用户输入一个查询时，ChatTranslator会检测输入的语言，将其翻译成中文，然后运行医疗诊断模型。在得到诊断结果后，它会将每个结果翻译回用户的原始语言。这样，用户就可以用自己的语言接收医疗诊断信息。

## 用户界面 UI

这是初始的用户界面，系统会提示用户选择一张图片并进行预测。

![用户界面示例图片](https://github.com/whossssssss/ML/blob/google-colab/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-11-12%20191311.png)

当模型接收到一张图片（支持常见的图片格式，如 jpg, jpeg, png 等），界面会对图像进行预测。

![用户界面示例图片](https://github.com/whossssssss/ML/blob/google-colab/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-11-12%20191324.png)
![用户界面示例图片](https://github.com/whossssssss/ML/blob/google-colab/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-11-12%20191331.png)
![用户界面示例图片](https://github.com/whossssssss/ML/blob/google-colab/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-11-12%20191800.png)
![用户界面示例图片](https://github.com/whossssssss/ML/blob/google-colab/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-11-12%20191807.png)

以下是动图展示:
![Example Image](https://github.com/whossssssss/ML/blob/google-colab/2378fe0a-ae7c-4874-beed-58958a718585.gif)

## 文本对话模型训练细节

该模型是基于Transformer的编码-解码（enc-dec）架构构建的。这个模型具有216百万个参数、12层、768的模型尺寸（d_model），并使用12个注意力头（n_heads）。训练数据包含270万个样本，数据大小为1.38GB。

其中训练模型的数据集来自于“Huatuo-26M”，这是一个大规模的中文医疗问答数据集。该数据集从多个来源收集而来：

- 在线医疗咨询网站：从一个名为“QianwenHealth”的在线医疗咨询网站上收集了大量的在线咨询记录，这些记录由医学专家提供。每条记录都是一个问答对：患者提出问题，医生给出答案。从这个网站上直接爬取患者的问题和医生的答案，共得到了3167万604个问答对。在去除包含特殊字符和重复对的问答对后，最终得到了2534万1578个问答对​​。
- 医学百科全书：从中文维基百科上收集了疾病和药物相关的8699个百科条目和2736个药品条目，以及从“Qianwen Health”网站上爬取了226432篇高质量的医学文章。通过对这些文章进行结构化处理，将每篇文章分为标题-段落对，然后基于这些标题设计模板，将每个标题转换成一个可以由相应段落回答的问题。最终，基于这些标题和模板，生成了问答对​​。
- 医学知识库：从几个现有的医学知识库中提取了医学问答对。这些知识库包括CPubMed-KG（一个基于中国医学会大规模医学文献数据的中文医学文献知识图谱）、39Health-KG和Xywy-KG（两个开源知识图谱）。从这些知识库中清洗和合并实体及其之间的关系，最终得到了798444个问答对​​。

“Huatuo-26M”数据集涵盖了从真实医疗咨询、医学百科到专业医学知识库的多种数据源，这使得数据集不仅规模庞大，而且内容丰富，覆盖了医学领域的广泛话题和知识点。这样的数据集为中文医疗问答模型的训练提供了坚实的基础​​。


###### 医疗诊断（chat）
该医疗问答模型使用了来自mimix库的med_base_conf权重文件以及med.base.model模型，并基于本地语料库以及测试数据进行相应的优化。

医疗问答的内容大部分将以中医的视角去诊断，例如“气滞血淤”，“固本培元”等，同时所开具的处方同样大部分也会采用中药或者中成药以及食物疗法等方式去实现，例如“小活络丹，四消丸”等中成药或者“平时可以多吃点胡萝卜,海带,百合等食物,来治疗肝胆湿热”等等，具有鲜明的中医特色。

在本地语料库二次训练的基础上，保留原本中医诊断以及处方的同时，也增加了一些西医的处方，例如“局部使用氯霉素滴眼液点眼来治疗结膜炎”，“滴左氧氟沙星滴眼液进行治疗角膜炎”等等，使得诊断结果更加准确以及有针对性，同时治疗方案也多元化及有效。

同时，用户可根据自行选择需要相应的语言进行问答，其回答使用的语言会基于用户提问使用的语言进行调整，对用户使用更加友好。
###### 请注意，医疗诊断模型仅仅有参考作用，不能代替医生做出诊断，具体详细的诊断资料请前往医院进行治疗。

以下为医疗诊断模型的运行示例：

![用户界面示例图片](https://github.com/whossssssss/ML/blob/google-colab/show_2.gif)

