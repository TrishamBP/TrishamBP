<!--
  GitHub profile README for TrishamBP.
  To publish: copy this file to the TrishamBP/TrishamBP repository as README.md.

  External images are optional. Each block marked OPTIONAL can be deleted
  without breaking the layout. No JavaScript, no custom CSS; GitHub strips both.
-->

<div align="center">

<h1>Trisham Bharat Patil</h1>

<code>forward-deployed ai engineer</code> · <code>ai systems</code> · <code>physical ai</code>

<br><br>

<!-- OPTIONAL: animated typing line (readme-typing-svg, demolab). Delete this <img> to remove. -->
<img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=500&size=15&duration=3200&pause=1100&color=22D3EE&center=true&vCenter=true&width=680&height=28&lines=from+attention+kernels+to+agent+memory+to+sensor+fusion;making+inference+faster+%2F+agents+more+reliable+%2F+machines+more+aware;read+the+paper+%E2%86%92+derive+the+math+%E2%86%92+build+it+%E2%86%92+measure+it" alt="Animated line: from attention kernels to agent memory to sensor fusion; making inference faster, agents more reliable and machines more aware; read the paper, derive the math, build it, measure it." />

<br>

<a href="https://trishampatil.com"><img src="https://img.shields.io/badge/lab_notebook-trishampatil.com-22d3ee?style=flat-square&labelColor=0b1220" alt="Website: trishampatil.com"></a>
<a href="https://trishampatil.com/newsletter/"><img src="https://img.shields.io/badge/newsletter-The_Weekly_Tech_Brew-8b5cf6?style=flat-square&labelColor=0b1220" alt="Newsletter: The Weekly Tech Brew"></a>
<a href="https://www.linkedin.com/in/trishampatil/"><img src="https://img.shields.io/badge/linkedin-trishampatil-3b82f6?style=flat-square&labelColor=0b1220" alt="LinkedIn: trishampatil"></a>
<a href="https://huggingface.co/Trisham97"><img src="https://img.shields.io/badge/hugging_face-Trisham97-64748b?style=flat-square&labelColor=0b1220" alt="Hugging Face: Trisham97"></a>

</div>

<br>

> **Engineering intelligence for digital and physical systems.**
>
> I build production AI systems for a living: agentic workflows, retrieval pipelines, and the distributed
> backends that run them on AWS. Most of my own time goes into the layers underneath: how attention
> reads a KV cache, why decode is memory-bound, what an agent should remember. I also study how
> the same ideas carry over to machines that have to perceive and act in the physical world.
> My background is in mechanical engineering, so I tend to think of models as *systems*, with
> state, latency budgets and failure modes.

<br>

## Research Interests

The four areas below are parts of one stack. A model is only useful if it is served efficiently, an
agent is only useful if it can remember and plan, and a robot runs the same perceive, reason and act
loop under real-time limits.

```text
  sense ──────────▶ perceive ─────────▶ remember ────────▶ reason / plan ─────▶ act
  camera · IMU      detection · SLAM    KV cache · RAG     agents · tools       APIs · actuators
  ultrasonic        tracking · fusion   hierarchical mem   orchestration        control loops
        └───────────────────────────────── runs on ───────────────────────────────┘
               inference runtime  (batching · paged KV · speculative decoding)
               distributed infra  (parallelism · queues · observability · edge)
```

<table>
<tr>
<td width="50%" valign="top">

#### `01` &nbsp; Agentic Intelligence

How do agents keep the *right* context? Memory hierarchies (working, episodic and long-term),
context engineering under a fixed token budget, planning and parallel tool execution, MCP-based
tool interfaces, human-in-the-loop control points, and evaluation methods that catch regressions
before users do.

</td>
<td width="50%" valign="top">

#### `02` &nbsp; LLM Systems & Inference

Where does serving time go? Prefill is compute-bound and decode is memory-bandwidth-bound. I study
KV cache lifecycle and placement, PagedAttention, continuous batching, prefill/decode
disaggregation, TTFT/TBT trade-offs under SLOs, MHA → MQA → GQA → MLA, quantization, and
speculative decoding.

</td>
</tr>
<tr>
<td width="50%" valign="top">

#### `03` &nbsp; Robotics & Physical AI

