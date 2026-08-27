---
permalink: /
lang: zh
title: ""
excerpt: ""
author_profile: true
redirect_from:
  - /about/
  - /about.html
---

<span class='anchor' id='about-me'></span>
# 关于我

我是[悉尼大学](https://www.sydney.edu.au/)计算机科学硕士研究生（数据科学与人工智能方向），师从 [Prof. Nguyen H. Tran](https://www.sydney.edu.au/engineering/about/our-people/academic-staff/nguyen-tran.html)。本科毕业于[哈尔滨工业大学](http://en.hit.edu.cn/)网络空间安全专业（2024）。

我的研究在**系统与机器学习**的交叉地带，当前聚焦**高效大模型推理**：推测解码、多客户端调度与边缘/分布式场景下的资源分配。硕士论文 [SpecSpeed](#research-experience) 提出多客户端推测解码的耦合预算建模，并给出可证明最优的调度器；相关工作已投稿 NeurIPS 2026 MLForSys Workshop，完整版准备投 ICLR 2027。研究之外我也动手实践大模型推理系统工程（vLLM 源码剖析与 benchmark、INT8/INT4 量化、Triton 算子），见 [vllm_serving](https://github.com/pablo-labo/vllm_serving)。

### 研究方向
- **大模型推理系统** — 推测解码、多客户端调度、verifier 预算耦合
- **边缘智能** — 云边协同推理、信息年龄感知调度
- **应用优化** — 梯度调度、KKT 分析、流体模型近似


<span class='anchor' id='news'></span>
# 🔥 新闻
- *2026.08*：📄 论文 **"Less Is More: Non-Monotone Service under Coupled Fan-out Budgets in Multi-Client SSD"** 投稿 **MLForSys Workshop（NeurIPS 2026）**；完整版准备投 **ICLR 2027**。
- *2026.06–08*：🛠️ 开源 [vllm_serving](https://github.com/pablo-labo/vllm_serving) — 大模型推理系统工程实践：vLLM 源码级剖析与 benchmark、INT8/INT4 量化、Triton 算子（GEMM / FlashAttention）。
- *2026.05*：🎓 提交 **105 页硕士论文**（成绩 89/100，多客户端推测解码调度）：提出的 CappedSSD 调度器在 **270/270** 网格点上与 DP + MILP 最优解一致，单客户端 goodput 最高提升 **+94.2%**。
- *2025.07*：🏆 Forget Me Not 智慧养老穿戴设备获 *CodingFest* **最具创意奖（亚军）**。


<span class='anchor' id='education'></span>
# 📖 教育背景

- **2024.09 — 2026.11（预计）** &nbsp;&nbsp; **悉尼大学**，计算机科学硕士（数据科学与人工智能方向）  
  &nbsp;&nbsp;&nbsp;&nbsp;<span style="font-size: 0.9em;">加权平均分：**85.94 / 100**（High Distinction）</span>

- **2020.09 — 2024.06** &nbsp;&nbsp; **哈尔滨工业大学**，网络空间安全理学学士  
  &nbsp;&nbsp;&nbsp;&nbsp;<span style="font-size: 0.9em;">加权平均分：**80 / 100**</span>


<span class='anchor' id='research-experience'></span>
# 💻 研究与工程经历

### **SpecSpeed** — 多客户端推测式解码调度（SSD）
*硕士学位论文 · 悉尼大学 · 2025.09 — 2026.05 · [代码](https://github.com/pablo-labo/ssd_specspeed)*

- 针对多个客户端共享同一云端 verifier 的推测解码系统，研究「草稿长度如何分配」这一调度问题：将草稿长度与共享验证预算建模为各客户端的 **goodput（有效产出吞吐）**，发现单客户端下的调度直觉在共享预算时失效——各 drafter 的服务曲线存在**非单调区间**（草稿加长后 goodput 反而下降）。
- 从双客户端 KKT 条件中拆出资源耦合项，设计 **CappedSSD** 与 **SSDGreedy** 两种调度策略；在 **270/270 个异构配置**上与 DP 及 HiGHS MILP 最优解的目标值和资源分配完全一致，并构造非凹反例验证普通贪心可产生 **15.8%** 的目标值差距。
- 配置 **Qwen3-8B/0.6B** 在 Alpaca、GSM8K 上运行校准 simulator：Alpaca 的 C=12、5,184 组配置中，**GoodSpeed** 基线有 **51.6%** 的资源分配与 SSD 感知最优解不同；严格优先级反转样本中，SSD 感知分配使单客户端 goodput **平均提升 +59.7%、最高 +94.2%**。
- 论文版已投稿 **MLForSys Workshop（NeurIPS 2026）**，完整版准备投 **ICLR 2027**。

### **大模型推理系统工程实践** — vLLM / 量化 / Triton
*个人项目 · 2026.06 — 2026.08 · [代码](https://github.com/pablo-labo/vllm_serving)*

- **vLLM 部署与源码剖析**：在 RTX 4090 上用 vLLM 部署 Qwen3-1.7B，源码级梳理一条请求的完整执行链（Scheduler → PagedAttention → prefill/decode → Model Runner）；并发 1→16 时吞吐 223→2869 tok/s（**12.8×**）、TPOT 仅 4.4→5.2 ms；关闭 continuous batching 对照下吞吐停在 224 tok/s，印证 decode 阶段受显存带宽限制、混批通过复用权重读取带宽放大吞吐。
- **模型量化**：实现 per-channel INT8 与 per-group INT4（对称/非对称），并与 bitsandbytes INT8/NF4 对比：INT8 perplexity 与 FP16 持平（16.42 vs 16.67）、权重降 64%；无校准 INT4 退化明显（16.67→22.29），印证 AWQ/GPTQ 等校准手段的必要性；vLLM 在线 4bit 量化单请求吞吐 **+52%**（340 vs 223 tok/s）。
- **Triton 算子**：实现 tiled GEMM 达 **cuBLAS 的 97–101%**（4096³ 上 138.8 TFLOPS）；FlashAttention 前向（tiling + online softmax，含 causal）相对朴素实现提速 **7.4×**、峰值显存 2248→200 MB，达 torch 原生 SDPA 的 **63–88%**。

### **G-FAST** — 面向实时边缘推理的信息新鲜度感知推测解码
*团队合作 · 投稿中（SIGMETRICS / INFOCOM 2026）· 2026.01 — 2026.04*

- 综述信息年龄（AoI）文献并将其与推测解码调度建立联系，协助构建 "Stale Compute" 问题框架。
- 复现 **GoodSpeed 吞吐最优基线**用于 G-FAST 对比，支持仿真搭建与结果可视化。
- 参与 **Timely Goodput** 指标设计，包括新鲜度-效率函数 $\Phi(\Delta)$ 的形态与 **LIFO-and-Drop** 和 FIFO 之间的权衡。

### **SpecDiff** — 基于扩散模型草稿器的云边推测解码
*与博士研究员合作 · 2025.11 — 至今*

- 共同设计云边 LLM 推理架构：边缘设备用**扩散模型 drafter** $Q_i$ 生成 $K$ 个候选序列，云端 verifier 只处理选出的最优草稿，降低通信开销。
- 实现**基于梯度的分布式调度**，动态管理各客户端草稿长度 $S_i(t)$ 与 best-of-$K$ 参数 $K_i(t)$；搭建在线估计器，通过指数平滑更新有效接受率 $\alpha^i(t)$ 并跟踪吞吐 $X_i(t)$。
- 仿真不同云端 verifier 预算 $C$ 下的多客户端资源分配，分析比例公平与聚合对数效用权衡。


<span class='anchor' id='selected-projects'></span>
# 🛠️ 项目

### **Forget Me Not** — 智慧养老智能穿戴设备 &nbsp;<span style="color: #c00000;">🏆 CodingFest 2025 最具创意奖（亚军）</span>
*2025.04 — 2025.07*

一款智能穿戴设备：通过摄像头捕捉失忆患者前方的物体并提供语音交互；设备经智能手机与远程后端通信，实现人脸识别辅助记忆、跌倒检测，以及由 LLM 生成的记忆刺激文本。

- 开发后端 `agent.py` 模块，由 LLM API 统一完成功能选择与工具编排，将多任务请求自动调度到人脸识别、跌倒检测、记忆刺激等工具链；身份识别用 **FAISS** 对人脸向量做余弦相似度检索；定制提示词链驱动本地大模型生成记忆刺激文本并合成语音。
- 负责**本地模型部署**与后端 API 设计：选用轻量级 **Qwen 0.6B** 满足端侧性能约束，通过 FastAPI 集成对话交互与记忆刺激接口。

### **EduCareer Bridge** — 网络安全课程与就业技能衔接
*假期研究实习 · 2025.06 — 2025.07*

端到端流水线对齐教育内容与网络安全就业市场需求：爬取 Glassdoor 与 Seek 的岗位数据，用 SVM 与随机森林聚类为六个类别。

- 对每个类别用 **KeyBERT** 提取代表性技能关键词并构建目标技能集；通过**稀疏编码**将课程描述映射到岗位技能集，输出匹配/错配技能并生成个性化建议。
- 负责网页爬虫、后端映射逻辑与本地 LLM 部署。


<span class='anchor' id='honors-awards'></span>
# 🏆 荣誉与奖项

- *2025*：CodingFest **最具创意奖（亚军）** — *Forget Me Not* 项目


<span class='anchor' id='skills'></span>
# 🧰 技能

- **编程语言**：Python、Java、C++、JavaScript、SQL
- **大模型与推理**：vLLM、推测解码、KV Cache、模型量化（INT8/INT4）、模型部署（Qwen / Llama）
- **系统与工具**：Triton、Linux、Git、FastAPI、仿真建模、LaTeX
- **机器学习与 NLP**：PyTorch、Scikit-learn、FAISS、KeyBERT、稀疏编码


<span class='anchor' id='contact'></span>
# ✉️ 联系方式

- **邮箱**：[rche0265@uni.sydney.edu.au](mailto:rche0265@uni.sydney.edu.au) · [erojar2001@gmail.com](mailto:erojar2001@gmail.com)
- **电话**：(+86) 186-6085-0974
- **GitHub**：[github.com/pablo-labo](https://github.com/pablo-labo)


<hr style="margin-top: 3em;">

<div id="footer" style="text-align: center; font-size: 0.9em; color: #666;">
  &copy; 2026 程荣邦（Rongbang Cheng）<br><br>
  <span style="color: #888;">
    总访问量：<span id="busuanzi_value_site_pv"></span> | 
    访客数：<span id="busuanzi_value_site_uv"></span>
  </span>
</div>

<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
