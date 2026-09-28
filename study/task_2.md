### Task 2 KV Cache 与 Paged Attention
### 1. 核心目标：理解推理引擎最核心的内存管理机制。

### 2. 理论和源码学习
     2.1 KV Cache 的内存占用公式、Paged KV Cache 的块分配原理
     2.2  阅读 minisgl.kvcache 模块，理解 BlockAllocator 的分配/释放逻辑
     2.3  理解 FlashAttentionBackend 和 FlashInferBackend 的接口抽象

### 3. 动手任务
      3.1 计算不同序列长度下 Llama-3-8B 的 KV Cache 大小，验证与代码中的分配逻辑一致

### 4.  打卡任务
**打卡选择三选一：**(1)4.1+4.2 ； (2) 4.1+4.2 + 4.3 或者 4.1+4.2 + 4.4 （3）4.1+4.2 + 4.3 + 4.4  

      4.1 最小打卡（对应2.1） KV Cache 计算，Paged KV Cache 内存布局示意图
      4.2 最小打卡（对应3.1）3.1 截图 
      4.3  学有余力增项1 （对应2.2）BlockAllocator 的分配/释放逻辑
      4.4  学有余力增项2 （对应2.3） FlashAttentionBackend 和 FlashInferBackend 的接口抽象




### 打卡学习任务说明
Mini-SGLang 是 SGLang 的轻量版实现，约 5,000 行 Python 代码，保留了 Radix Cache、Chunked Prefill、Overlap Scheduling、Tensor Parallelism 等核心特性，适合理解现代 LLM 服务系统的工程实现。仅支持 Linux（x86_64/aarch64），Windows 需使用 WSL2。

### ===打卡截图要求 请仔细阅读===

微信群截图具体要求："两步走” 与“三要素”

第一步： github 指定issue链接中，上传测试通过截图，作为打卡；

第二步：然后把自己打卡截图发到群里。 微信群截图包括（1）issue 标题 （2） GitHub ID 和（3） 微信群昵称清晰可见