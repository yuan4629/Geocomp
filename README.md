# Geocomp: Geolocation with Real Human Gameplay Data: A Large-Scale Dataset and Human-Like Reasoning Framework


## 📝 Introduction

Geocomp is a research project and codebase focusing on **image geolocation**. Geolocation aims to precisely identify the location where an image was captured, which is crucial in fields such as navigation, autonomous driving, content moderation, and cultural heritage preservation. However, its inherent complexity poses significant challenges to existing methods. Current mainstream approaches often produce coarse, imprecise, and uninterpretable localization results. This is partly due to the limitations of existing benchmark datasets, which are often limited in scale, automatically constructed, contain noise, and have an uneven distribution of task difficulty (image clues are either too obvious or severely lacking), making it difficult to effectively evaluate and advance the development of models' advanced reasoning capabilities.

To address these challenges, this project proposes a comprehensive research framework for geolocation, comprising three core components:

1.  **GeoComp Dataset**: A large-scale, high-quality dataset derived from real human participation in geolocation competitions.
2.  **GeoCoT Reasoning Method**: A geospatial reasoning framework that mimics the human Chain-of-Thought (CoT), designed to enhance the geolocation capabilities of Large Vision-Language Models (LVMs).
3.  **GeoEval Evaluation Suite**: A set of specifically designed metrics and tools for comprehensively evaluating the performance and reasoning processes of geolocation models.

This project aims to tackle key bottlenecks in current geolocation research through this framework, driving substantial progress in the field.

<p align="center">
  <img src="docs/lab.png" alt="GeoComp project overview or core concept diagram" width="400"/>
</p>

## ✨ Main Features

* **Large-Scale Real-World Dataset (GeoComp)**:
    * Derived from real interaction data of 740,000 users over more than two years on the online geolocation gaming platform (tuxun.fun).
    * Contains 25 million metadata records and **over 3 million** geotagged street view locations, covering extensive global regions.
    * Each location has undergone thousands, even tens of thousands, of localization attempts by human players, embedding rich information about task difficulty and valuable real-world human performance benchmarks.
* **Human-Like Reasoning Framework (GeoCoT)**:
    * Proposes a novel multi-step Geospatial Chain-of-Thought (GeoCoT) framework, significantly enhancing the reasoning ability of Large Vision-Language Models (LVMs) in complex geolocation tasks.
    * Mimics the human reasoning process from macro-level context (climate, topography, vegetation) to micro-level details (language on signs, architectural styles, vehicle features), effectively integrating contextual and spatial clues from images.
    * Experiments demonstrate that GeoCoT can significantly improve geolocation accuracy (up to **25%**) while enhancing the interpretability of the model's decision-making process.
* **Comprehensive Evaluation Suite (GeoEval)**:
    * Includes metrics for comparing model reasoning processes with human expert-annotated "golden" reasoning, as well as assessments of the internal consistency of the model's own reasoning chain.
    * Introduces detailed hallucination evaluation dimensions (Object Hallucination OH, Fact Hallucination FH, Attribution Hallucination AH) to comprehensively ensure the reliability and truthfulness of the model's reasoning results.
* **Benchmark Models & Complete Code**:
    * Provides implementations of various geolocation benchmark models (`baseline`) for fair comparison by researchers.
    * Open-sources the complete code, including data processing (`Dataset`), the core method (`Geocot`), and evaluation (`Geoeval`), supporting community reproduction and extension.

## 📄 Paper

For detailed information about this project, methodology, and comprehensive experimental results, please refer to our arXiv paper:

