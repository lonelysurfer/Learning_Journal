# Learning Journal

深度学习练习笔记仓库。每个项目放在独立目录中，数据和环境的说明见各项目自己的 README。

## 项目索引

| 项目 | 内容 | 任务类型 | 技术栈 | 数据集 |
| :--- | :--- | :--- | :--- | :--- |
| [CNN](./CNN/) | 基于 LeNet-5 的手写数字识别 | 图像多分类 | TensorFlow / Keras | MNIST |
| [MLP](./MLP/) | 北京 PM2.5 浓度回归预测 | 时间序列回归 | TensorFlow / Keras | UCI Beijing PM2.5 |

## 目录约定

```
Learning_Journal/
├── README.md          # 本索引
└── <项目名>/
    ├── README.md      # 该项目的依赖、数据集与运行说明
    └── *.ipynb        # 项目代码
```

数据集统一**不纳入版本控制**，需按各项目 README 的说明自行下载。

## 新增项目

1. 新建项目目录，放入 Notebook
2. 在项目目录内写 `README.md`（依赖、数据集来源与放置路径、运行方式）
3. 回到本文件，在上方索引表中新增一行
