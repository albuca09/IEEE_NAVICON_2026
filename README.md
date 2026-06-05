# TSMS-Drone Multimodal Fusion Pipeline

A complete experimental pipeline for the **Time-Synchronized Multi-Sensor Drone Dataset (TSMS-Drone)**, designed for multimodal drone detection and characterization using synchronized **CW Radar**, **FMCW Radar**, and **RF Receiver** data.

This project transforms the raw TSMS-Drone dataset into an organized, auditable, and experiment-ready structure. It includes automatic dataset download, compressed-file inspection, extraction, directory standardization, integrity validation, exploratory data analysis, benchmark evaluation, and a proposed multimodal fusion architecture based on attention and reliability-aware sensor gating.

---

## Overview

The main goal of this project is to support rigorous experiments with synchronized multi-sensor drone data. The pipeline handles the full workflow from raw dataset preparation to publication-ready results.

It supports:

* Automatic download of TSMS-Drone files from Figshare.
* Inspection and extraction of compressed files.
* Standardization of the dataset directory tree.
* Integrity validation of `.mat` files.
* Detection of missing, inconsistent, or transposed sensor files.
* Exploratory data analysis for scientific reporting.
* Classical benchmark evaluation.
* Multimodal deep learning with CW Radar, FMCW Radar, and RF Receiver data.
* Experimental-rigor audits, including leakage detection, duplicate checks, and statistical testing.

---

## Dataset

This project is built around the **Time-Synchronized Multi-Sensor Drone Dataset (TSMS-Drone)**.

The dataset contains synchronized measurements from multiple sensing modalities:

* **CW Radar**
* **FMCW Radar**
* **RF Receiver**

These modalities enable the evaluation of single-sensor, dual-sensor, and full multimodal fusion strategies for drone-related tasks.

---

## Main Objectives

The pipeline was designed to:

1. Convert the raw TSMS-Drone dataset into a clean and standardized structure.
2. Verify data integrity across sensors, targets, distances, and experimental conditions.
3. Generate exploratory tables and figures suitable for scientific publication.
4. Evaluate classical machine-learning and deep-learning benchmarks.
5. Implement a multimodal fusion model with attention, reliability gating, and sensor dropout.
6. Support rigorous experimental protocols such as open-set evaluation, leave-one-distance-out validation, and leakage analysis.

---

## Pipeline Stages

### 1. Dataset Download

The pipeline starts by automatically downloading the required files from Figshare.

This stage ensures that the raw data can be reproduced from the original public source.

### 2. File Inspection and Extraction

Compressed files are inspected before extraction. The pipeline verifies file names, folder structures, and expected contents.

### 3. Directory Standardization

The raw dataset is reorganized into a consistent and reproducible directory tree, making it easier to run experiments and track samples across modalities.

### 4. Data Integrity Validation

The validation stage checks:

* Expected number of files per condition.
* Internal variables inside `.mat` files.
* Shape consistency.
* Missing files.
* Corrupted or unreadable files.
* FMCW files with transposed dimensions.

When corrections are applied, backup files are generated automatically.

### 5. Exploratory Data Analysis

The project generates publication-oriented exploratory analysis outputs, including:

* CSV tables.
* Markdown tables.
* LaTeX tables.
* Dataset summaries.
* Sensor availability statistics.
* Class and distance distributions.

These outputs can be used directly in technical reports, dissertations, or scientific papers.

### 6. Benchmark Evaluation

The pipeline evaluates baseline models for multiple tasks, including:

* Target classification.
* Drone/non-drone detection.
* Drone model identification.
* Distance estimation.

These benchmarks provide reference performance for comparison with multimodal fusion models.

### 7. Proposed Multimodal Fusion Model

The project includes a multimodal architecture based on:

* Sensor-specific encoders.
* Cross-modal self-attention.
* Reliability gating.
* Sensor dropout.
* Auxiliary prediction head.

The model supports different sensor configurations:

* CW Radar only.
* FMCW Radar only.
* RF Receiver only.
* CW + FMCW.
* CW + RF.
* FMCW + RF.
* CW + FMCW + RF.

This allows a systematic comparison between isolated sensors, sensor pairs, and complete multimodal fusion.

---

## Experimental Rigor

The pipeline includes several procedures to improve experimental reliability:

* Split-leakage checking.
* Hash-based duplicate detection.
* Near-repetition analysis.
* Leave-one-distance-out protocols.
* Distance-bin-based splitting.
* Open-set evaluation.
* Leave-target-out evaluation.
* Bootstrap confidence intervals.
* McNemar statistical tests.
* Calibration analysis.
* Risk-coverage curves.