**Geolocation with Real Human Gameplay Data: A Large-Scale Dataset and Human-Like Reasoning Framework**
[https://arxiv.org/abs/2502.13759](https://arxiv.org/abs/2502.13759)

### 💡 Rethinking the Geolocation Task

<p align="center">
  <img src="docs/rethinking.png" alt="Diagram comparing GeoCoT method with traditional geolocation methods" width="600"/>
</p>

Traditional geolocation methods primarily rely on classification (dividing the Earth into predefined grids) or retrieval (matching visually similar images in large-scale databases). While these methods have achieved some progress, they often exhibit limitations in localization accuracy, generalization capability to new regions, and the interpretability of results. Inspired by the natural "coarse-to-fine, progressively narrowing down the scope" process employed by human experts during geolocation, we propose a new paradigm for geolocation: **Leveraging large models to generate coherent, step-by-step natural language reasoning chains that ultimately deduce the precise geographic location of the image**. The GeoCoT framework is specifically designed to realize this generative reasoning paradigm, aiming to overcome the bottlenecks of traditional methods and enhance the accuracy, robustness, and transparency of localization.

<p align="center">
  <img src="docs/table1.png" alt="Table comparing GeoComp dataset with other datasets (Table 1)" width="700"/>
</p>

## 📁 Codebase Structure

```text
Geocomp/
├── docs/                 # Documentation and project-related static resources (e.g., GitHub Pages site files)
│   └── assets/           # Stores images, PDFs, etc., used in README and documentation
├── Hallucination/        # Manual hallucination evaluation data for model reasoning results
│   ├── GeoCoT.csv        # Hallucination evaluation results for the GeoCoT method
│   ├── GeoReasoners.csv  # Hallucination evaluation results for the GeoReasoners benchmark
│   └── GPT4o.csv         # Hallucination evaluation results for the GPT-4o benchmark
├── src/                  # Core project source code
│   ├── baseline/         # Implementation code for various geolocation baseline models
│   ├── Dataset/          # Code for dataset processing, loading, and interaction with Street View APIs
│   ├── Geocot/           # Implementation and testing code for the core GeoCoT reasoning framework
│   └── Geoeval/          # Implementation code for the GeoEval evaluation suite (including various metrics and tools)
├── requirements.txt      # List of Python dependencies for the project
├── README_zh.md          # This README file (Chinese version)
├── README.md             # README file (English version)
└── ...                   # Other configuration files, scripts, etc.
```
Key Directory Descriptions:

* **`src/baseline`**: Contains implementation code and running scripts for various baseline models used in comparative experiments.
* **`src/Dataset`**: Includes code related to data downloading, preprocessing, data loaders, and interacting with APIs like Google Street View to fetch image data (e.g., `street_view_api.py`).
* **`src/Geocot`**: Contains the core logic code implementing the GeoCoT reasoning framework, as well as scripts for running and testing the method.
* **`src/Geoeval`**: Provides the complete implementation of the GeoEval evaluation suite, including scripts for calculating geographic distance errors, various classification/regression metrics, similarity assessment between reasoning chains and ground truth, and hallucination detection functionalities.
* **`Hallucination`**: Contains the raw data (CSV format) from detailed manual hallucination evaluations performed on the reasoning outputs of different models (our method GeoCoT and benchmarks GeoReasoners, GPT-4o).
* **`docs`**: Stores images, charts (like `case.png`), and potentially supplementary PDF materials used in this documentation and the project homepage.

## 📊 Hallucination Evaluation

To thoroughly evaluate the credibility of the model-generated reasoning content, we conducted meticulous manual hallucination checks on the model outputs. The evaluation process strictly adhered to predefined criteria, primarily focusing on the following three types of hallucinatory errors:

1.  **Object Hallucination (OH):** The model describes objects, features, or elements that *do not actually exist* in the image.
2.  **Fact Hallucination (FH):** The model states information that *contradicts* generally accepted geographical, cultural, or common-sense facts (e.g., incorrect landmark names, inconsistent geographical relationships, inaccurate climate descriptions).
3.  **Attribution Hallucination (AH):** The model *incorrectly interprets* elements actually present in the image, or *erroneously attributes* their properties, origins, or meanings to the wrong country, region, culture, or object.

<p align="center">
  <img src="docs/human.png" alt="Hallucination Statistics" width="600"/>
</p>

Each evaluation sample was independently judged by human annotators with relevant geographical background knowledge. Annotators carefully compared the original street view image with the model's reasoning text, checking item by item for the presence of the three types of hallucination issues mentioned above. Detailed evaluation statistics are stored in the CSV files within the Hallucination/ directory.

## ⚙️ Installation
```bash
# Clone the repository
git clone [https://github.com/ZiruiSongBest/Geocomp.git](https://github.com/ZiruiSongBest/Geocomp.git)
cd Geocomp
# Create a virtual environment (recommended)
conda create --name geocomp python=3.10
conda activate geocomp
# Install dependencies
pip install -r requirements.txt # Please ensure requirements.txt exists and contains all dependencies
# Other necessary setup steps... (e.g., API key configuration)
```

## 🚀 Usage Instructions
```bash
# How to run GeoCoT for reasoning and prediction
python src/Geocot/run_geocot.py 
# How to use GeoEval for evaluation
python src/Geoeval/evaluate_model.py 
# How to run baseline models
python src/baseline/[some_baseline_model]/run.py --config [path_to_config_file]
```
## 📄 License

This project is licensed under the **MIT** License.
Please see the `LICENSE` file in the project root directory for details.

## 📧 Contact & Citation

**Contact**

If you have any questions about this project, or if you have used any part of this project in your research, please feel free to contact us through various channels.

**Citation**

If the dataset (GeoComp), method (GeoCoT), or evaluation tools (GeoEval) from this project have been helpful to your research work, please consider citing our paper:

```bibtex

```
