# AI_deepseek
Stuffs on the AI and deepseek
![image](https://github.com/user-attachments/assets/64a600bb-89d1-4165-9237-b16b9cabae8d)

**人生的意义是什么？是大自然演变的一环而已，何必纠结。是碗中餐、身边人和眼中景。加油做自己喜欢的事吧，想清楚每天要做的事，实现它们！改变世界，从一点点开始！！**

## deepseek官方网址[deepseek.ai](https://www.deepseek.com/) and [deepseek chat](https://chat.deepseek.com/)
License
The model weights are licensed under the MIT License. DeepSeek-R1 series support commercial use, allow for any modifications and derivative works, including, but not limited to, distillation for training other LLMs. Please note that:
The Qwen distilled models are derived from Qwen-2.5 series, which are originally licensed under Apache 2.0 License, and now finetuned with 800k samples curated with DeepSeek-R1.
The Llama 8B distilled model is derived from Llama3.1-8B-Base and is originally licensed under llama3.1 license.
The Llama 70B distilled model is derived from Llama3.3-70B-Instruct and is originally licensed under llama3.3 license.

![image](https://github.com/user-attachments/assets/1ddfae73-5f84-4bda-8a7f-a7467fabc037)


## deepseek本地部署
### 使用ollama环境：
   I. 下载ollama软件，官网[ollama](https://ollama.com/)，最新版本0.5.7。在win11系统，注意默认的安装路径不能修改，不得不安装在C盘。
   
   II. 为了避免C盘过于臃肿，更改ollama安装模型时的默认存储路径(C:\Users%username%.ollama\models)。变更方法：设置系统环境变量：OLLAMA_MODELS=D:\ollama\models。这里假设把下载的模型都存在了这里。

   在ollama官网浏览deepseek构建的[models](https://ollama.com/library/deepseek-r1)：
   DeepSeek’s first-generation reasoning models, achieving performance comparable to OpenAI-o1 across math, code, and reasoning tasks.

**Models**
DeepSeek-R1
```
ollama run deepseek-r1:671b
```
具有671B参数量。理论上需要350GB以上显存/内存才能部署FD4量化版本。也许需要1T内存+2个H00可以本地部署。
Distilled models
DeepSeek team has demonstrated that the reasoning patterns of larger models can be distilled into smaller models, resulting in better performance compared to the reasoning patterns discovered through RL on small models.
Below are the models created via fine-tuning against several dense models widely used in the research community using reasoning data generated by DeepSeek-R1. The evaluation results demonstrate that the distilled smaller dense models perform exceptionally well on benchmarks.

DeepSeek-R1-Distill-Qwen-1.5B
```
ollama run deepseek-r1:1.5b
```
DeepSeek-R1-Distill-Qwen-7B
```
ollama run deepseek-r1:7b
```
DeepSeek-R1-Distill-Llama-8B
```
ollama run deepseek-r1:8b
```
DeepSeek-R1-Distill-Qwen-14B
```
ollama run deepseek-r1:14b
```
MyLaptop@MacBook air (8GB) can run this version.
DeepSeek-R1-Distill-Qwen-32B
```
ollama run deepseek-r1:32b
```
MyPC@home with 3090 (24GB) can run this version.
DeepSeek-R1-Distill-Llama-70B
```
ollama run deepseek-r1:70b
```

####模型的优化性能

1、创建或编辑配置文件：

vim ~/.ollama/config

2、添加配置信息（~/.ollama/config）：
```
{
  "gpu_layers": 35,         // GPU层数，根据显卡性能调整
  "cpu_threads": 6,         // CPU线程数，建议设为CPU核心数
  "batch_size": 512,        // 批处理大小，影响内存使用
  "context_size": 4096      // 上下文窗口大小，影响对话长度
}
```
3、重启ollama服务生效
```
ollama stop 
ollama start
ollama run deepseek-r1:7b
```
4、性能调优建议：

如果电脑发烫/卡顿：减小 gpu_layers 和 batch_size
如果内存不足：减小 batch_size
如果需要更长对话：增加 context_size（会消耗更多内存）
cpu_threads 建议设置为实际CPU核心数-2
5、性能参考

内存占用：~12-14GB
首次加载：30-60秒
对话延迟：1-3秒
上下文窗口：4096 tokens

#### 验证优化生效

1、在模型对话界面输入一个较长的问题

请给我详细解释一下量子计算的基本原理，要求回答内容超过500字

2、查看CPU和内存使用

top
3、检查是否生效的判断标准：

GPU使用率应该显著（如果有独立显卡）
CPU线程数应该是配置的6个
长文本响应时不会出现内存溢出
对话上下文能保持4096个token左右


### 使用[cherry studio](https://cherry-studio.com/)


### 使用[LM Studio](https://lmstudio.ai/)

### [AnthingLLM](https://anythingllm.com/)

### [MaxKB](https://maxkb.cn/)
  仅支持Linux，在win平台需要借助docker安装。

### [Open WebUI](https://docs.openwebui.com/)

内网穿透的常用软件主要有NPS（好像很久没有更新了，作者弃坑了），FRP；好像都需要购买一个服务器提供商。
