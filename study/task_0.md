### Task 0 推理基础与 SGLang 定位
### 1. 核心目标：理解 LLM 推理的本质问题，建立系统视角。

### 2. 环境安装与整体了解
     2.1 Quick Start https://github.com/sgl-project/mini-sglang
     2.2 阅读 Mini-SGLang 的 Code Structure 文档，理解 core（Req/Batch/Context）、engine、layers、models、kvcache 等模块的职责划分 https://mintlify.wiki/sgl-project/mini-sglang/api/code-structure  

### 3.动手任务
      3.1 安装环境`uv venv + uv pip install -e .` ,   跑通 python -m minisgl.server 启动基础服务


### 4.  打卡任务
**打卡选择三选一：**(1)4.1+4.2 ； (2) 4.1+4.2 + 4.3 或者 4.1+4.2 + 4.4 （3）4.1+4.2 + 4.3 + 4.4

      4.1 最小打卡（对应2.2）  职责理解图
      4.2 最小打卡  (对应3.1）  截图
      4.3 学有余力增项1  Sglang 与vllm对比
      4.4 学有余力增项2  推理基础笔记：用自己的话解释 KV Cache、Prefill/Decode、内存墙

### 打卡学习任务说明
Mini-SGLang 是 SGLang 的轻量版实现，约 5,000 行 Python 代码，保留了 Radix Cache、Chunked Prefill、Overlap Scheduling、Tensor Parallelism 等核心特性，适合理解现代 LLM 服务系统的工程实现。仅支持 Linux（x86_64/aarch64），Windows 需使用 WSL2。

### ===打卡截图要求 请仔细阅读===

微信群截图具体要求："两步走” 与“三要素”

第一步： github 指定issue链接中，上传测试通过截图，作为打卡；

第二步：然后把自己打卡截图发到群里。 微信群截图包括（1）issue 标题 （2） GitHub ID 和（3） 微信群昵称清晰可见