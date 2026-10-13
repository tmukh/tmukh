<div id="header" align="center">
  <img src="https://media.giphy.com/media/tFGBovr5CtfWt7MtqK/giphy.gif" width="100"/>
<div id="badges">
<a href="https://www.linkedin.com/in/tarik-abu-mukh-753779231/">
  <img src="https://img.shields.io/badge/LinkedIn-blue?style=for-the-badge&logo=linkedin&logoColor=black" alt="LinkedIn"/>
 </a>
 <a href="https://takodana.dev">
  <img src="https://img.shields.io/badge/takodana.dev-0b7285?style=for-the-badge&logo=firefoxbrowser&logoColor=white" alt="takodana.dev"/>
  </a>
  <br>
<img src="https://komarev.com/ghpvc/?username=tmukh&style=flat-square&color=blue" alt=""/>
</div>

</div>
<h1>
  Hello there
  <img src="https://media.giphy.com/media/xTiIzJSKB4l7xTouE8/giphy.gif" width="100px"/>
</h1>

I'm Tarik, a platform engineer from Germany :de:!

### About me

- I build infrastructure and then run it in public <img src="https://media.giphy.com/media/tAjb5pyCEBhEb8jWxC/giphy.gif" width="30px">
- I'm heading for **DevOps / SRE**, with a side interest in actually *serving* models rather than just calling them
- I still love the behind-the-scenes stuff — it's just that "behind the scenes" now means clusters, GitOps and the question of why the graph went flat at 3am
- Finishing my **M.Sc. Informatik at TU Berlin** (thesis done, one attendance colloquium to go). Before that, B.Sc. at RPTU Kaiserslautern
- Everything I build ends up at **[takodana.dev](https://takodana.dev)** — projects, build logs and write-ups
- I am a book worm 📚, you can see a list of my current and planned books here: <a href="https://www.goodreads.com/user/show/154602339-tarik"> <img src= "https://img.shields.io/badge/G-My%20goodreads-yellowgreen" width="80px" alt="Join me in reading!"> </a>
- Fun fact: I can solve a Rubik's cube in 10.23 seconds
- 📫 How you can reach me: [![Linkedin Badge](https://img.shields.io/badge/-Tarik-blue?style=flat&logo=Linkedin&logoColor=white)](https://www.linkedin.com/in/tarik-abu-mukh-753779231)

---

### 🔭 What I'm building

Four repos, all public, all actually running. Links go to the live thing, not a screenshot.

#### [glasswing](https://github.com/tmukh/glasswing) · [try it in your browser →](https://takodana.dev/projects/glasswing/)
A small language model you can watch think.

A Llama-style transformer (RMSNorm, RoPE, SwiGLU, GQA — 15.7M params) that I trained on TinyStories, plus an inference engine I wrote **from scratch in Rust** with no ML framework and my own safetensors reader. CI checks it tensor-by-tensor against the PyTorch reference — all 78 traced tensors to 1e-4 — so the Rust, the WASM and the Python all emit identical greedy text.

- Trained in **3h38m on one RTX 3060 Ti**: 40k steps, 1.31B tokens, val loss **1.182**, no overfitting
- Compiles to a **288 KB WebAssembly** engine running ~300 tok/s in the browser, with 31.5 MB f16 weights cached at Cloudflare's edge
- I went looking for a circuit and found one: two previous-token heads (L3H3, L3H1) feeding an induction head (L4H4). Ablating them hurts copying — loss 1.40 → 1.59, where three random heads only reach 1.42. **On ordinary stories the circuit costs about as much as random heads, and [the write-up says so](https://takodana.dev/writing/glasswing-induction-heads/)**
- You can toggle the circuit off in the lab and regenerate with the same seed. The story changes

It also [serves SmolLM2-135M](https://glasswing.takodana.dev) on the same engine — a Rust HTTP server with SSE streaming, per-IP rate limiting, a concurrency cap and Prometheus TTFT metrics, on a distroless signed image. CPU-only on my own cluster, so it's slow on purpose.

#### [homelab-dev](https://github.com/tmukh/homelab-dev)
The cluster everything above runs on, and the reason I can talk about operations instead of theory.

Single-node **k3s** where nothing changes except through Git: **Argo CD** app-of-apps managing itself, and a **shared Helm chart I wrote** that the apps deploy from. Plus **CloudNativePG** with nightly backups and a restore I actually tested row-for-row, **Prometheus / Grafana / Alertmanager / Loki**, SLOs with multiwindow burn-rate alerts, Sealed Secrets, a Cloudflare Tunnel for public routes, and Trivy + Syft SBOM + keyless cosign in the pipeline. There's a second environment in AWS built with Terraform — a personal lab on the free plan, not production.

Three incidents so far, including my favourite: an alert that fired because the metrics *stopped*.

#### [night-sky-digest](https://github.com/tmukh/night-sky-digest) · [live →](https://digest.takodana.dev)
Retrieval over **51,282 astro-ph abstracts**, harvested from arXiv over OAI-PMH.

Hybrid search — Postgres full-text and **pgvector** HNSW fused with reciprocal rank fusion, bge-m3 embeddings via Ollama on a local GPU. The part I'm proudest of is the evaluation: 80 queries (60 EN / 20 DE) graded by two LLM judges with a tie-break, then a 30-item human audit at **κ = 0.81**. Hybrid reaches **nDCG@10 0.72** against 0.69 semantic-only and 0.34 lexical-only, and a frozen snapshot guards it as a CI regression gate. Traced end-to-end with Langfuse. Personal project, one user.

#### [takodana.dev](https://github.com/tmukh/takodana.dev) · [visit →](https://takodana.dev)
My site: a 3D orrery of my projects, case studies, build logs and essays. Next.js static export with three.js, deployed to the cluster by Argo CD like everything else.

<details>
<summary>🗄️ Older things, including my thesis</summary>

- **[Fainder-Redone](https://github.com/tmukh/Fainder-Redone)** — my M.Sc. thesis at TU Berlin's DIMA group (1.7): reimplemented Fainder's query phase in **Rust** and measured it with hardware performance counters. **1.34× to 22.7× faster** than the Python reference depending on dataset size, through data compression and hardware-conscious engineering
- **[application-tracker](https://github.com/tmukh/application-tracker)** — because job hunting is itself a data problem. Runs on the cluster with a local LLM doing the classification
- **[codingCheatingDetection](https://github.com/tmukh/codingCheatingDetection)** — conventional and LLM-based cheating detection
- **[ds2dc](https://github.com/tmukh/ds2dc)** — turning unstructured data lakes into data containers (B.Sc. era)
- **[nand2tetris](https://github.com/tmukh/nand2tetris)**, **[boids-pygame](https://github.com/tmukh/boids-pygame)** — building things to understand them, which is the whole pattern really

</details>

---

### 🧰 What I work with

![Rust](https://img.shields.io/badge/Rust-000000?style=for-the-badge&logo=rust&logoColor=white)
![Python](https://img.shields.io/badge/Python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Bash](https://img.shields.io/badge/Bash-4EAA25?style=for-the-badge&logo=gnubash&logoColor=white)

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Argo CD](https://img.shields.io/badge/Argo%20CD-EF7B4D?style=for-the-badge&logo=argo&logoColor=white)
![Helm](https://img.shields.io/badge/Helm-0F1689?style=for-the-badge&logo=helm&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=for-the-badge&logo=terraform&logoColor=white)
![Ansible](https://img.shields.io/badge/Ansible-EE0000?style=for-the-badge&logo=ansible&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)

![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=grafana&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)

<img src="https://img.shields.io/github/last-commit/tmukh/tmukh?color=blue">
