# LEX-Bench: Construction Regulatory Compliance Benchmark

This repository contains the dataset, raw model outputs, and evaluation logs for the paper: 
**"Lex: A Neuro-Symbolic Compound AI System for Resource-Efficient Construction Compliance"**.

The repository is structured to provide full transparency into the deterministic reasoning capabilities of the LEX system compared to standard probabilistic LLM approaches.

## Repository Structure

### 📂 /Core-benchmark/
This directory contains the primary evaluation data for the **LEX-10** benchmark (the 10 adversarial queries analyzed in Section 4 of the paper).

*   **LEX-10_eng.pdf / LEX-10_ru.pdf**: The core benchmark queries in English and Russian, covering structural integrity, safety protocols, and chemical constraints.
*   **bundle_for_input.pdf**: The anonymized data bundle provided to the LLM-as-a-Judge. It contains the query, the expert ground truth, and the responses from four strategies (Lex, Naive RAG, Zero-shot, and Full-Context) in randomized order.
*   **keys for position.pdf**: The mapping key used to de-anonymize the results. It links "Model A, B, C, D" to their respective strategies for each query to ensure a blind evaluation process.
*   **LLM-as-a-Judge_evaluation.pdf**: The final scores and summarized reasoning provided by Gemini 3 Pro (the Judge) based on the weighted rubric (Correctness, Safety, Citability).

### 📂 /Extended_pool/
This directory contains broader research materials and raw diagnostic data.

*   **Bench 28.pdf / Bench 28_eng.pdf**: An expanded pool of 28 complex regulatory queries used during the initial R&D phase to test the scalability of the knowledge graph.
*   **LLM-as-judge-keys.pdf**: Full, raw evaluation logs (100+ pages). This document provides the complete chain-of-thought of the Judge model for all queries. Note: Primary reasoning in these logs is conducted in Russian to maintain the highest precision regarding national technical standards (GOST/SP).

## Methodology & Scoring
We utilized an automated evaluation pipeline with the following weighted criteria:
1.  **Correctness (40%)**: Accuracy of the engineering solution.
2.  **Safety (30%)**: Adherence to mandatory safety prohibitions.
3.  **Citability (30%)**: Verifiability of references. 

**Hallucination Penalty:** Any citation of a non-existent regulatory clause resulted in an automatic score of 0 for the Citability dimension.

## Reproducibility
All results presented in the paper are derived from the data in `/Core-benchmark/`. The system architecture enables 100% traceability, meaning every verdict in the evaluation logs can be cross-referenced with the source documents cited in the knowledge graph.