What changes when inference has a deadline and the input is a noisy sensor stream? Camera-based
perception and tracking, visual SLAM, IMU and sensor fusion, path planning, edge inference on
microcontroller-class hardware, and world models. My mechanical engineering background
(control, aerodynamics, numerical PDEs) is the starting point.

</td>
<td width="50%" valign="top">

#### `04` &nbsp; Distributed Systems & Infrastructure

How do you make all of this reliable? Tensor, pipeline and data parallelism (Megatron-LM, FSDP),
collective communication, async orchestration with queues and workers, event-driven pipelines,
and the observability work (traces, metrics, evals) that turns a demo into a dependable system.

</td>
</tr>
</table>

<br>

## `/currently-exploring`

Active work, not finished results. Checked items have a public repository.

```text
~/explorations $ ls -l
[x] transformer-components-in-rust   BPE tokenizer, RoPE (done) → attention, KV cache (next)
[x] speculative-decoding             EAGLE-3 draft model + lossless verification, CPU-scale
[x] agent-kv-cache-engineering       semantic labels for dropped context on an SGLang backend
[ ] llm-inference-engines            vLLM · SGLang · TensorRT-LLM · FlashInfer · Mooncake internals
[ ] kv-cache-optimization            prefix reuse, hierarchical placement, SLO-aware eviction
[ ] agent-memory-architectures       hierarchical / episodic memory, retrieval-as-memory
[ ] multi-agent-planning             plan-and-execute, parallel function calling, harness design
[ ] visual-slam + sensor-fusion      camera + IMU state estimation (reading and notes)
[ ] edge-intelligence                ESP32-S3 drone platform, Arduino UNO R4 (bench experiments)
```

<br>

## Selected Engineering Projects

<sub>All repositories below are public. Where a project builds on someone else's work, it says so.</sub>

#### ◆ AI Systems & LLM Infrastructure

