### Task 3 调度器与 Continuous Batching
### 1. 核心目标：理解请求如何在引擎中被调度和执行。

### 2. 理论和源码学习
    2.1 阅读 minisgl.engine 中的 Engine 类，理解 Prefill 队列和 Decode 队列的调度策略
    2.2 Continuous Batching： 理解“请求动态加入/退出批次”的机制，以及它相比 Static Batching 的优势
    2.3 Chunked Prefill：理解 Chunked Prefill 如何控制长上下文场景下的峰值内存占用

### 3. 动手任务
    3.1 启动服务，用不同长度的 prompt 并发请求，观察调度行为（可通过日志）

### 4. 打卡任务
    4.1 2.2+2.3 说明
    4.2 调度流程时序图 
    4.3  3.1 截图
    4.4 Continuous Batching 与 Static Batching 的对比分析

### 打卡学习任务说明

Mini-SGLang 是 SGLang 的轻量版实现，约 5,000 行 Python 代码，保留了 Radix Cache、Chunked Prefill、Overlap Scheduling、Tensor Parallelism 等核心特性，适合理解现代 LLM 服务系统的工程实现。仅支持 Linux（x86_64/aarch64），Windows 需使用 WSL2。
### ===打卡截图要求 请仔细阅读===

微信群截图具体要求："两步走” 与“三要素”

第一步： github 指定issue链接中，上传测试通过截图，作为打卡；

第二步：然后把自己打卡截图发到群里。 微信群截图包括（1）issue 标题 （2） GitHub ID 和（3） 微信群昵称清晰可见