---
permalink: /
title: ""
excerpt: ""
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

<span class='anchor' id='about-me'></span>
# About Me

I am currently an M.S. student in Computer Science at the [University of Sydney](https://www.sydney.edu.au/), advised by [Prof. Nguyen H. Tran](https://www.sydney.edu.au/engineering/about/our-people/academic-staff/nguyen-tran.html). I earned my B.Eng (2024) in Cyberspace Security from the [Harbin Institute of Technology (HIT)](http://en.hit.edu.cn/).

My research sits at the intersection of **systems and machine learning**, with a current focus on **efficient LLM inference** — specifically, scheduling, speculative decoding, and resource allocation in edge / distributed settings. My recent master's thesis ([SpecSpeed](#research-experience)) develops a coupled-budget formulation for multi-client speculative decoding, with a provably optimal scheduler under discrete concavity.

### Research Interests
- **LLM Inference Systems** — speculative decoding, multi-client scheduling, verifier-budget coupling
- **Edge Intelligence** — cloud-edge collaborative inference, age-of-information aware scheduling
- **Applied Optimization** — gradient-based scheduling, KKT analysis, fluid-model approximation


<span class='anchor' id='news'></span>
# 🔥 News
- *2026.05*: 🎓 Submitted **105-page master's thesis** on multi-client SSD scheduling — main result: a capped greedy scheduler that beats GoodSpeed by up to **+316%** throughput and is provably globally optimal on **228/228** calibrated grid points.
- *2025.07*: 🏆 Won the **Most Creative Award (2nd place)** at *CodingFest* for *Forget Me Not*, a wearable assistive device for memory care.


<span class='anchor' id='education'></span>
# 📖 Education

- **2024.09 — Present** &nbsp;&nbsp; **M.S. in Computer Science**, University of Sydney  
  &nbsp;&nbsp;&nbsp;&nbsp;<span style="font-size: 0.9em;">WAM: **84.18 / 100**</span>

- **2020.09 — 2024.06** &nbsp;&nbsp; **B.Eng in Cyberspace Security**, Harbin Institute of Technology  
  &nbsp;&nbsp;&nbsp;&nbsp;<span style="font-size: 0.9em;">WAM: **80 / 100**</span>


<span class='anchor' id='research-experience'></span>
# 💻 Research Experience

### **SpecSpeed** — Multi-Client Speculative Decoding Scheduling under Verifier-Budget Coupling
*Master's Thesis · University of Sydney · 09/2025 — 05/2026*

- Formulated the **multi-client SSD scheduling problem** under a shared cloud verifier budget; **proved unimodality** of the SSD service curve $\mu^{SSD}(k)$ and showed that GoodSpeed-style "more-is-better" schedulers exhibit up to **123% throughput loss** under capacity pressure.
- Designed **CappedSSDScheduler**, a peak-detecting greedy algorithm that stops allocating at marginal-utility sign-flip. Across **63 calibrated configurations**, achieves **+316% throughput vs GoodSpeed** and **+266% vs an uncapped SSD-aware ablation**, isolating the contributions of *capping* and *correct service-curve modeling*.
- Cross-validated optimality with a **DP + MILP oracle (HiGHS)** double-check: greedy = DP = MILP on **228/228 grid points** (gap = 0) under discrete concavity; constructed a non-concave counterexample to delimit the theoretical boundary.
- Delivered a **105-page thesis** (9 chapters + 2 appendices) covering KKT analysis, $a/b/T_V$ timing calibration, honest negative findings ($k^\ast(B)$ non-monotonicity), and stated limitations.

### **G-FAST** — Freshness-Aware Speculative Decoding for Real-Time Edge Inference
*Group collaboration · in submission, SIGMETRICS / INFOCOM 2026 · 01/2026 — 04/2026*

- Contributed to **early-stage literature review** bridging Age of Information (AoI) and speculative decoding scheduling; helped articulate the "Stale Compute" problem framing.
- **Reproduced the GoodSpeed throughput-optimal baseline** used as the principal comparison in G-FAST experiments; assisted with simulation setup and figure generation.
- Joined design discussions on the **Timely Goodput** metric and the shape of the freshness-efficiency function $\Phi(\Delta)$, as well as the trade-offs of the **LIFO-and-Drop** pipeline vs FIFO.

### **SpecDiff** — Cloud-Edge Speculative Decoding with Diffusion Drafters
*Collaboration with a PhD researcher · 11/2025 — Present*

- Co-designed a cloud-edge LLM inference architecture: edge devices use a **diffusion-model drafter** $Q_i$ to generate $K$ candidate sequences; the cloud verifier processes only the selected best draft, reducing communication overhead.
- Implemented **gradient-based distributed scheduling** that dynamically manages per-client draft length $S_i(t)$ and best-of-$K$ parameter $K_i(t)$; built an online estimator that updates effective acceptance rate $\alpha^i(t)$ via exponential smoothing.
- Simulated multi-client allocation under different cloud verifier budgets $C$, analyzing proportional fairness vs aggregate log-utility trade-offs.


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

### **Histopathology Image Classification with SVM, MLP, and CNN**
*Course Project · 03/2025 — 06/2025*

Compared SVM, MLP, and CNN on **PathMNIST** for multi-class colorectal histology classification, applying normalization, PCA, one-hot encoding, and data augmentation to improve generalization.

- **RBF-kernel SVM** with stratified cross-validation + grid/random search, balancing overfitting vs cost via PCA — **67.1%** test accuracy.
- **Deep MLP** with KerasTuner-driven architecture search, structured Dropout, batch norm, and activation sweeps — **80.4%** test accuracy.
- **CNN pipeline** tailored to small-format histology images with custom conv/pool stages — **81.8%** test accuracy, demonstrating strong spatial-feature robustness.


<span class='anchor' id='honors-awards'></span>
# 🏆 Honors & Awards

- *2025*: **Most Creative Award (2nd Place)**, CodingFest — *Forget Me Not* project


<span class='anchor' id='skills'></span>
# 🧰 Skills

- **Languages**: Python, Java, C++, JavaScript, SQL
- **LLM & Inference**: Speculative Decoding, Model Deployment (Qwen / Llama), FastAPI
- **ML & NLP**: PyTorch, Scikit-learn, CNN, SVM, KeyBERT, Sparse Coding, FAISS
- **Systems & Tooling**: Linux, Git, simulation modeling, LaTeX


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
