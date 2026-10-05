# OpenAudit: An Evidence-Linked Framework for LLM Transparency, Accessibility, and Reproducibility

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![Research](https://img.shields.io/badge/Research-LLM%20Transparency-blueviolet.svg)](#)
[![Models](https://img.shields.io/badge/Models-121-success.svg)](#evaluated-models)
[![Period](https://img.shields.io/badge/Model%20Releases-2019--2025-orange.svg)](#)
[![Status](https://img.shields.io/badge/Status-Research%20Repository-brightgreen.svg)](#)

## OpenAudit: A Comprehensive Analysis and Framework for Transparency and Accessibility in OpenAI, DeepSeek, Anthropic, and Other State-of-the-Art LLM Developers

**Authors:** Ranjan Sapkota, Shaina Raza, Manoj Karkee

**Repository:** https://github.com/rnjnspkt/OpenAudit

---

## Overview

**OpenAudit** is an evidence-linked framework for systematically evaluating transparency, accessibility, disclosure depth, and reproducibility across contemporary large language models (LLMs).

The rapid development of foundation models has created substantial ambiguity around terms such as *open source*, *open weight*, *accessible*, and *transparent*. A model may provide downloadable weights while withholding its training corpus, preprocessing procedures, evaluation methodology, source code, or safety documentation. Conversely, a proprietary model may provide extensive documentation while withholding the underlying parameters. OpenAudit therefore treats transparency as a **multidimensional, model/version-specific property** rather than a binary open-versus-closed label.

The empirical study evaluates **121 model/version records released between 2019 and 2025**, covering systems associated with OpenAI, DeepSeek, Anthropic, SpaceXAI, Meta, Google, and numerous other research and industrial organizations.

The repository provides the data, computational workflow, statistical-analysis scripts, visualization code, and supporting documentation required to inspect and reproduce the principal quantitative analyses reported in the study.

> **Important:** OpenAudit evaluates specific model/version records based on documented evidence. Scores assigned to one release should not be generalized automatically to an entire developer, organization, or model family.

---

## Research Motivation

Modern AI transparency cannot be determined solely from whether model weights are downloadable. Meaningful external inspection can depend on the availability of source code, training-data information, preprocessing procedures, evaluation protocols, technical documentation, safety information, licensing conditions, and reproducibility-relevant artifacts.

OpenAudit was developed to provide a structured and reproducible mechanism for examining these differences.

The project addresses four related questions:

1. How much model-level transparency is observable across contemporary LLM releases?
2. Which technical artifacts are most and least frequently disclosed?
3. How do transparency and reproducibility vary across access categories and release years?
4. How can evidence-linked transparency auditing evolve toward continuously updated evaluation of multimodal AI, AI agents, Agentic AI, world models, world-action models, and future highly autonomous AI systems?

---

## Core OpenAudit Metrics

### 1. Composite Transparency Score (CTS)

CTS measures the **breadth of model-level disclosure** across seven binary components:

| # | CTS component | What is evaluated |
|---:|---|---|
| 1 | Source code | Availability of relevant implementation code |
| 2 | Model weights | Availability of downloadable pretrained parameters |
| 3 | Training data | Disclosure of training-data information |
| 4 | Preprocessing | Disclosure of preprocessing/data-processing procedures |
| 5 | Evaluation protocol | Availability of evaluation methodology |
| 6 | Technical documentation | Availability of substantive technical documentation |
| 7 | Alignment/safety | Disclosure of alignment, safety, safeguards, or related evaluation |

For model \(m\):

\[
CTS_m = \frac{1}{7}\sum_{i=1}^{7} d_{mi}
\]

where \(d_{mi}\in\{0,1\}\) represents the verified disclosure status of component \(i\).

CTS ranges from **0 to 1**, with larger values indicating broader disclosure under the operational criteria used in OpenAudit.

---

### 2. Training Data Disclosure Index (TDDI)

TDDI is analytically separate from CTS and focuses specifically on **training-data transparency**.

Five dimensions are evaluated:

- data-source specification;
- preprocessing methodology;
- licensing clarity;
- language/domain distribution; and
- synthetic-to-organic data composition.

\[
TDDI_m = \frac{1}{5}\sum_{j=1}^{5} b_{mj}
\]

where \(b_{mj}\) represents the corresponding training-data disclosure indicator.

TDDI allows training-data transparency to be examined independently rather than being hidden inside a general openness score.

---

### 3. Depth Deficiency Index (DDI)

DDI captures **deficiency in disclosure depth** across the seven transparency dimensions.

\[
DDI_m = \frac{1}{7}\sum_{i=1}^{7}(1-d_{mi})
\]

Higher DDI values indicate greater disclosure deficiency under the defined scoring framework.

The project additionally reports a focused five-field training-data disclosure-depth analysis. This auxiliary measure should not be confused with the formal seven-dimensional DDI.

---

### 4. Reproducibility Score (RS)

RS measures availability of four artifacts particularly relevant to external reproduction and verification:

- source code;
- model weights;
- training-data disclosure; and
- evaluation-protocol disclosure.

\[
RS_m =
\frac{
a_{\mathrm{code}}+
a_{\mathrm{weights}}+
a_{\mathrm{data}}+
a_{\mathrm{eval}}
}{4}
\]

RS ranges from **0 to 1**.

---

## Evidence-Linked Audit Protocol

OpenAudit separates **literature synthesis** from **empirical model auditing**.

Scientific publications are used to establish conceptual background, definitions, governance considerations, and prior research. Model scores, however, are based on model/version-specific evidence rather than being inferred from general descriptions of a developer.

Where available, the audit structure records:

- resolved model/version identity;
- evidence source;
- source date;
- evidence-access date;
- archived or persistent source information;
- exact evidence location;
- applicable scoring criterion;
- disclosure status; and
- scoring rationale.

Missing or uncertain evidence should not automatically be converted to zero. The methodology distinguishes states including **Present**, **Insufficient disclosure**, **Verified absence after search**, **Inaccessible evidence**, **Ambiguous**, and **Not applicable**.

---

## Main Empirical Results

The empirical audit contains **121 model/version records** and **120 distinct model-name strings**.

| Measure | Result |
|---|---:|
| Number of evaluated records | 121 |
| Mean CTS | 0.5195 |
| Median CTS | 0.5714 |
| CTS standard deviation | 0.2773 |
| CTS 95% bootstrap CI | [0.4711, 0.5691] |
| CTS ≤ 0.25 | 18/121 (14.88%) |
| 0.25 < CTS < 0.75 | 76/121 (62.81%) |
| CTS ≥ 0.75 | 27/121 (22.31%) |
| Mean RS | 0.5186 |
| Median RS | 0.5000 |
| RS standard deviation | 0.3341 |
| RS 95% bootstrap CI | [0.4587, 0.5785] |
| RS = 1 | 21/121 (17.36%) |
| RS = 0 | 18/121 (14.88%) |
| Five-field training-data disclosure-depth mean | 0.1955 |
| Five-field complementary incompleteness mean | 0.8045 |

Bootstrap confidence intervals were calculated using **10,000 resamples** with random seed **20261003**.

### Component-level disclosure

| CTS component | Records satisfying criterion |
|---|---:|
| Technical documentation | 79 |
| Downloadable model weights | 76 |
| Evaluation protocol | 68 |
| Alignment/safety disclosure | 67 |
| Source code | 58 |
| Training-data disclosure | 49 |
| Preprocessing disclosure | 43 |

These results demonstrate an important distinction between **model accessibility** and **model transparency**. Downloadable weights can substantially increase practical accessibility without necessarily revealing the data provenance and development procedures required for end-to-end inspection or reproduction.

The temporal results also do not show a simple monotonic increase in transparency. Mean CTS varied from **0.6234 in 2019** to **0.5089 in 2025**, with substantial fluctuations between years.


### `run_openaudit_analysis.py`

Complete reproducible workflow for loading and validating the OpenAudit dataset, mapping disclosure variables, computing CTS, TDDI, DDI, and RS, checking metric consistency, and exporting analysis-ready outputs.

### `openaudit_statistical_analysis.py`

Performs descriptive statistics, bootstrap confidence intervals, transparency-band analysis, component frequencies, category and release-year comparisons, Pearson and Spearman associations, and Kruskal–Wallis analyses used in the empirical study.

### `openaudit_plot_analysis.py`

Generates the analytical visualizations used to examine CTS distributions, component prevalence, access-category differences, temporal patterns, reproducibility, disclosure-depth relationships, and model-level transparency profiles.

---

## Evaluated Models

The following table summarizes the **121 model/version records** included in the study. `—` indicates information that was not publicly disclosed, not reported by the evaluated source, or not sufficiently supported for inclusion as a verified architectural value. Architectural fields are not inferred from unofficial estimates.

| No. | Model | License / Access | Weights | Parameters | Context |
|---:|---|---|:---:|---:|---:|
| 1 | GPT-2 | MIT | Yes | 1.5B | 1024 |
| 2 | Legacy ChatGPT-3.5 | Proprietary | No | — | — |
| 3 | Default ChatGPT-3.5 | Proprietary | No | — | — |
| 4 | GPT-3.5 Turbo | Proprietary | No | — | 16K |
| 5 | GPT-4 | Proprietary | No | — | 8K |
| 6 | GPT-4o | Proprietary | No | — | 128K |
| 7 | GPT-4o mini | Proprietary | No | — | 128K |
| 8 | o1-preview | Proprietary | No | — | 128K |
| 9 | o1-mini | Proprietary | No | — | 128K |
| 10 | o1 | Proprietary | No | — | 128K |
| 11 | o1 pro mode | Proprietary | No | — | 128K |
| 12 | o3-mini | Proprietary | No | — | 128K |
| 13 | o3-mini-high | Proprietary | No | — | 128K |
| 14 | DeepSeek-R1 | Open-weight | Yes | 671B MoE | 128K |
| 15 | DeepSeek LLM | Open-weight | Yes | 67B | 4K |
| 16 | DeepSeek-V2 | Open-weight | Yes | 236B MoE | 128K |
| 17 | DeepSeek-Coder-V2 | Open-weight | Yes | 236B MoE | 128K |
| 18 | DeepSeek-V3 | Open-weight | Yes | 671B MoE | 128K |
| 19 | BERT-Base | Apache 2.0 | Yes | 110M | 512 |
| 20 | BERT-Large | Apache 2.0 | Yes | 340M | 512 |
| 21 | T5-Small | Apache 2.0 | Yes | 60M | 512 |
| 22 | T5-Base | Apache 2.0 | Yes | 220M | 512 |
| 23 | T5-Large | Apache 2.0 | Yes | 770M | 512 |
| 24 | T5-3B | Apache 2.0 | Yes | 3B | 512 |
| 25 | T5-11B | Apache 2.0 | Yes | 11B | 512 |
| 26 | Mistral 7B | Apache 2.0 | Yes | 7.3B | 8K |
| 27 | Llama 2 70B | Llama 2 License | Yes | 70B | 4K |
| 28 | CriticGPT | Proprietary | No | — | — |
| 29 | Olympus | Proprietary | No | — | — |
| 30 | HLAT | Research | — | 7B | — |
| 31 | Multimodal-CoT | Research | — | — | — |
| 32 | AlexaTM 20B | Research | Restricted | 20B | — |
| 33 | Chameleon | Research | — | 34B | — |
| 34 | Llama 3 70B | Llama 3 License | Yes | 70B | 8K |
| 35 | LIMA | Research | — | 65B base | — |
| 36 | BlenderBot 3x | Research | — | 150B | — |
| 37 | Atlas | Research | — | 11B | — |
| 38 | InCoder | Research | Yes | 6.7B | — |
| 39 | 4M-21 | Research | — | 3B | — |
| 40 | Apple OpenELM | Research | Yes | 3.04B | — |
| 41 | MM1 | Research | Restricted | 30B | — |
| 42 | ReALM-3B | Research | — | 3B | — |
| 43 | Ferret-UI | Research | — | 13B | — |
| 44 | MGIE | Research | — | 7B | — |
| 45 | Ferret | Research | — | 13B | — |
| 46 | Nemotron-4 340B | Model license | Yes | 340B | — |
| 47 | VIMA | Research | — | 0.2B | — |
| 48 | InstructRetro | Research | — | 48B | — |
| 49 | Raven | Research | — | 11B | — |
| 50 | Gemini 1.5 | Proprietary | No | — | — |
| 51 | Med-Gemini-L 1.0 | Proprietary | No | — | — |
| 52 | Hawk | Research | — | 7B | — |
| 53 | Griffin | Research | — | 14B | — |
| 54 | Gemma 7B | Gemma License | Yes | 7B | 8K |
| 55 | Gemini 1.5 Pro | Proprietary | No | — | — |
| 56 | PaLI-3 | Research | — | 5B | — |
| 57 | RT-X | Research | — | 55B | — |
| 58 | Med-PaLM M | Proprietary | No | — | — |
| 59 | MAI-1 | Proprietary | No | — | — |
| 60 | YOCO | Research | — | 3B | — |
| 61 | Phi-3-medium | Model license | Yes | 14B | — |
| 62 | Phi-3-mini | Model license | Yes | 3.8B | 128K |
| 63 | WizardLM-2-8x22B | Open-weight | Yes | 141B MoE | — |
| 64 | WaveCoder-Pro-6.7B | Research | Yes | 6.7B | — |
| 65 | WaveCoder-Ultra-6.7B | Research | Yes | 6.7B | — |
| 66 | Claude 3 Opus | Proprietary | No | — | 200K |
| 67 | Claude 3.5 Sonnet | Proprietary | No | — | 200K |
| 68 | Claude 3 Haiku | Proprietary | No | — | 200K |
| 69 | Claude 2 | Proprietary | No | — | 100K |
| 70 | Claude (original) | Proprietary | No | — | — |
| 71 | Grok-1.5 | Proprietary | No | — | 128K |
| 72 | Grok-2 | Proprietary | No | — | 128K |
| 73 | Grok-3 | Proprietary | No | — | — |
| 74 | Turing-NLG | Proprietary | No | 17B | 1024 |
| 75 | CTRL | Apache 2.0 | Yes | 1.6B | 256 |
| 76 | XLNet | Apache 2.0 | Yes | 340M | 512 |
| 77 | RoBERTa | MIT | Yes | 355M | 512 |
| 78 | ELECTRA | Apache 2.0 | Yes | 110M/335M | 512 |
| 79 | ALBERT | Apache 2.0 | Yes | 12M/18M | 512 |
| 80 | DistilBERT | Apache 2.0 | Yes | 66M | 512 |
| 81 | BigBird | Apache 2.0 | Yes | 110M/340M | 4096 |
| 82 | Gopher | Proprietary | No | 280B | 2048 |
| 83 | Chinchilla | Proprietary | No | 70B | 2048 |
| 84 | PaLM | Proprietary | No | 540B | 2048 |
| 85 | OPT-175B | Non-commercial | Yes | 175B | 2048 |
| 86 | BLOOM | RAIL | Yes | 176B | 2048 |
| 87 | Jurassic-1 Jumbo | Proprietary | No | 178B | 2048 |
| 88 | Codex | Proprietary | No | — | 4096 |
| 89 | T0 | Apache 2.0 | Yes | 11B | 512 |
| 90 | UL2 | Apache 2.0 | Yes | 20B | 2048 |
| 91 | GLaM | Proprietary | No | 1.2T MoE | 2048 |
| 92 | ERNIE 3.0 | Proprietary | No | 10B | — |
| 93 | GPT-NeoX-20B | Apache 2.0 | Yes | 20B | 2048 |
| 94 | CodeGen-16B | Apache 2.0 | Yes | 16B | 2048 |
| 95 | FLAN-T5-XXL | Apache 2.0 | Yes | 11B | 512 |
| 96 | mT5-XXL | Apache 2.0 | Yes | 13B | 1024 |
| 97 | Reformer | Apache 2.0 | Yes | — | 64K |
| 98 | Longformer | Apache 2.0 | Yes | 149M | 4096 |
| 99 | DeBERTa | MIT | Yes | — | 512 |
| 100 | T-NLG | Proprietary | No | 17B | 1024 |
| 101 | Switch Transformer | Apache 2.0 | Yes | 1.6T MoE | — |
| 102 | WuDao 2.0 | Proprietary | No | 1.75T | — |
| 103 | LaMDA | Proprietary | No | 137B | 2048 |
| 104 | MT-NLG | Proprietary | No | 530B | 2048 |
| 105 | GShard | Proprietary | No | 600B MoE | — |
| 106 | T5-XXL | Apache 2.0 | Yes | 11B | 512 |
| 107 | ProphetNet | MIT | Yes | 300M | 512 |
| 108 | DialoGPT | MIT | Yes | 345M | 1024 |
| 109 | BART | MIT | Yes | 406M | 1024 |
| 110 | PEGASUS | Apache 2.0 | Yes | 568M | 512 |
| 111 | UniLM | MIT | Yes | 340M | 512 |
| 112 | Grok 4 | Proprietary | No | — | — |
| 113 | Gemini 2 Ultra | Proprietary | No | — | 2M |
| 114 | GPT-4.5 | Proprietary | No | — | 128K |
| 115 | Gemini 2.0 Flash-Lite | Proprietary | No | — | 1M |
| 116 | Gemini 2.0 Pro | Proprietary | No | — | 2M |
| 117 | Gemini 2.5 Pro | Proprietary | No | — | 2M |
| 118 | o3 | Proprietary | No | — | 200K |
| 119 | GPT-4.1 | Proprietary | No | — | 1M |
| 120 | o4-mini | Proprietary | No | — | 200K |
| 121 | Qwen3-235B-A22B | Apache 2.0 | Yes | 235B MoE | 128K |

**Note:** The table is a technical reference accompanying the transparency audit. `—` denotes unavailable or insufficiently verified information. Architectural specifications and benchmark information are not components of CTS, TDDI, DDI, or RS unless explicitly defined by the OpenAudit scoring framework.

---

## Reproducing the Analysis

### 1. Clone the repository

```bash
git clone https://github.com/rnjnspkt/OpenAudit.git
cd OpenAudit
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

Core dependencies include:

```text
numpy
pandas
scipy
matplotlib
openpyxl
python-docx
```

### 3. Run the complete analysis

```bash
python pipeline/run_openaudit_analysis.py
```

### 4. Run statistical analysis

```bash
python analysis/openaudit_statistical_analysis.py
```

### 5. Reproduce visualizations

```bash
python analysis/openaudit_plot_analysis.py
```

The scripts use the released model-level dataset rather than hard-coded manuscript results. Output tables should therefore be regenerated directly from the underlying audit records.

---

## Data Quality and Reuse

The dataset is intended to support transparent inspection and reuse. Users should preserve the distinction between:

- release date and evidence-access date;
- model/version-level evidence and developer-level claims;
- missing evidence and verified absence;
- open-source and open-weight access;
- transparency breadth and disclosure depth;
- model accessibility and reproducibility; and
- descriptive benchmark information and transparency metrics.

Because public documentation can change after model release, transparency scores should be interpreted relative to the evidence snapshot represented in the released audit data.

---

## Beyond LLMs: Agentic AI and Artificial Superintelligence

OpenAudit is empirically evaluated on the 121 model/version records described above. The study additionally proposes a future research direction for extending transparency auditing beyond conventional LLMs.

The **Automated Transparency Benchmarking Framework (ATBF)** is intended as a foundation for scalable, continuously updated evidence collection and transparency assessment. Its proposed agentic extension, the **Agentic Transparency Benchmarking System (ATBS)**, recognizes that AI-agent transparency requires evidence beyond foundation-model documentation.

For AI agents and Agentic AI, future transparency frameworks may need to document:

- tool access and tool invocation;
- retrieval provenance;
- persistent memory;
- action histories;
- orchestration logic;
- inter-agent communication;
- planning and decision provenance;
- human oversight;
- uncertainty and failure states; and
- changes introduced through adaptation or self-improvement.

These considerations become increasingly important for world models, world-action models, self-improving AI, and prospective **artificial superintelligence (ASI)** or **digital superintelligence**. These systems are discussed as future transparency challenges and are **not presented as systems empirically evaluated in the current 121-model audit**.

A central principle motivating this extension is that **self-improvement must not become self-obscuration**: as AI systems acquire greater autonomy and capacity to modify their behavior, transparency mechanisms should preserve traceability of what changed, why it changed, which evidence or interaction caused the change, and how the resulting system can be independently evaluated.

---

## Scope and Limitations

OpenAudit measures the availability and depth of publicly accessible evidence under explicitly defined operational criteria. It does not establish that a developer is legally compliant with a particular governance framework, nor does the absence of publicly accessible evidence establish that an artifact does not exist internally.

Likewise, architectural specifications and benchmark values may originate from different evaluation settings and should not be interpreted as a controlled performance ranking.

The framework should therefore be used as an **evidence-linked transparency audit**, not as a universal measure of model quality, intelligence, safety, or benchmark capability.

---

## Citation

If you use the OpenAudit dataset, metrics, code, or framework in academic research, please cite the associated paper and repository.

```bibtex
@article{sapkota2026openaudit,
  title   = {OpenAudit: A Comprehensive Analysis and Framework for
             Transparency and Accessibility in OpenAI, DeepSeek,
             Anthropic, SpaceXAI, and Other State-of-the-Art LLM Developers},
  author  = {Sapkota, Ranjan and Raza, Shaina and Karkee, Manoj},
  year    = {2026},
 journal = {AI OPEN, UNDER REVIEW},
  note    = {Manuscript and accompanying OpenAudit research repository},
  url     = {https://github.com/rnjnspkt/OpenAudit}
}
```

Please replace or update this BibTeX entry with the final journal citation, DOI, volume, pages, and publication year after publication.

---

## Data and Code Availability

The model-level audit data, transparency records, metric definitions, computational workflow, statistical-analysis scripts, and visualization code supporting this study are made publicly available in this repository to facilitate independent verification, reproducibility, extension, and reuse.

For long-term preservation, the final repository release should additionally be archived in a persistent research repository and assigned a DOI. The archived DOI should then be cited in the final manuscript and added to this README.

---

## Contributing

Corrections and evidence-based updates are welcome.

If proposing a change to a model record, please provide:

1. the exact model/version;
2. the transparency component affected;
3. a primary or authoritative evidence source;
4. the relevant source date/version;
5. the exact evidence location; and
6. a short explanation of why the evidence changes the existing audit decision.

Please use GitHub Issues or submit a pull request with supporting evidence.

---

## License

The repository license applies to the code and materials explicitly covered by the accompanying `LICENSE` file. Third-party model documentation, model weights, datasets, trademarks, and external resources remain subject to their respective owners' licenses and terms.

---

## Keywords

**LLM Transparency · AI Transparency · Foundation Model Transparency · Open-Source AI · Open-Weight Models · AI Auditability · AI Accountability · Responsible AI · Trustworthy AI · Training Data Transparency · Data Provenance · Model Provenance · AI Reproducibility · AI Governance · AI Safety · Agentic AI Transparency · AI Agent Transparency · Multi-Agent Transparency · World Model Transparency · Self-Improving AI Transparency · Artificial Superintelligence Transparency · Digital Superintelligence · OpenAudit · CTS · TDDI · DDI · RS · ATBF · ATBS**

---

## Contact

For questions regarding the OpenAudit framework, dataset, code, or reproducibility package, please open an issue in this repository or contact the corresponding authors through the information provided in the associated publication.

---

### OpenAudit

**Evidence-linked transparency auditing from today's LLMs toward accountable Agentic AI and future intelligent systems.**
