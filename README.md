# 面向资源受限场景的轻量类增量学习

Python 程序设计与实现课程期末项目。研究在固定小内存、无预训练的小骨干条件下，用轻量样本回放、类原型与原型感知的 logit 校准缓解类增量学习中的灾难性遗忘。

## 当前状态

- [x] 选题报告
- [ ] 数据划分与数据管线
- [ ] 基线：Fine-tuning / EWC / LwF / Experience Replay / DER++
- [ ] 原型感知的 logit 校准
- [ ] 主实验、消融与结果分析
- [ ] 论文与最终打包

## 环境

- Python 3.12
- PyTorch（按本机 CUDA 版本安装）
- 其余依赖见 `requirements.txt`

## 数据集

- Split-MNIST、Split-FashionMNIST：官方 60k/10k 划分，按类别切成 5 个任务，每任务 2 类。
- Split-CIFAR-10：官方 50k/10k 划分，按类别切成 5 个任务，每任务 2 类。

数据集由 `torchvision` 自动下载，不提交到仓库。划分脚本与随机种子将记录在 `src/cllearn/data.py`。

## 快速开始

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt

python train.py --config configs/split_mnist_finetune.yaml
```

> 当前为项目骨架，训练入口与配置文件将在后续提交中补充。

## 目录结构

```text
project/
  configs/            # YAML 实验配置
  logs/               # 运行日志（保留用于复现）
  results/            # 指标 CSV 与图表
  src/cllearn/        # 数据、模型、缓冲、方法与指标
  tests/              # pytest 测试
  train.py
  evaluate.py
  requirements.txt
  README.md
```

## 可复现性

- 随机种子：数据划分固定 42；模型训练使用 42 / 43 / 44。
- 任务顺序：固定顺序，所有方法共享。
- 超参数：待主实验确定后写入本文件。
- 运行环境：Python 3.12，PyTorch 版本与 CUDA 版本在安装后补充。
