# MiniGPT-4

这个项目是来自阿卜杜拉国王科技大学的几位博士做的，目标是实现图像对话能力，虽然这个项目名字叫做MiniGPT-4，但是实际上跟GPT-4没有任何关系，只是为了吸引眼球而已。

GitHub：https://github.com/Vision-CAIR/MiniGPT-4

在线体验：https://minigpt-4.github.io/

项目作者认为，GPT-4 所实现的多模态能力，在以前的视觉 - 语言模型中很少见，因此认为，GPT-4 先进的多模态生成能力，主要原因在于利用了更先进的大型语言模型。

为了验证这一想法，团队成员将一个冻结的视觉编码器与一个冻结的 Vicuna 进行对齐，造出了 MiniGPT-4。

这个项目提供了预训练模型，可以直接使用，但是模型效果不是很好，如果想要训练自己的模型，需要自己准备数据集。并且需要使用 A100 GPU，因为模型太大了，不然训练不起来。目前我们没有 A100 GPU，所以暂时无法训练。等有钱了再说。

所以这部分的文档我只写如何使用预训练模型。等有钱了再写训练模型的文档。

值得注意的是，预训练模型效果真的的很差，所以这个项目目前的意义不大。即使使用作者的在线体验（作者自己训练的模型），也是很差的效果。

## 安装
 
### 1.准备代码和环境
```
git clone https://github.com/Vision-CAIR/MiniGPT-4.git
cd MiniGPT-4
conda env create -f environment.yml
conda activate minigpt4
```
### 2.预训练的Vicuna权重

要准备 Vicuna 的权重，首先从(https://huggingface.co/lmsys/vicuna-13b-delta-v0)下载 Vicuna 的增量权重。如果你安装了 git-lfs ( https://git-lfs.com )，这可以通过
    ```
    git lfs install
    git clone https://huggingface.co/lmsys/vicuna-13b-delta-v0
    ```
然后，您需要按照[here](https://huggingface.co/docs/transformers/main/model_doc/llama) HuggingFace 提供的说明或从 Internet 获取 HuggingFace 格式的原始 LLAMA-13B 权重。

当这两个配重准备就绪后，我们就可以使用 Vicuna 团队的工具来创建真正的工作配重。首先，通过以下方式安装与 v0 Vicuna 兼容的库

```
pip install git+https://github.com/lm-sys/FastChat.git@v0.1.10
```
然后，运行以下命令来创建最终的工作权重
```
python -m fastchat.model.apply_delta --base /path/to/llama-13b-hf/  --target /path/to/save/working/vicuna/weight/  --delta /path/to/vicuna-13b-delta-v0/
```

然后，在minigpt4.yaml第 16行的模型配置文件中设置 vicuna 权重的路径 。
### 3.下载预训练模型

要使用作者的预训练模型，请在[here](https://drive.google.com/file/d/1a4zLvaiDBr-36pasffmgpvH5P7CKmpze/view?usp=share_link)下载预训练模型。然后，在第 11 行的eval_configs/minigpt4_eval.yaml中的评估配置文件中设置预训练模型的路径。

### 4.在本地启动演示
通过运行在本地计算机上试用演示demo.py

```
python demo.py --cfg-path eval_configs/minigpt4_eval.yaml  --gpu-id 0
```