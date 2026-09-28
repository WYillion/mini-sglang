# Task 0 打卡 — 推理基础与 SGLang 定位

## 打卡信息

- **身份**：Ing（已结束前置学习阶段）
- **环境**：本地 NVIDIA
- **系统**：WSL2 (Ubuntu 26.04 LTS)
- **关键信息**：RTX 3060 Laptop 6GB / Driver 591.74 / CUDA 13.1 / WSL2 内 nvcc 12.4.131
- **已完成**：4.1 职责理解图 ✅；4.2 服务启动截图（待跑通后补充）
- **当前卡点**：`uv pip install -e .` 依赖安装进行中（sgl_kernel/flashinfer 编译 CUDA 内核）

---

## 4.1 职责理解图（对应 2.2 Code Structure）

### 核心数据结构（core.py）

| 结构 | 职责 | 关键字段 |
|------|------|---------|
| `SamplingParams` | 采样参数 | temperature, top_k, top_p, max_tokens |
| `Req` | 单个推理请求的状态 | input_ids, cached_len, output_len, cache_handle |
| `Batch` | 一批请求（区分 prefill/decode 两阶段） | reqs, phase, input_ids, positions, attn_metadata |
| `Context` | 全局上下文（贯穿一次 forward） | page_table, attn_backend, kv_cache, moe_backend |

### 模块职责划分

| 模块 | 职责 |
|------|------|
| `core.py` | 核心数据结构 Req / Batch / Context / SamplingParams |
| `server/` | HTTP 服务（FastAPI 接收请求、返回响应） |
| `llm/` | LLM 高层接口（构造请求、管理生成循环） |
| `scheduler/` | 调度器（组装 Batch、管理 prefill/decode 两阶段、缓存分配、页表） |
| `engine/` | 核心引擎（执行 forward、采样、计算图） |
| `models/` | 模型实现（llama / mistral / qwen2 / qwen3 / qwen3_moe） |
| `layers/` | 模型层（linear / attention / norm / rotary / moe / embedding） |
| `attention/` | Attention 后端（FlashAttention / FlashInfer） |
| `kernel/` | CUDA / Triton 内核 |
| `kvcache/` | KV 缓存（radix_cache / mha_pool / naive_cache） |
| `distributed/` | 分布式通信（Tensor Parallelism） |
| `moe/` | MoE 后端 |
| `tokenizer/` | 分词器 |
| `shell.py` | 交互式 shell |

### 数据流图

```
用户请求 (HTTP)
    ↓
server/  ── FastAPI 接收请求
    ↓
llm/  ── 构造 Req (core.py)
    ↓
scheduler/  ── 组装 Batch (prefill / decode 两阶段)
    ├── prefill.py    首次处理 prompt（计算密集）
    ├── decode.py     逐 token 生成（带宽密集）
    ├── cache.py      分配 KV 缓存槽位
    └── table.py      维护页表映射
    ↓
Context  ── 绑定 attn_backend / kv_cache / moe_backend
    ↓
engine/  ── 执行 forward
    ├── models/  ── 模型前向（llama / qwen3 / ...）
    │   └── layers/  ── linear / attention / norm / rotary / moe
    │       └── attention/  ── fa / fi 后端
    │           └── kernel/  ── CUDA / Triton 内核
    └── sample.py  ── 从 logits 采样下一个 token
    ↓
kvcache/  ── radix_cache 存/取 KV（共享前缀复用）
    ↓
生成的 token → 回给用户
```

### 关键机制理解

1. **两阶段调度**：Prefill（计算密集，处理整个 prompt）→ Decode（带宽密集，逐 token 生成），由 scheduler 分别调度
2. **Radix Cache**：`kvcache/radix_cache.py` 用 Radix 树管理 KV，共享前缀的请求复用 KV，减少重复计算
3. **Overlap Scheduling**：CPU 调度与 GPU forward 解耦，隐藏调度开销
4. **Context 贯穿 forward**：Context 把 attn_backend、kv_cache、page_table 绑在一起，layers 通过全局 Context 访问这些对象，避免层层传参

---

## 4.2 服务启动截图（对应 3.1）

**启动命令**（环境装完后执行）：

```bash
cd ~/mini-sglang
source .venv/bin/activate
python -m minisgl --model Qwen/Qwen3-0.6B
```

**状态**：⏳ 依赖安装（`uv pip install -e .`）进行中，待跑通后补充启动成功截图。

**截图要求**（来自 task_0.md）：
1. 在 GitHub 指定 issue 上传测试通过截图
2. 微信群截图含：issue 标题 + GitHub ID + 微信群昵称清晰可见