| Project | What it is | Problem it addresses | Stack |
|:--|:--|:--|:--|
| [**AKV-Sem**](https://github.com/TrishamBP/AKV-Sem) | Extension of [AKV](https://github.com/thu-nics/AKV) (Fu et al.). I designed and added the semantic-awareness policy. | When agents drop KV entries, they forget *why* a path failed. Labelled verdicts (failed, irrelevant, resolved) outlive the evicted cache and prevent repeated dead ends. | Python · SGLang · KV cache ops |
| [**eagle_3**](https://github.com/TrishamBP/eagle_3) | From-scratch reconstruction of EAGLE-3 speculative decoding. | Reproduces the draft model, multi-layer feature fusion and training-time test, and checks lossless verification token by token. Correctness only; no speed claims. | PyTorch · Transformers |
| [**llm-router**](https://github.com/TrishamBP/llm-router) | Hybrid neural network + XGBoost router across Claude model tiers. | Chooses a model per query by trading predicted quality against latency and cost. [Model on HF](https://huggingface.co/Trisham97/llm-complexity-router). | PyTorch · XGBoost · scikit-learn |
| [**llm_db** (LARQL)](https://github.com/TrishamBP/llm_db) | Exposes transformer FFN activations through a SQL-like query interface. | Treats a model's internals as a queryable knowledge graph for interpretability, on consumer GPUs. | PyTorch hooks · Docker |

#### ◆ Agentic AI & Memory

| Project | What it is | Problem it addresses | Stack |
|:--|:--|:--|:--|
| [**harness-engineering**](https://github.com/TrishamBP/harness-engineering) | Reference agent harness plus 36 architecture diagrams, a companion to a long-form article. | Breaks down the runtime of production coding agents (tool loop, context, permissions, memory) into small parts with tests. | Python (stdlib only) · 79 tests |
| [**ThermaCore**](https://github.com/TrishamBP/ThermaCore) | AMD ACT III hackathon: data-center thermal operations backend. | Streams simulated telemetry, forecasts inlet temperature, and runs a LangGraph multi-agent recommender that can only recommend, never actuate. | Kafka · XGBoost · LangGraph · FastAPI |
| [**Autopay-Recovery-Voice-Agent**](https://github.com/TrishamBP/Autopay-Recovery-Voice-Agent) | Simulated payment-recovery voice agent backend. | Human-in-the-loop by construction: no call is placed without explicit approval. Includes state machines, an event ledger and an audit log. | FastAPI · SQLAlchemy async · Twilio (mock) |
| [**ai_career_twin**](https://github.com/TrishamBP/ai_career_twin) | Grounded, source-cited Q&A over my career documents. [Live demo](https://huggingface.co/spaces/Trisham97/AI-Career-Twin). | Hybrid retrieval, cross-encoder reranking and hallucination controls applied to a small personal corpus. | RAG · hybrid search · reranking |

#### ◆ Robotics & Physical AI

| Project | What it is | Problem it addresses | Stack |
|:--|:--|:--|:--|
| [**football_analysis_yolo**](https://github.com/TrishamBP/football_analysis_yolo) | Broadcast video turned into frame-level tracking analytics. | A perception pipeline: detection → multi-object tracking → camera-motion compensation → perspective transform → speed and distance. The same building blocks used in robot perception. | YOLOv8 · ByteTrack · OpenCV · PyTorch |
| [**Rescue-Disaster-AStar-PathPlanning**](https://github.com/TrishamBP/Rescue-Disaster-AStar-PathPlanning) | A* path planning for rescue scenarios. | Grid search and heuristic planning, a first step toward autonomous navigation. | Python · Jupyter |
| [**Wave**](https://github.com/TrishamBP/Wave-Equation-Solver) / [**Heat**](https://github.com/TrishamBP/1D-2D-Heat-Equation-Solver) solvers | 1D/2D numerical PDE solvers from my master's coursework. | Finite-difference simulation of physical systems, the numerical foundation for physics-informed ML. | Python · NumPy |
| `embedded-systems-journey` | **Placeholder.** The [repository](https://github.com/TrishamBP/embedded-systems-journey) exists but has no commits yet. | Will document ESP32-S3 drone platform and Arduino UNO R4 experiments with HC-SR04, NRF24L01+, IMU and camera modules. | ESP32-S3 · Arduino · C/C++ · Rust (planned) |

#### ◆ Systems Programming & Rust

| Project | What it is | Problem it addresses | Stack |
|:--|:--|:--|:--|
| [**rust-bpe-tokenizer**](https://github.com/TrishamBP/rust-bpe-tokenizer) | Byte-level BPE tokenizer: training, encoding, decoding and a versioned binary model format. | Understanding tokenization exactly, without a library hiding the details. Measured before optimized. | Rust (std only) · no `unsafe` · 65 tests |
| [**rust_rope**](https://github.com/TrishamBP/rust_rope) | Rotary Position Embeddings from scratch, including real-model layouts and long-context scaling. | Validated against PyTorch on 288 cases, with CPU benchmarks. | Rust 2024 · 0 deps · 323 tests |
| [**tiny_gpt_llm**](https://github.com/TrishamBP/tiny_gpt_llm) | Roughly 3M-parameter GPT trained from first principles. | Connects every line of code to the concept it implements: causal attention, blocks, training loop. | PyTorch |

#### ◆ Full-Stack AI Applications

| Project | What it is | Problem it addresses | Stack |
|:--|:--|:--|:--|
| [**IBM_Bob_2.0_Hackathon**](https://github.com/TrishamBP/IBM_Bob_2.0_Hackathon) | ACME Onboard: enterprise onboarding portal plus knowledge assistant. | LLM-assisted structural chunking validated against the source text, department-aware routing, and hybrid-search RAG with citations. | FastAPI · RAG · hybrid search |
| [**drug-information-rag-system**](https://github.com/TrishamBP/drug-information-rag-system) | RAG over FDA drug records. | Turns tabular regulatory data into source-attributed natural-language answers using multi-query retrieval. | LangChain · ChromaDB · OpenAI · Gradio |
| [**fastapi_claude_code_plugin**](https://github.com/TrishamBP/fastapi_claude_code_plugin) | Agent skill that encodes my production FastAPI standards. | Async execution, Pydantic validation, guardrails and RAG/agent layout for AWS ECS Fargate services. | FastAPI · AWS · agent skills |

<br>

## Engineering Philosophy

```text
1. derive before you implement     If I can't write the equation, I don't understand the code yet.
2. profile before you optimize     Know the architecture and where time goes before tuning anything.
3. measure, don't assume           A benchmark beats an intuition. A correctness test beats both.
4. papers → working code           A paper is a hypothesis until it runs on my own machine.
5. reliability is a feature        Real systems have SLOs, retries, audits and humans in the loop.
6. bits meet atoms                 The perceive → reason → act loop doesn't change. The deadlines do.
```

<br>

## Technical Arsenal

<sub>Self-assessed depth: <b>●</b> used in production · <b>◐</b> used in projects · <b>○</b> studying / exploring</sub>

<p>
<img src="https://img.shields.io/badge/Python-0b1220?style=flat-square&logo=python&logoColor=22d3ee" alt="Python">
<img src="https://img.shields.io/badge/TypeScript-0b1220?style=flat-square&logo=typescript&logoColor=22d3ee" alt="TypeScript">
<img src="https://img.shields.io/badge/Rust-0b1220?style=flat-square&logo=rust&logoColor=22d3ee" alt="Rust">
<img src="https://img.shields.io/badge/PyTorch-0b1220?style=flat-square&logo=pytorch&logoColor=22d3ee" alt="PyTorch">
<img src="https://img.shields.io/badge/FastAPI-0b1220?style=flat-square&logo=fastapi&logoColor=22d3ee" alt="FastAPI">
<img src="https://img.shields.io/badge/AWS-0b1220?style=flat-square&logo=amazonwebservices&logoColor=22d3ee" alt="AWS">
<img src="https://img.shields.io/badge/Docker-0b1220?style=flat-square&logo=docker&logoColor=22d3ee" alt="Docker">
<img src="https://img.shields.io/badge/ESP32-0b1220?style=flat-square&logo=espressif&logoColor=22d3ee" alt="ESP32">
</p>

| Domain | Tools |
|:--|:--|
| **Languages** | ● Python · ● TypeScript / JavaScript · ◐ Rust · ○ C / C++ |
| **AI / ML** | ◐ PyTorch · ◐ Hugging Face · ◐ scikit-learn · ◐ XGBoost · ◐ TensorFlow · ◐ OpenCV / YOLO |
| **LLM Infrastructure** | ◐ SGLang · ○ vLLM · ○ TensorRT-LLM · ○ FlashInfer · ○ Mooncake · ○ Megatron-LM · ○ FSDP · ○ Triton |
| **Agentic Systems** | ● LangGraph · ● LangChain · ● AWS Bedrock · ● OpenAI APIs · ◐ DSPy · ◐ MCP · ◐ ChromaDB · ◐ FAISS · ◐ Pinecone · ◐ Weaviate |
| **Backend** | ● FastAPI · ◐ Django · ◐ Node.js / Express |
| **Frontend** | ◐ React · ◐ Next.js · ◐ Tailwind CSS |
| **Cloud & DevOps** | ● AWS · ● Docker · ◐ Kubernetes · ◐ Terraform · ◐ Jenkins · ◐ Nginx · ● CI/CD |
| **Robotics & Embedded** | ○ ESP32-S3 · ○ Arduino UNO R4 · ○ HC-SR04 · ○ NRF24L01+ · ○ IMU / camera modules · ○ Visual SLAM |
| **Databases & Messaging** | ● PostgreSQL · ● Redis · ◐ MongoDB · ◐ MySQL · ◐ RabbitMQ · ◐ Kafka |
| **Observability** | ◐ LangSmith · ◐ Prometheus · ◐ Grafana · ◐ Jaeger · ◐ Sentry |

<!-- Review the ●/◐/○ markers before publishing. They are an honest first draft, so adjust them to match your experience. -->

<br>

## Research Notes & Technical Writing

My lab notebook is at **[trishampatil.com](https://trishampatil.com)**. It holds paper implementations,
long-form systems notes, and the weekly newsletter **[The Weekly Tech Brew](https://trishampatil.com/newsletter/)**.

<table>
<tr>
<td width="50%" valign="top">

**Research write-ups**
- [SLO-Aware KV-Cache Management for Large-Scale LLM Serving](https://trishampatil.com/research-articles/2026-08-30-slo-aware-kv-cache-management-large-scale-llm-serving/)
- [LambdaNER-Bench: Serverless NER Inference on AWS Lambda](https://trishampatil.com/research-articles/2026-10-06-lambdaner-bench-serverless-ner-inference-benchmark-aws-lambda/)

**Inference & distributed systems**
- [LLM Inference Optimization](https://trishampatil.com/2026/04/19/llm-inference-optimization/)
- [Megatron-LM: Tensor, Pipeline & Data Parallelism](https://trishampatil.com/ai%20engineering/2026/09/09/megatron-lm-tensor-pipeline-data-parallelism/)
- [Collective Communication: All-Reduce, All-Gather](https://trishampatil.com/ai%20engineering/2026/09/20/collective-communication-tpu-gpu-clusters-all-reduce-all-gather/)
- [GPU MatMul Kernels on Hopper Tensor Cores](https://trishampatil.com/ai%20engineering/2026/09/20/nvidia-gpu-matmul-kernels-hopper-h100-tensor-cores/)

</td>
<td width="50%" valign="top">

**Paper implementations**
- [EAGLE-3 Speculative Decoding](https://trishampatil.com/engineering/eagle-3-speculative-decoding-llm-inference-acceleration/)
- [DistServe: Prefill–Decode Disaggregation](https://trishampatil.com/engineering/distserve-prefill-decode-disaggregation-llm-serving/)
- [Mooncake: KVCache-Centric Serving](https://trishampatil.com/engineering/mooncake-kvcache-centric-architecture-for-serving-llm-chatbot/)
- [DeepSeek-V2: MoE + Multi-head Latent Attention](https://trishampatil.com/engineering/deepseek-v2-mixture-of-experts-mla-language-model/)
- [Harness Engineering](https://trishampatil.com/engineering/harness-engineering/)

**Agents · memory · physical AI**
- [Context Engineering: Loop & Graph Engineering](https://trishampatil.com/ai%20engineering/2026/08/22/context-engineering-loop-graph-engineering/)
- [HiMeS: Hippocampus-Inspired Agent Memory](https://trishampatil.com/engineering/himes-hippocampus-inspired-agent-memory-system/)
- [Physical Intelligence Lab: SLAM notes](https://trishampatil.com/physical-intelligence-lab/slam/)

</td>
</tr>
</table>

<br>

## GitHub Activity

<!--
  OPTIONAL: delete this whole section to remove every third-party stats service.
  Checked 2026-11-11: streak-stats.demolab.com responded (200).
  The public github-readme-stats and activity-graph instances were down (503 / 402), so they are
  commented out below. Self-host them on Vercel before enabling:
    https://github.com/anuraghazra/github-readme-stats#deploy-on-your-own
    https://github.com/Ashutosh00710/github-readme-activity-graph
-->

<div align="center">

<img src="https://streak-stats.demolab.com?user=TrishamBP&background=0b1220&border=1e293b&stroke=1e293b&ring=22d3ee&fire=8b5cf6&currStreakNum=e2e8f0&sideNums=e2e8f0&currStreakLabel=22d3ee&sideLabels=94a3b8&dates=64748b&hide_border=true" alt="GitHub contribution streak for TrishamBP" width="560">

<!--
<img src="https://<your-instance>.vercel.app/api?username=TrishamBP&show_icons=true&hide_border=true&bg_color=0b1220&title_color=22d3ee&icon_color=8b5cf6&text_color=cbd5e1" alt="GitHub statistics for TrishamBP" height="165">
<img src="https://<your-instance>.vercel.app/api/top-langs/?username=TrishamBP&layout=compact&hide_border=true&bg_color=0b1220&title_color=22d3ee&text_color=cbd5e1" alt="Most used languages in TrishamBP repositories" height="165">
-->

</div>

<br>

## Connect

<div align="center">

[`github/TrishamBP`](https://github.com/TrishamBP) &nbsp;·&nbsp;
[`linkedin/trishampatil`](https://www.linkedin.com/in/trishampatil/) &nbsp;·&nbsp;
[`trishampatil.com`](https://trishampatil.com) &nbsp;·&nbsp;
[`newsletter`](https://trishampatil.com/newsletter/)

<br>

<sub><code>perceive → remember → reason → act</code> · in software and in hardware</sub>

</div>