These procedures help ensure that the reported performance reflects true generalization rather than data leakage or repeated samples.

---

## Recommended Repository Structure

```text
TSMS-Drone-Fusion/
│
├── data/
│   ├── raw/
│   ├── extracted/
│   ├── standardized/
│   └── processed/
│
├── notebooks/
│   └── figure_fusion_drone.ipynb
│
├── outputs/
│   ├── tables/
│   ├── figures/
│   ├── logs/
│   └── checkpoints/
│
├── src/
│   ├── download.py
│   ├── prepare_dataset.py
│   ├── validate_dataset.py
│   ├── eda.py
│   ├── benchmarks.py
│   ├── models.py
│   ├── train.py
│   └── evaluate.py
│
├── requirements.txt
└── README.md
```

---

## Installation

Clone the repository:

```bash
git clone https://github.com/your-username/TSMS-Drone-Fusion.git
cd TSMS-Drone-Fusion
```

Create a virtual environment:

```bash
python -m venv .venv
```

Activate the environment:

On Linux/macOS:

```bash
source .venv/bin/activate
```

On Windows:

```bash
.venv\Scripts\activate
```

Install the required packages:

```bash
pip install -r requirements.txt
```

---

## Suggested Requirements

```text
numpy
pandas
scipy
matplotlib
seaborn
scikit-learn
torch
torchvision
tqdm
h5py
joblib
requests
```

Depending on the notebook version, additional packages may be required for statistical testing, advanced visualization, or deep-learning utilities.

---

## Usage

### Run the Notebook

The main experimental workflow is available in:

```text
notebooks/figure_fusion_drone.ipynb
```

Launch Jupyter Notebook or JupyterLab:

```bash
jupyter notebook
```

or:

```bash
jupyter lab
```

Then open the notebook and execute the cells sequentially.

---

## Main Outputs

The pipeline produces several outputs, including:

* Cleaned and standardized dataset folders.
* Integrity-validation reports.
* Dataset summary tables.
* Exploratory data analysis figures.
* Benchmark metrics.
* Multimodal fusion metrics.
* Statistical comparison results.
* Calibration and risk-coverage plots.
* Publication-ready CSV, Markdown, and LaTeX tables.

---

## Supported Tasks

The project supports experiments for:

* Drone detection.
* Drone/non-drone classification.
* Drone model identification.
* Target classification.
* Distance estimation.
* Sensor-ablation studies.
* Multimodal fusion evaluation.
* Open-set and leave-target-out protocols.

---

## Model Description

The proposed model follows a multimodal fusion strategy. Each sensor modality is first processed by a dedicated encoder. The resulting embeddings are then combined through a cross-modal attention mechanism.

A reliability-gating module estimates the contribution of each sensor, allowing the network to reduce the influence of noisy or less informative modalities. Sensor dropout is used during training to improve robustness when one or more sensors are unavailable or degraded.

The architecture also includes an auxiliary prediction head to encourage each modality to learn discriminative representations before fusion.

---

## Scientific Use

This project is suitable for:

* Technical reports.
* Master’s and doctoral dissertations.
* IEEE-style conference or journal papers.
* Comparative studies on multimodal sensing.
* Drone detection and characterization research.
* Radar-RF fusion experiments.
* Robustness and generalization studies.

---

## Reproducibility

The pipeline emphasizes reproducibility by including:

* Standardized data preparation.
* Explicit dataset validation.
* Fixed experimental splits.
* Backup generation before file correction.
* Exported tables and figures.
* Statistical evaluation procedures.
* Multiple fusion and ablation configurations.

---

## Citation

When using this project, please cite the original TSMS-Drone dataset and any related publications associated with it.

A suggested project citation format is:

```bibtex
@misc{tsms_drone_fusion_pipeline,
  title        = {TSMS-Drone Multimodal Fusion Pipeline},
  author       = {Your Name},
  year         = {2026},
  note         = {Experimental pipeline for multimodal drone detection and characterization using CW Radar, FMCW Radar, and RF Receiver data}
}
```

---

## License

Specify the license according to your intended use.

Example:

```text
MIT License
```

---

## Project Status

This project is under active development and is intended for experimental research on multimodal drone sensing, sensor fusion, and robust target characterization.

# TSMS-Drone Multisensor Fusion

