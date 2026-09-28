### Task 4 Radix Cache 与前缀复用
### 1. 核心目标：理解 SGLang 最具特色的优化——RadixAttention。

### 2. 理论和源码学习
    2.1 （1）Radix Tree 数据结构 （2）前缀共享的原理、（3）为什么多轮对话和 Few-shot 场景受益最大
    2.2  Overlap Scheduling： 理解 Overlap Scheduling 如何隐藏 CPU 调度开销，将其与 GPU 计算重叠
    2.3 阅读 minisgl 中 Radix Cache 的实现，理解 KV Cache 如何在前缀级别复用
### 3. 动手任务
    3.1 设计一个实验：同一前缀的多个请求 vs 不同前缀的多个请求，对比吞吐量差异

### 4. 打卡任务
    4.1 2.1 + 2.2 说明
    4.2  3.1 截图
    4.3  Radix Cache 复用效果实验报告

### 打卡学习任务说明

Mini-SGLang 是 SGLang 的轻量版实现，约 5,000 行 Python 代码，保留了 Radix Cache、Chunked Prefill、Overlap Scheduling、Tensor Parallelism 等核心特性，适合理解现代 LLM 服务系统的工程实现。仅支持 Linux（x86_64/aarch64），Windows 需使用 WSL2。
### ===打卡截图要求 请仔细阅读===

微信群截图具体要求："两步走” 与“三要素”

第一步： github 指定issue链接中，上传测试通过截图，作为打卡；

第二步：然后把自己打卡截图发到群里。 微信群截图包括（1）issue 标题 （2） GitHub ID 和（3） 微信群昵称清晰可见