# Geocomp: [在此处添加项目副标题或简短描述]

[![arXiv](https://img.shields.io/badge/arXiv-2502.13759-b31b1b.svg)](https://arxiv.org/abs/2502.13759)
**中文** | [English](README.md) ## 📝 简介

Geocomp 是一个专注于 [在此处简要说明项目的核心目标，例如：地理图像理解、地理定位、视觉问答等] 的研究项目/代码库。本项目旨在 [在此处说明项目的主要贡献或解决的问题]。

## ✨ 主要特性

* **[特性 1]**: [简要描述第一个关键特性]
* **[特性 2]**: [简要描述第二个关键特性]
* **全面的基准测试**: 包含多种基准模型的实现 (`baseline`) 和详细的评估代码 (`Geoeval`, `Geocot`)。
* **细致的幻觉评估**: 对模型输出进行严格的人工幻觉评估 (`Hallucination`)。
* **[其他特性]**: [例如：易于扩展、包含数据集处理工具等]

## 📄 论文

关于本项目的详细信息、方法和实验结果，请参阅我们的论文：

**[在此处添加论文标题]**
[https://arxiv.org/abs/2502.13759](https://arxiv.org/abs/2502.13759)

## 📁 代码库结构

Geocomp/├── docs/                  # 文档和可能的静态资源 (例如 GitHub Pages)│   └── assets/            # 存放图片、PDF 等资源├── Hallucination/         # 模型推理结果的幻觉评估数据│   ├── GeoCoT.csv│   ├── GeoReasoners.csv│   └── GPT4o.csv├── src/                   # 主要源代码│   ├── baseline/          # 各种基准模型对应的部署代码│   ├── Dataset/           # 处理地理/统计数据的代码 (例如街景API交互)│   ├── Geocot/            # 测试和评估本项目核心方法的基准代码│   └── Geoeval/           # 使用大语言模型进行评估的代码和基准测试工具├── README.md              # 本文件└── ...                    # 其他配置文件、脚本等
**关键目录说明:**

* **`src/baseline`**: 存放了用于比较的各种基准模型的实现和部署脚本。
* **`src/Dataset`**: 包含了数据收集（如使用 `street_view_api.py`）和预处理的代码。
* **`src/Geocot`**: 包含用于运行和评估我们提出的 `GeoCoT` (或其他核心方法) 的代码。
* **`src/Geoeval`**: 提供了一套利用 LLM 进行地理空间推理任务评估的工具和脚本。这包括计算地理距离、分类指标、语义相似度、从文本预测坐标等功能。
* **`Hallucination`**: 包含了对不同模型（如 GeoCoT, GeoReasoners, GPT-4o）输出进行人工幻觉评估的结果。

## 📊 幻觉评估

我们对模型的推理文本进行了细致的人工检查，以识别和量化幻觉现象。评估主要关注以下三个方面：

1.  **物体幻觉 (Object Hallucination, OH)**: 模型描述了图像中实际不存在的物体或元素。
2.  **事实幻觉 (Fact Hallucination, FH)**: 模型陈述了与地理事实（如地标、文化信息）不符的内容。
3.  **归因幻觉 (Attribution Hallucination, AH)**: 模型错误地解释了图像中存在的元素，或将其归因于错误的国家/地区或含义。

每个样本都由具备相关地理知识的人工标注员进行评估，他们会仔细比对图像和模型的推理文本，判断是否存在上述三类幻觉。评估结果存储在 `Hallucination/` 目录下的 CSV 文件中。

## ⚙️ 安装

```bash
# 在此处添加详细的安装步骤
# 例如：克隆仓库
git clone [https://github.com/your_username/Geocomp.git](https://github.com/your_username/Geocomp.git)
cd Geocomp

# 创建虚拟环境 (推荐)
python -m venv venv
source venv/bin/activate  # Linux/macOS
# venv\Scripts\activate  # Windows

# 安装依赖
pip install -r requirements.txt # 假设你有 requirements.txt 文件

# 其他必要的设置步骤...
🚀 使用说明# 在此处添加如何运行代码的示例
# 例如：如何运行基准测试
python src/Geocot/run_benchmark.py --config [配置文件路径]

# 例如：如何进行评估
python src/Geoeval/evaluate_model.py --model [模型名称] --data [数据路径]

# 例如：如何进行幻觉分析 (如果提供了脚本)
# python tools/analyze_hallucination.py --input Hallucination/GeoCoT.csv
🤝 贡献指南我们欢迎各种形式的贡献！请阅读 CONTRIBUTING.md 文件（如果创建了该文件）了解详细信息。📄 许可证本项目采用 [在此处填写许可证名称，例如：MIT] 许可证。详情请见 LICENSE 文件（如果创建了该文件）。📧 联系方式与引用如果您对本项目有任何疑问，或者在您的研究中使用了本项目，请联系 [你的邮箱地址] 或通过 GitHub Issues 提出。如果本项目对您的研究有所帮助，请考虑引用我们的论文：@misc{your_citation_key_2025,
      title={[在此处填写论文标题]},
      author={[在此处填写作者列表]},
      year={2025},
      eprint={2502.13759},
      archivePrefix={arXiv},
      primaryClass={cs.CV} # 或者适合的分类
}