Pipeline em Python/Jupyter para baixar, organizar, auditar, explorar e modelar o **Time-Synchronized Multi-Sensor Drone Dataset (TSMS-Drone)**, com foco em fusão multimodal de sensores para reconhecimento de drones, identificação de modelo, detecção drone/não-drone e estimação de distância.

O projeto trabalha com três modalidades sincronizadas:

- **CW Radar**
- **FMCW Radar**
- **RF Receiver**

E considera cinco alvos:

- Inspire 2
- Matrice 30
- Mavic 2 Pro
- Phantom 4 Pro
- Corner Reflector

As distâncias avaliadas são de **2 m a 30 m**, em passos de 2 m.

---

## Objetivo

Este repositório reúne um fluxo completo para experimentos com o TSMS-Drone:

1. baixar automaticamente os arquivos do Figshare;
2. inspecionar arquivos compactados `.7z`;
3. extrair e reorganizar o dataset em uma estrutura padronizada;
4. verificar integridade dos arquivos `.mat` e `.png`;
5. corrigir inconsistências específicas em arquivos FMCW transpostos;
6. gerar análise exploratória de dados;
7. construir índices sincronizados entre sensores;
8. treinar benchmarks clássicos;
9. treinar um modelo proposto de fusão multimodal com atenção e gating;
10. auditar vazamento de dados, duplicatas e robustez experimental;
11. gerar tabelas e gráficos prontos para artigo.

---

## Estrutura esperada do dataset

Após a reorganização, o projeto espera a seguinte estrutura:

```text
D:\Time-Synchronized Multi-Sensor Drone Dataset (TSMS-Drone)
├── Dataset
│   ├── CW Radar
│   │   ├── 2m
│   │   │   ├── Inspire 2
│   │   │   │   ├── Raw File
│   │   │   │   └── Image File
│   │   │   └── ...
│   │   └── ...
│   ├── FMCW Radar
│   └── RF Receiver
├── _organization_check
├── _eda_ieee
├── _advanced_fusion_improvements
├── _baseline_multitask_fusion_benchmark
├── _proposed_multitask_attention_fusion_vscode
├── _ieee_leakage_and_robustness_audit
└── _comparative_all_scenario_metrics
```

Cada condição é definida por:

```text
sensor × distância × alvo
```

No notebook, a organização esperada considera **500 arquivos `.mat`** e **500 arquivos `.png`** por condição.

---

## Principais etapas do notebook

### 1. Download do Figshare

O notebook contém rotinas para baixar o artigo/dataset do Figshare por:

- URL direta do `ndownloader`;
- API do Figshare, preservando nomes e tamanhos esperados dos arquivos;
- suporte a retomada de download com arquivos `.part`.

Saída principal:

```text
D:\Fusion\figshare_30027313_v1
```

---

### 2. Inspeção dos arquivos baixados

São gerados relatórios de inventário e inspeção:

```text
_exploration_report/
├── file_inventory.csv
├── folder_summary.csv
├── extension_summary.csv
├── largest_files.csv
├── empty_files.csv
├── duplicate_names.csv
├── duplicate_sizes.csv
├── directory_tree.txt
└── summary_report.md
```

Também há inspeção interna dos arquivos `.7z` sem extração completa:

```text
_archive_inspection/
├── archive_file_summary.csv
├── archive_contents_full.csv
├── archive_contents_by_extension.csv
├── archive_contents_by_top_folder.csv
└── archive_report.md
```

---

### 3. Extração e reorganização

O notebook extrai os arquivos compactados e reorganiza o conteúdo em uma estrutura padronizada por sensor, distância e alvo.

Estrutura final por condição:

```text
Dataset/<Sensor>/<Distance>/<Target>/Raw File/*.mat
Dataset/<Sensor>/<Distance>/<Target>/Image File/*.png
```

Arquivos auxiliares são salvos em:

```text
_organization_check/
_reorganization_logs/
_tmp_extract/
```

---

### 4. Verificação de integridade

A rotina de verificação confere:

- presença das pastas esperadas;
- quantidade de `.mat` por condição;
- quantidade de `.png` por condição;
- nome dos arquivos;
- variável esperada dentro dos `.mat`;
- shape esperado dos dados.

Variáveis esperadas:

| Sensor | Variável `.mat` esperada | Shape esperado |
|---|---:|---:|
| CW Radar | `data` | `(16384,)` |
| RF Receiver | `data` | `(262144,)` |
| FMCW Radar | `RD` | `(161, 4096)` |

Saídas típicas:

```text
_organization_check/
├── condition_counts.csv
├── mat_content_check.csv
├── mat_content_check_final_interpretation.csv
├── warnings_diagnostic.csv
├── saving_tree.txt
└── saving_tree_summary.csv
```

