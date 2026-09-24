### Task 1 模型层与核心数据结构
### 1. 核心目标：理解 Mini-SGLang 如何加载和表示一个 LLM。

### 2. 源码学习
      2.1  阅读 minisgl.models：BaseLLMModel 基类、ModelConfig 配置、Llama/Qwen2/Qwen3 的具体实现
      2.2  阅读 minisgl.layers：VocabParallelEmbedding、LinearQKVMerged、RMSNorm、RoPE、AttentionLayer 
      2.3  阅读 minisgl.core：Req（请求状态）、Batch（批处理分组）、Context（全局推理上下文）

### 3. 动手任务
      3.1 写一个最小脚本，加载 Llama 模型并打印其配置，手动构造一个 Req 和 Batch


### 4.  打卡任务
**打卡选择三选一：**(1)4.1+4.2 ； (2) 4.1+4.2 + 4.3 或者 4.1+4.2 + 4.4 （3）4.1+4.2 + 4.3 + 4.4

      4.1 最小打卡 （对应2.1，2.3）运行截图，说明基类的使用、配置使用，说明请求、batch 如何构造
      4.2 最小打卡 （对应3.1）运行截图，
      4.3 学习有余力打卡1 ： 模型加载流程图 
      4.4 学习有余力打卡2 ： 核心数据结构关系图

### 打卡学习任务说明
Mini-SGLang 是 SGLang 的轻量版实现，约 5,000 行 Python 代码，保留了 Radix Cache、Chunked Prefill、Overlap Scheduling、Tensor Parallelism 等核心特性，适合理解现代 LLM 服务系统的工程实现。仅支持 Linux（x86_64/aarch64），Windows 需使用 WSL2。

### ===打卡截图要求 请仔细阅读===

微信群截图具体要求："两步走” 与“三要素”

第一步： github 指定issue链接中，上传测试通过截图，作为打卡；

第二步：然后把自己打卡截图发到群里。 微信群截图包括（1）issue 标题 （2） GitHub ID 和（3） 微信群昵称清晰可见