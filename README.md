# Geolocation with Real Human Gameplay Data: A Large-Scale Dataset and Human-Like Reasoning Framework

[![arXiv](https://img.shields.io/badge/arXiv-2502.13759-b31b1b.svg)](https://arxiv.org/abs/2502.13759)
## 📝 简介

Geocomp 是一个专注于**图像地理定位** **Geolocation**的研究项目和代码库。地理定位任务旨在识别图像的拍摄地点，这对于导航、监控和文化遗产保护至关重要，但需要复杂的推理能力。当前方法往往产生粗糙、不精确且难以解释的定位结果，部分原因是现有数据集规模小、自动构建导致噪声多、任务难度不一致（要么过于简单，要么缺乏足够线索）。

为应对这些挑战，本项目提出了一个综合性的地理定位框架，包含三大核心组件：
1.  **GeoComp**: 一个从真实人类地理定位竞赛中收集的大规模、高质量数据集。
2.  **GeoCoT**: 一种新颖的、模仿人类思维链的地理推理方法（Geographical Chain-of-Thought）。
3.  **GeoEval**: 一套用于评估地理定位模型性能和推理过程的指标。

本项目旨在通过这套框架解决当前地理定位研究中的关键瓶颈，推动领域发展。

!(docs/assets/label.pdf)

## ✨ 主要特性

* **大规模真实世界数据集 (GeoComp)**:
    * 源自 74 万用户参与两年多的在线地理定位游戏 (tuxun.fun)。
    * 包含 2500 万条元数据记录和 **300 多万个**带有地理标签的地点，覆盖全球大部分地区。
    * 每个地点都经过数千至数万次人类玩家标注，提供了丰富的难度信息和真实的人类表现数据。
* **类人推理框架 (GeoCoT)**:
    * 一种新颖的多步骤地理链式思维（GeoCoT）框架，旨在增强大型视觉语言模型（LVM）在地理定位任务中的推理能力。
    * 通过模仿人类从宏观（气候、地貌）到微观（路牌、建筑细节）的推理过程，整合上下文和空间线索。
    * 显著提升地理定位准确率（最高达 **25%**）和结果的可解释性。
* **全面的评估体系 (GeoEval)**:
    * 包含与地面真实推理数据的比较以及内在逻辑评估。
    * 细致的幻觉评估（OH, FH, AH），确保模型推理的可靠性。
* **基准模型与代码**:
    * 提供多种基准模型的实现 (`baseline`)。
    * 包含数据处理 (`Dataset`)、核心方法测试 (`Geocot`) 和评估 (`Geoeval`) 的完整代码。

## 📄 论文

关于本项目的详细信息、方法和实验结果，请参阅我们的论文：

**Geolocation with Real Human Gameplay Data: A Large-Scale Dataset and Human-Like Reasoning Framework**
[https://arxiv.org/abs/2502.13759](https://arxiv.org/abs/2502.13759)

![GeoCoT 方法示意图](docs/assets/geocot_method.png)
![关键实验结果图](docs/assets/results_summary.png)

## 💡 重新思考地理定位任务

传统的地理定位方法主要依赖于分类（将地球划分为网格）或检索（匹配相似图像）。这些方法在精度和可扩展性方面存在局限。受人类逐步缩小范围（从宏观观察到微观细节）进行定位的启发，我们提出了一种新的范式：**通过生成式的、分步的自然语言推理过程来预测地理位置**。GeoCoT 框架正是为实现这一范式而设计，旨在提高定位的准确性和可解释性。

![地理定位范式对比图](docs/assets/paradigm_comparison.png) 
## 📁 代码库结构

Geocomp/├── docs/                  # 文档和可能的静态资源 (例如 GitHub Pages)│   └── assets/            # 存放图片、PDF 等资源 (例如 case.png, staticcopy.pdf 相关图)├── Hallucination/         # 模型推理结果的幻觉评估数据│   ├── GeoCoT.csv│   ├── GeoReasoners.csv│   └── GPT4o.csv├── src/                   # 主要源代码│   ├── baseline/          # 各种基准模型对应的部署代码│   ├── Dataset/           # 处理地理/统计数据的代码 (例如街景API交互)│   ├── Geocot/            # 测试和评估本项目核心方法 (GeoCoT) 的基准代码│   └── Geoeval/           # 使用大语言模型进行评估的代码和基准测试工具 (GeoEval)├── README_zh.md           # 本文件 (中文版)├── README.md              # 英文版 README└── ...                    # 其他配置文件、脚本等 (如 requirements.txt)
**关键目录说明:**

* **`src/baseline`**: 存放了用于比较的各种基准模型的实现和部署脚本。
* **`src/Dataset`**: 包含了数据收集（如使用 `street_view_api.py`）和预处理的代码。
* **`src/Geocot`**: 包含用于运行和评估我们提出的 `GeoCoT` 框架的代码。
* **`src/Geoeval`**: 提供了一套利用 LLM 进行地理空间推理任务评估的工具和脚本 (GeoEval)。这包括计算地理距离、分类指标、语义相似度、从文本预测坐标、幻觉检测等功能。
* **`Hallucination`**: 包含了对不同模型（如 GeoCoT, GeoReasoners, GPT-4o）输出进行人工幻觉评估的结果。
* **`docs/assets`**: 存放用于文档和 README 的图片、PDF 等资源。你可以将 `case.png` 以及从 `staticcopy.pdf` 等文件中提取的关键图表放在这里。

## 📊 幻觉评估

我们对模型的推理文本进行了细致的人工检查，以识别和量化幻觉现象。评估主要关注以下三个方面：

1.  **物体幻觉 (Object Hallucination, OH)**: 模型描述了图像中实际不存在的物体或元素。
2.  **事实幻觉 (Fact Hallucination, FH)**: 模型陈述了与地理事实（如地标、文化信息）不符的内容。
3.  **归因幻觉 (Attribution Hallucination, AH)**: 模型错误地解释了图像中存在的元素，或将其归因于错误的国家/地区或含义。

每个样本都由具备相关地理知识的人工标注员进行评估，他们会仔细比对图像和模型的推理文本，判断是否存在上述三类幻觉。评估结果存储在 `Hallucination/` 目录下的 CSV 文件中。

![幻觉评估结果统计图](docs/assets/hallucination_results.png)
![幻觉案例分析图](docs/assets/case.png)

## ⚙️ 安装

```bash
# 克隆仓库
git clone [https://github.com/](https://github.com/)[你的用户名]/Geocomp.git
cd Geocomp

# 创建虚拟环境 (推荐)
python -m venv venv
source venv/bin/activate  # Linux/macOS
# venv\Scripts\activate  # Windows

# 安装依赖
pip install -r requirements.txt # 请确保 requirements.txt 文件存在且包含所有依赖

# 其他必要的设置步骤... (例如：API密钥配置)
🚀 使用说明# 如何运行 GeoCoT 进行推理和预测
python src/Geocot/run_geocot.py --image [图像路径] --output [输出路径]

# 如何使用 GeoEval 进行评估
python src/Geoeval/evaluate_model.py --predictions [预测结果文件] --groundtruth [真实标签文件]

# 如何运行基准模型
python src/baseline/[某个基准模型]/run.py --config [配置文件路径]

# 如何进行幻觉分析 (如果提供了脚本)
# python tools/analyze_hallucination.py --input Hallucination/GeoCoT.csv

# 请根据你的项目实际情况修改或补充以上命令示例
🤝 贡献指南我们欢迎各种形式的贡献！如果你想为项目做出贡献，请 [说明贡献方式，例如：查阅 CONTRIBUTING.md 文件、提交 Pull Request 或 Issue]。📄 许可证本项目采用 [在此处填写许可证名称，例如：MIT] 许可证。详情请见 LICENSE 文件（如果创建了该文件）。📧 联系方式与引用如果您对本项目有任何疑问，或者在您的研究中使用了本项目，请联系 [你的邮箱地址] 或通过 GitHub Issues 提出。如果本项目的数据集 (GeoComp)、方法 (GeoCoT) 或评估工具 (GeoEval) 对您的研究有所帮助，请考虑引用我们的论文：@misc{song2025geocomp,
      title={Geolocation with Real Human Gameplay Data: A Large-Scale Dataset and Human-Like Reasoning Framework},
      author={Zirui Song and Jingpu Yang and Yuan Huang and Jonathan Tonglet and Zeyu Zhang and Tao Cheng and Meng Fang and Iryna Gurevych and Xiuying Chen},
      year={2025},
      eprint={2502.13759},
      archivePrefix={arXiv},
      primaryClass={cs.CV}
}
