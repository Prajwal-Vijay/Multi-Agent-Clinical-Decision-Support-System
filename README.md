# Multi-Agent Clinical Decision Support System (CDSS)

## Features

- **Three cooperative agents**:
  - **Clinical QA Agent**: answers clinician queries grounded in patient EHR snippets.
  - **Triage Agent**: detects abnormal vitals/labs and computes risk scores (qSOFA).
  - **Diagnosis Agent**: proposes likely ICD-10 codes with confidence and evidence.

- **Hybrid retrieval pipeline**:
  - BM25 + FAISS dense embeddings
  - Reciprocal Rank Fusion (RRF)
  - Cross-encoder reranking (scaffolded)

- **MCP Tools**:
  - EHR access (`ehr.*`): search, labs, vitals, conditions, meds
  - Clinical calculators (`calc.*`): qSOFA, eGFR, lab interpretation

- **Training / Adaptation**:
  - Domain Adaptive Pretraining (DAPT) on Synthea evidence
  - Parameter-efficient fine-tuning with LoRA

- **Outputs** (JSONL/JSON):
  - `retrieval_results.jsonl`
  - `qa_results.jsonl`
  - `triage_results.jsonl`
  - `diagnosis_results.jsonl`
  - `system_metrics.json`

- **Safety**:
  - Input validation and schema enforcement with Pydantic
  - Audit logging of all MCP tool usage
  - Confidence-based human-in-the-loop triggers

⚠️ **Disclaimer**: For research/educational use only. Operates on **synthetic Synthea data**. **Not a medical device.**

## Installation

```bash
pip install -r requirements.txt
```

## Usage

1. Open and run the Jupyter notebook:

```bash
jupyter notebook clinical_multi_agent_cdss.ipynb
```

2. Run cells in order to:
   - Install dependencies (if not already installed)
   - Download and prepare Synthea sample EHR data
   - Build evidence corpus and hybrid search indices
   - Use MCP tools for EHR access and calculations
   - Run orchestration (Clinical QA → Triage → Diagnosis)
   - Export required JSONL/JSON outputs to `./outputs`

## Data

- Uses [Synthea synthetic patient data](https://synthetichealth.github.io/synthea/).
- Sample CSVs are automatically downloaded on first run.

## Deliverables

- Notebook: `clinical_multi_agent_cdss.ipynb`
- Outputs: `outputs/*.jsonl`, `outputs/system_metrics.json`
- Supporting files: `requirements.txt`, `README.md`

## Citation Anchoring

All agent responses include **meta tags** (`obs:...`, `cond:...`, `med:...`) which serve as structured citations back to the originating EHR snippets.

## License

MIT License. For educational use only.
