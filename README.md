LexBench: Construction Regulatory Compliance Benchmark
This repository contains the dataset, raw model outputs, visual assets, and evaluation logs for the research paper: "Lex: A Neuro-Symbolic Compound AI System for Resource-Efficient Construction Compliance".
The goal of LexBench is to provide full transparency into the deterministic reasoning capabilities of the LEX system and demonstrate its superiority over standard probabilistic LLM approaches in safety-critical engineering domains.
📂 Repository Structure
🏗️ /Core-benchmark/
The primary evaluation data for the LEX-10 benchmark — 10 adversarial engineering queries analyzed in the paper.
LEX-10_eng.pdf / LEX-10_ru.pdf: Core queries covering structural integrity, Arctic safety, and chemical constraints.
bundle_for_input.pdf: Anonymized responses from four strategies (LEX, Naive RAG, Zero-shot, Full-Context) provided to the Judge.
keys for position.pdf: De-anonymization key for evaluation results.
LLM-as-a-Judge_evaluation.pdf: Final scores and reasoning provided by Gemini 3 Pro.
🔬 /Extended_pool/
Broader research materials and diagnostic data.
Bench 28.pdf / Bench 28_eng.pdf: 28 complex queries used to test graph scalability.
LLM-as-judge-keys.pdf: 100+ pages of raw evaluation logs containing the Judge's complete Chain-of-Thought (CoT).
🖼️ /imgs/
Visual proof of the system's underlying architecture.
meta_graph.png: The ontological schema showing how Documents, Norms, Tables, and Images are interconnected.
RU-code_graph.png: Visualization of the 1.1M-edge graph covering the Russian national regulatory corpus.
DBC_graph.png: Visualization of the Dubai Building Code graph, proving jurisdiction-agnostic scalability.
📄 Raw Data & Samples
data_v4.json: The structured dataset containing extracted entities, relations, and semantic metadata used to populate the Knowledge Graph.
СП 430.1325800.2018.md: A "Gold Standard" sample of a parsed normative document.
Context: This is the Russian federal code for "Industrial Floors" (Promyshlennye poly).
Significance: It demonstrates how our pipeline converts messy, unstructured PDF text into machine-readable Markdown, preserving hierarchical headers, tabular data, and cross-standard references before ingestion into Neo4j.
🧠 System & Methodology
9-Step Agentic Pipeline
Lex implements a "System 2" thinking process:
Query Decomposition (Rewriting into atomic tasks).
Hybrid Retrieval (Combining Vector embeddings + Keyword search).
Topological Expansion (Traversing graph edges: :REFERS_TO, :HAS_TABLE).
Gap Detection (Iterative self-correction for missing context).
Constrained Synthesis (Deterministic answer generation grounded in graph nodes).
Scoring Rubric
Correctness (40%): Accuracy against expert ground truth.
Safety (30%): Adherence to mandatory safety prohibitions.
Citability (30%): Verifiability of references (Hallucination Penalty applied: any fake citation = 0 score).
📺 Demonstration
A video walkthrough of the reasoning engine, showing the Gradio interface and real-time graph traversal, is available in demo.mp4.
