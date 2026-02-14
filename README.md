# LexBench: Construction Regulatory Compliance Benchmark

This repository contains the dataset, raw model outputs, visual assets, and evaluation logs for the research paper: **"Lex: A Neuro-Symbolic Compound AI System for Resource-Efficient Construction Compliance"**.

The goal of LexBench is to provide full transparency into the **deterministic reasoning** capabilities of the LEX system and to demonstrate its architecture for safety-critical engineering domains, where probabilistic hallucinations are unacceptable.

---

## 📂 Repository Structure

### 🏗️ `/Core-benchmark/`
The primary evaluation data for the **LEX-10 benchmark** — a set of 10 adversarial engineering queries analyzed in the paper.

- **`LEX-10_eng.pdf` / `LEX-10_ru.pdf`**: The core benchmark queries in English and Russian, covering scenarios in structural integrity, Arctic safety protocols, and chemical constraints.
- **`bundle_for_input.pdf`**: The anonymized data bundle provided to the *LLM-as-a-Judge*. It contains queries, expert ground truths, and the responses from four distinct strategies in randomized order to ensure a blind evaluation.
- **`keys for position.pdf`**: The mapping key used to de-anonymize the results, linking "Model A, B, C, D" to their respective strategies for each query.
- **`LLM-as-a-Judge_evaluation.pdf`**: The final scores and summarized reasoning provided by **Gemini 3 Pro** based on a weighted rubric (Correctness, Safety, Citability).

### 🔬 `/Extended_pool/`
Broader research materials and raw diagnostic data.

- **`Bench 28.pdf` / `Bench 28_eng.pdf`**: An expanded pool of 28 complex regulatory queries used to test the scalability of the knowledge graph.
- **`LLM-as-judge-keys.pdf`**: Full, raw evaluation logs (**100+ pages**). This document provides the complete chain-of-thought of the Judge model. 
  - *Note: Primary reasoning in these logs is conducted in Russian to maintain the highest precision regarding national technical standards (GOST/SP).*

Visualizations of the underlying system architecture and data scale.

- **`meta_graph.png`**: The ontological schema of the Knowledge Graph, showing how Documents, Norms, Tables, and Images are interconnected.
- **`RU-code_graph.png`**: A visualization of the **1.1M-edge graph** covering the Russian national construction regulatory corpus.
- **`DBC_graph.png`**: A visualization of the **Dubai Building Code** graph, demonstrating jurisdiction-agnostic scalability.

### 📄 Raw Data & Samples
- **`SP_430_parsed.json`**: The structured dataset containing extracted entities, relations, and semantic metadata used to populate the Knowledge Graph.
- **`СП 430.1325800.2018.md`**: A "Gold Standard" sample of a parsed normative document.
  - *Context:* This is the Russian federal code for "MONOLITHIC STRUCTURAL SYSTEMS" 
  - *Significance:* It demonstrates how our pipeline converts unstructured PDF text into machine-readable Markdown, preserving hierarchical headers and tabular data before graph ingestion.

*Note: Images from SP 430 parsed using PaddleOCR-VL and located in /imgs folder.

---

## 🧠 System & Methodology

### 9-Step Agentic Pipeline
LEX implements a "System 2" thinking process designed for high-stakes environments:
1. **Query Decomposition**: Rewriting input into atomic sub-tasks.
2. **Hybrid Retrieval**: Combining vector embeddings with strict keyword matching.
3. **Topological Expansion**: Traversing graph edges (`:REFERS_TO`, `:HAS_TABLE`) to find hidden dependencies.
4. **Gap Detection**: An iterative loop that checks for context sufficiency and triggers follow-up retrievals.
5. **Constrained Synthesis**: Final answer generation grounded strictly in retrieved graph nodes.

### Scoring Rubric
System performance was evaluated along three primary dimensions:
- **Correctness (40%)**: Accuracy of the engineering solution.
- **Safety (30%)**: Adherence to mandatory safety prohibitions.
- **Citability (30%)**: Verifiability of references. 
- **Hallucination Penalty**: Any citation of a non-existent clause resulted in an **automatic score of 0** for the Citability dimension.

---

## 📺 Demonstration
A video walkthrough of the LEX system interface (built with Gradio), showing real-time reasoning traces and global scalability (switching between Dubai and Russian codes), is available in **`demo.mp4`**.

---

## ✍️ Authors
- **Petr Tymofieiev** — AI Talent Hub, ITMO University.
- **Ilya Makarov** — AIRI / ISP RAS / ITMO University.

---

### Citation
If you use this benchmark or the LEX architecture in your research, please cite:
*(Citation details will be updated upon IJCAI 2026 publication)*
