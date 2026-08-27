---
permalink: /en/
lang: en
title: ""
excerpt: ""
author_profile: true
---

<span class='anchor' id='about-me'></span>
# About Me

I am currently an M.S. student in Computer Science at the [University of Sydney](https://www.sydney.edu.au/), advised by [Prof. Nguyen H. Tran](https://www.sydney.edu.au/engineering/about/our-people/academic-staff/nguyen-tran.html). I earned my B.Eng (2024) in Cyberspace Security from the [Harbin Institute of Technology (HIT)](http://en.hit.edu.cn/).

My research sits at the intersection of **systems and machine learning**, with a current focus on **efficient LLM inference** — specifically, scheduling, speculative decoding, and resource allocation in edge / distributed settings. My master's thesis ([SpecSpeed](#research-experience)) develops a coupled-budget formulation for multi-client speculative decoding, with a provably optimal scheduler; the work has been submitted to the MLForSys Workshop (NeurIPS 2026), with a full version in preparation for ICLR 2027. Beyond research, I get hands-on with LLM inference systems engineering — vLLM internals and benchmarking, INT8/INT4 quantization, and Triton kernels (see [vllm_serving](https://github.com/pablo-labo/vllm_serving)).

### Research Interests
- **LLM Inference Systems** — speculative decoding, multi-client scheduling, verifier-budget coupling
- **Edge Intelligence** — cloud-edge collaborative inference, age-of-information aware scheduling
- **Applied Optimization** — gradient-based scheduling, KKT analysis, fluid-model approximation


<span class='anchor' id='news'></span>
# 🔥 News
- *2026.08*: 📄 Submitted the paper **"Less Is More: Non-Monotone Service under Coupled Fan-out Budgets in Multi-Client SSD"** to the **MLForSys Workshop (NeurIPS 2026)**; a full version is in preparation for **ICLR 2027**.
- *2026.06–08*: 🛠️ Open-sourced [vllm_serving](https://github.com/pablo-labo/vllm_serving) — hands-on LLM inference systems engineering: vLLM source-level analysis and benchmarking, INT8/INT4 quantization, and Triton kernels (GEMM / FlashAttention).
- *2026.05*: 🎓 Submitted the **105-page master's thesis** (89/100) on multi-client SSD scheduling — a capped greedy scheduler (**CappedSSD**) that matches DP + MILP optimal solutions on **270/270** grid points and improves per-client goodput by up to **+94.2%**.
- *2025.07*: 🏆 Won the **Most Creative Award (2nd place)** at *CodingFest* for *Forget Me Not*, a wearable assistive device for memory care.


<span class='anchor' id='education'></span>
# 📖 Education

- **2024.09 — 2026.11 (expected)** &nbsp;&nbsp; **M.S. in Computer Science** (Data Science & AI), University of Sydney  
  &nbsp;&nbsp;&nbsp;&nbsp;<span style="font-size: 0.9em;">WAM: **85.94 / 100** (High Distinction)</span>

- **2020.09 — 2024.06** &nbsp;&nbsp; **B.Eng in Cyberspace Security**, Harbin Institute of Technology  
  &nbsp;&nbsp;&nbsp;&nbsp;<span style="font-size: 0.9em;">WAM: **80 / 100**</span>


<span class='anchor' id='research-experience'></span>
# 💻 Research & Engineering Experience

### **SpecSpeed** — Multi-Client Speculative Decoding Scheduling under Verifier-Budget Coupling
*Master's Thesis · University of Sydney · 09/2025 — 05/2026 · [Code](https://github.com/pablo-labo/ssd_specspeed)*

- Formulated the **multi-client SSD scheduling problem** under a shared cloud verifier budget, modeling draft lengths and the shared verification budget as per-client **goodput**; showed that single-client scheduling intuition breaks under budget sharing — each drafter's service curve has a **non-monotone region** where longer drafts *reduce* goodput.
- Decomposed the resource-coupling term from two-client KKT conditions to design **CappedSSD** and **SSDGreedy** schedulers; matched the objective values and allocations of **DP and HiGHS MILP optimal solutions on 270/270 heterogeneous configurations**, and constructed a non-concave counterexample where a plain greedy scheduler incurs a **15.8%** objective gap.
- Calibrated simulators with **Qwen3-8B/0.6B** on Alpaca and GSM8K: on 5,184 Alpaca configurations (C=12), the **GoodSpeed** baseline deviates from the SSD-aware optimal allocation in **51.6%** of cases; under strict priority-reversal samples, SSD-aware allocation improves per-client goodput by **+59.7% on average, up to +94.2%**.
- The thesis is packaged into a paper: submitted to the **MLForSys Workshop (NeurIPS 2026)**; a full version is in preparation for **ICLR 2027**.

### **LLM Inference Systems Engineering Practice** — vLLM / Quantization / Triton
*Personal project · 06/2026 — 08/2026 · [Code](https://github.com/pablo-labo/vllm_serving)*

- **vLLM deep-dive & benchmarking**: served Qwen3-1.7B with vLLM on an RTX 4090 and traced a request's full execution path at source level (Scheduler → PagedAttention → prefill/decode → Model Runner); at concurrency 1→16, throughput grows 223→2869 tok/s (**12.8×**) with TPOT only 4.4→5.2 ms, while disabling continuous batching caps throughput at 224 tok/s — confirming decode is memory-bound and batching amplifies throughput by reusing weight-read bandwidth.
- **Model quantization**: implemented per-channel INT8 and per-group INT4 (symmetric/asymmetric) and compared against bitsandbytes INT8/NF4: INT8 matches FP16 perplexity (16.42 vs 16.67) at 64% weight size; uncalibrated INT4 degrades markedly (16.67→22.29), confirming the need for AWQ/GPTQ-style calibration; vLLM online 4-bit serving boosts single-request throughput by **+52%** (340 vs 223 tok/s).
- **Triton kernels**: implemented a tiled GEMM reaching **97–101% of cuBLAS** (138.8 TFLOPS at 4096³) and a FlashAttention forward pass (tiling + online softmax, causal) that is **7.4×** faster than a naive implementation, cutting peak memory 2248→200 MB and reaching **63–88%** of torch's native SDPA.

### **G-FAST** — Freshness-Aware Speculative Decoding for Real-Time Edge Inference
*Group collaboration · in submission, SIGMETRICS / INFOCOM 2026 · 01/2026 — 04/2026*

- Reviewed Age of Information (AoI) literature to connect it with speculative decoding scheduling, helping frame the "Stale Compute" problem.
- Reproduced the **GoodSpeed throughput-optimal baseline** for G-FAST comparisons; supported simulation setup and result visualization.
- Contributed to the design of the **Timely Goodput** metric, including the shape of the freshness-efficiency function $\Phi(\Delta)$ and the trade-off between **LIFO-and-Drop** and FIFO.

### **SpecDiff** — Cloud-Edge Speculative Decoding with Diffusion Drafters
*Collaboration with a PhD researcher · 11/2025 — Present*

- Co-designed a cloud-edge LLM inference architecture: edge devices use a **diffusion-model drafter** $Q_i$ to generate $K$ candidate sequences, while the cloud verifier processes only the selected best draft, reducing communication overhead.
- Implemented **gradient-based distributed scheduling** that dynamically manages per-client draft length $S_i(t)$ and best-of-$K$ parameter $K_i(t)$; built an online estimator that updates effective acceptance rate $\alpha^i(t)$ via exponential smoothing and tracks throughput $X_i(t)$.
- Simulated multi-client resource allocation under different cloud verifier budgets $C$, analyzing proportional fairness and aggregate log-utility trade-offs.


<span class='anchor' id='selected-projects'></span>
# 🛠️ Selected Projects

### **Forget Me Not** — Smart Wearable for Memory Care &nbsp;<span style="color: #c00000;">🏆 Most Creative Award (2nd Place), CodingFest 2025</span>
*04/2025 — 07/2025*

A smart wearable device that captures objects in front of memory-impaired patients and provides voice interaction. The device communicates with a remote backend via smartphone, enabling face-recognition-assisted memory cues, fall detection, and LLM-generated memory stimulation text.

- Built the `agent.py` backend module that orchestrates function selection through LLM API calls; used **FAISS** to compute cosine similarity over vectorized face embeddings for identity recognition; designed custom prompt-chains to drive an on-device LLM that produces memory-stimulation narratives, then converts them to speech.
- Owned **on-device model deployment** and backend API design — selected **Qwen 0.6B** to fit edge performance constraints, integrated via FastAPI for conversational and memory-stimulation endpoints.

### **EduCareer Bridge** — Bridging Cybersecurity Curricula and Job Market Skills
*Vacation Research Internship · 06/2025 — 07/2025*

End-to-end pipeline aligning education content with cybersecurity job-market demand. Crawled job titles and descriptions from Glassdoor and Seek; clustered into six categories using SVM and Random Forest.

- For each category, used **KeyBERT** to extract representative skill keywords and built a target skill set. Mapped course descriptions to job skill sets via **sparse coding**, surfacing matched / mismatched skills and producing personalized recommendations.
- Built the web scraper, backend mapping logic, and the local LLM deployment.


<span class='anchor' id='honors-awards'></span>
# 🏆 Honors & Awards

- *2025*: **Most Creative Award (2nd Place)**, CodingFest — *Forget Me Not* project


<span class='anchor' id='skills'></span>
# 🧰 Skills

- **Languages**: Python, Java, C++, JavaScript, SQL
- **LLM & Inference**: vLLM, Speculative Decoding, KV Cache, Model Quantization (INT8/INT4), Model Deployment (Qwen / Llama)
- **Systems & Tooling**: Triton, Linux, Git, FastAPI, simulation modeling, LaTeX
- **ML & NLP**: PyTorch, Scikit-learn, FAISS, KeyBERT, Sparse Coding


<span class='anchor' id='contact'></span>
# ✉️ Contact

- **Email**: [rche0265@uni.sydney.edu.au](mailto:rche0265@uni.sydney.edu.au) · [erojar2001@gmail.com](mailto:erojar2001@gmail.com)
- **Phone**: (+86) 186-6085-0974
- **GitHub**: [github.com/pablo-labo](https://github.com/pablo-labo)


<hr style="margin-top: 3em;">

<div id="footer" style="text-align: center; font-size: 0.9em; color: #666;">
  &copy; 2026 Rongbang Cheng<br><br>
  <span style="color: #888;">
    Total Views: <span id="busuanzi_value_site_pv"></span> | 
    Unique Visitors: <span id="busuanzi_value_site_uv"></span>
  </span>
</div>

<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
