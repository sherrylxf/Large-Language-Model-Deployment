

## 大模型部署实践

---

### 一、下载大模型到本地

#### 1. 切换目录到 `/mnt/data`

```bash
cd /mnt/data
```

#### 2. 下载一个大模型

```bash
# 只下载一个模型，避免存储不足
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

cat > run_qwen_cpu.py
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


### ✅ Bonus：使用 `modelscope` 下载和加载模型（自动下载权重）

如果你更喜欢自动化方式，也可以这样写 `run_qwen_cpu.py`：

```python
from modelscope import AutoModelForCausalLM, AutoTokenizer
from modelscope.utils.constant import Tasks

model = AutoModelForCausalLM.from_pretrained('qwen/Qwen-7B-Chat', task=Tasks.text_generation)
tokenizer = AutoTokenizer.from_pretrained('qwen/Qwen-7B-Chat', revision='v1.0.4')

input_text = "你好，介绍一下你自己"
inputs = tokenizer(input_text, return_tensors="pt")
outputs = model.generate(**inputs, max_new_tokens=100)
print(tokenizer.decode(outputs[0], skip_special_tokens=True))
```

并运行：

```bash
python run_qwen_cpu.py
```

---

## ✅ 总结（你只需记住这几点）：

| 步骤      | 命令示例                                    |
| ------- | --------------------------------------- |
| 1. 下载模型 | `cd /mnt/data && git clone https://...` |
| 2. 安装依赖 | `pip install transformers==4.33.3 ...`  |
| 3. 写脚本  | `nano run_qwen_cpu.py`                  |
| 4. 运行模型 | `python run_qwen_cpu.py`                |

---

如果你愿意，我也可以直接为你生成一个完整的 `run_all.sh` 脚本，一键完成安装、下载、推理流程。需要我帮你生成吗？