---

### 5. Tratamento de warnings e correção FMCW

O notebook interpreta diferenças de shape em arquivos `.mat` e identifica arquivos FMCW transpostos.

Quando necessário, os arquivos são corrigidos com backup prévio:

```text
_backup_fmcw_transposed_originals/
```

A correção esperada converte arquivos FMCW para:

```text
(161, 4096)
```

---

### 6. Análise exploratória de dados

A EDA gera estatísticas e tabelas compatíveis com artigo IEEE, incluindo:

- distribuição por sensor;
- distribuição por alvo;
- distribuição por distância;
- contagem por condição;
- amostras de metadados `.mat`;
- amostras de imagens `.png`;
- tabelas `.csv`, `.md` e `.tex`.

Saída principal:

```text
_eda_ieee/
```

---

## Modelos e experimentos

### Benchmarks clássicos

O script de benchmark multitarefa avalia modelos clássicos com diferentes combinações de sensores.

Tarefas:

1. **Target classification**  
   Classificação entre 5 classes: Inspire 2, Matrice 30, Mavic 2 Pro, Phantom 4 Pro e Corner Reflector.

2. **Drone vs non-drone**  
   Classificação binária: drones contra Corner Reflector.

3. **Drone model identification**  
   Identificação entre os 4 modelos de drone, excluindo Corner Reflector.

4. **Distance estimation**  
   Estimação da distância como classificação em 15 classes: 2 m, 4 m, ..., 30 m.

Cenários de sensores:

- CW only
- FMCW only
- RF only
- CW + FMCW
- CW + RF
- FMCW + RF
- All sensors

Modelos de baseline:

- RidgeClassifier
- LinearSVM
- LogisticRegression
- ExtraTrees
- RandomForest, opcional no preset completo

Saída:

```text
_baseline_multitask_fusion_benchmark/
├── features/
├── metrics/
├── predictions/
├── figures/
└── tables/
```

---

### Modelo proposto

O modelo proposto utiliza fusão multimodal com:

- encoders CNN específicos por sensor;
- tokens por modalidade;
- self-attention cross-modal;
- reliability gate por amostra;
- cabeça auxiliar;
- sensor dropout;
- avaliação por máscaras de sensores;
- treinamento multitarefa.

Arquivo principal sugerido:

```text
tsms_drone_proposed_multitask_attention_fusion_vscode.py
```

Execução padrão:

```bash
python tsms_drone_proposed_multitask_attention_fusion_vscode.py
```

Teste rápido:

```bash
python tsms_drone_proposed_multitask_attention_fusion_vscode.py --epochs 2 --max-train-samples 3000 --image-size 96
```

Saída:

```text
_proposed_multitask_attention_fusion_vscode/
├── checkpoints/
├── metrics/
├── predictions/
├── figures/
└── tables/
```

---

## Auditoria de leakage, robustez e tabelas IEEE

O notebook inclui auditoria complementar para produzir evidências experimentais mais rigorosas:

- checagem de overlap entre splits;
- duplicatas por caminho, tupla, arquivo e hash;
- MD5 e perceptual hash;
- risco de leakage por repetições próximas;
- protocolos leave-one-distance-out;
- split por faixas near/mid/far;
- protocolo open-set / leave-target-out;
- bootstrap confidence intervals;
- teste de McNemar;
- calibração e reliability diagrams;
- risk-coverage curves;
- análise de gates/pesos de confiabilidade;
- tabelas `.csv`, `.md` e `.tex`.

Execução sugerida:

```bash
python tsms_drone_ieee_audit_tables_complete.py --root "D:\Time-Synchronized Multi-Sensor Drone Dataset (TSMS-Drone)"
```

Teste rápido:

```bash
python tsms_drone_ieee_audit_tables_complete.py --no-hash-images --bootstrap 200
```

Saídas:

```text
_ieee_leakage_and_robustness_audit/
└── _paper_results_tables/
```

---

## Comparação baseline vs modelo proposto

O notebook também gera tabelas e gráficos comparando:

- métricas gerais por tarefa;
- métricas por cenário de sensores;
- desempenho por distância;
- acurácia por alvo e distância;
- curvas e figuras em estilo publicável.

Saída:

```text
_comparative_all_scenario_metrics/
├── tables/
└── figures/
```

---

## Requisitos

### Dependências Python

Instalação básica:

```bash
pip install numpy pandas pillow tqdm scikit-learn matplotlib scipy h5py requests tabulate
```

