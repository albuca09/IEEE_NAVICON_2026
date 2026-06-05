
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
