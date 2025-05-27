## 大模型部署教程（以Qwen-7B-Chat为例）

---

### 一、下载大模型到本地

#### 1. 切换目录到 `/mnt/data`

```bash
cd /mnt/data
```

#### 2. 下载一个大模型

```bash
git clone https://www.modelscope.cn/qwen/Qwen-7B-Chat.git
```

---

###  二、安装模型运行所需依赖

在 `/mnt/workspace` 目录下执行以下命令：

```bash
cd /mnt/workspace

# 用虚拟环境以避免依赖冲突
python -m venv venv
source venv/bin/activate
pip install -U pip setuptools wheel
apt update && apt install nano -y

# 安装 transformers 4.33.3 和其他依赖
pip install \
  intel-extension-for-transformers==1.4.2 \
  neural-compressor==2.5 \
  transformers==4.33.3 \
  modelscope==1.9.5 \
  pydantic==1.10.13
```

---

### 三、编写运行脚本 `run_qwen_cpu.py`

#### 在 `/mnt/workspace` 目录下，新建一个 Python 文件：

```bash
nano run_qwen_cpu.py
```

#### run_qwen_cpu.py ：

```python
from transformers import AutoTokenizer, AutoModelForCausalLM

# 模型路径（使用你刚刚下载的模型）
model_path = "/mnt/data/Qwen-7B-Chat"

# 加载 tokenizer 和模型
tokenizer = AutoTokenizer.from_pretrained(model_path, trust_remote_code=True)
model = AutoModelForCausalLM.from_pretrained(model_path, trust_remote_code=True)

# 将模型设置为 evaluation 模式（关闭 Dropout）
model.eval()

# 输入一个提示词进行推理
prompt = "你好，请介绍一下你自己。"
inputs = tokenizer(prompt, return_tensors="pt")

# 前向推理
with torch.no_grad():
    outputs = model.generate(**inputs, max_new_tokens=100)

# 输出结果
response = tokenizer.decode(outputs[0], skip_special_tokens=True)
print(response)
```

按下 `Ctrl + O` 保存，`Enter` 确认，`Ctrl + X` 退出编辑器。

---

### 四、运行模型脚本

在终端执行：

```bash
python run_qwen_cpu.py
```

如果你安装了 `torch`，这时就会开始生成回答。

---

## 大模型部Tips：

| 步骤      | 命令示例                                    |
| ------- | --------------------------------------- |
| 1. 下载模型 | `cd /mnt/data && git clone https://...` |
| 2. 安装依赖 | `pip install transformers==4.33.3 ...`  |
| 3. 写脚本  | `nano run_qwen_cpu.py`                  |
| 4. 运行模型 | `python run_qwen_cpu.py`                |

---