Para o modelo proposto em PyTorch:

```bash
pip install torch
```

### Dependências externas

Para extração e inspeção dos arquivos `.7z`, instale o **7-Zip** e confirme que o executável está em um dos caminhos esperados pelo notebook, por exemplo:

```text
C:\Program Files\7-Zip\7z.exe
```

---

## Como usar

### 1. Ajustar caminhos

Antes de executar, ajuste os caminhos principais dentro do notebook ou dos scripts exportados:

```python
ROOT = Path(r"D:\Time-Synchronized Multi-Sensor Drone Dataset (TSMS-Drone)")
SOURCE_ROOT = Path(r"D:\Fusion\figshare_30027313_v1")
DEST_ROOT = Path(r"D:\Time-Synchronized Multi-Sensor Drone Dataset (TSMS-Drone)")
```

### 2. Baixar o dataset

Execute as células de download do Figshare.

### 3. Inspecionar os arquivos

Execute as células de inventário e inspeção dos `.7z`.

### 4. Extrair e reorganizar

Execute a etapa de extração/reorganização.

Para teste inicial, use:

```python
LIMIT_ARCHIVES = 2
```

Para processar tudo:

```python
LIMIT_ARCHIVES = None
```

### 5. Conferir integridade

Execute as células de checagem da organização e conteúdo dos `.mat`.

### 6. Corrigir inconsistências FMCW, se necessário

Execute a etapa de diagnóstico e correção apenas se forem encontrados arquivos FMCW transpostos.

### 7. Rodar EDA

Execute a análise exploratória para gerar tabelas e estatísticas.

### 8. Rodar benchmarks

Execute o script/célula de benchmark multitarefa.

### 9. Rodar modelo proposto

Execute o modelo de fusão com atenção/gating.

### 10. Gerar auditoria e tabelas finais

Execute a auditoria IEEE e a geração de gráficos comparativos.

---

## Recomendações de organização do repositório

Uma estrutura limpa para transformar o notebook em projeto seria:

```text
.
├── README.md
├── requirements.txt
├── notebooks/
│   └── figure_fusion_drone.ipynb
├── scripts/
│   ├── download_figshare.py
│   ├── explore_figshare_dataset.py
│   ├── inspect_7z_contents_figshare.py
│   ├── reorganize_tsms_drone_dataset.py
│   ├── check_dataset_organization.py
│   ├── tsms_drone_multitask_baseline_fusion_benchmark.py
│   ├── tsms_drone_proposed_multitask_attention_fusion_vscode.py
│   ├── tsms_drone_ieee_audit_tables_complete.py
│   └── extract_all_scenario_metrics_and_plots.py
├── docs/
│   └── DESCRICAO.md
├── outputs/
└── data/
    └── README.md
```

---

## Resultados esperados

Ao final do fluxo, o projeto deve produzir:

- dataset reorganizado e validado;
- relatórios de integridade;
- tabelas de EDA;
- índices sincronizados entre sensores;
- benchmarks clássicos por sensor e tarefa;
- modelo proposto de fusão multimodal;
- predições por tarefa;
- métricas por cenário de sensores;
- análise por distância;
- análise por alvo;
- auditoria de leakage;
- tabelas em CSV/Markdown/LaTeX;
- gráficos prontos para relatório ou artigo.

---

## Observações importantes

- O notebook usa caminhos Windows absolutos. Para outros ambientes, altere as variáveis `ROOT`, `SOURCE_ROOT`, `DEST_ROOT` e `OUT_DIR`.
- A etapa de hashing completo pode ser demorada em datasets grandes.
- A extração de arquivos `.7z` depende do 7-Zip instalado.
- O treinamento em PyTorch pode se beneficiar de GPU.
- Antes de publicar resultados, recomenda-se usar os protocolos de auditoria para evitar vazamento entre treino, validação e teste.

---

## Licença e uso dos dados

Este repositório contém código de processamento e experimentação. Os dados do TSMS-Drone devem ser utilizados conforme os termos de uso e citação definidos pelos autores originais do dataset.

---

## Citação sugerida do projeto

```bibtex
@misc{tsms_drone_multisensor_fusion_pipeline,
  title  = {TSMS-Drone Multisensor Fusion: Dataset Organization, Audit, Baselines and Attention-Gated Fusion},
  author = {Luis Paulo Guedes},
  year   = {2026},
  note   = {Python/Jupyter pipeline for TSMS-Drone multisensor fusion experiments}
}
```
