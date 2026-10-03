# CNN — 基于 LeNet-5 的手写数字识别

用经典卷积神经网络 LeNet-5 完成 MNIST 手写数字（0-9）多分类。

## 文件

| 文件 | 说明 |
| :--- | :--- |
| `LeNet.ipynb` | 完整实验：数据探索 → 建模 → 训练 → 评估 → 错误分析 |
| `best_lenet5.keras` | 训练过程中验证集表现最好的权重（`ModelCheckpoint` 保存） |

## 环境依赖

```bash
pip install tensorflow numpy matplotlib seaborn scikit-learn jupyter
```

## 数据集

**MNIST**，无需手动下载。Notebook 通过 Keras 内置接口自动获取：

```python
(X_train, y_train), (X_test, y_test) = tf.keras.datasets.mnist.load_data()
```

- 规模：60,000 张训练图 + 10,000 张测试图
- 格式：28×28 灰度图

首次运行会自动下载并缓存到 `~/.keras/datasets/`。

## 模型结构

| 层 | 类型 | 输入尺寸 | 配置 | 输出尺寸 | 参数量 |
| :--- | :--- | :--- | :--- | :--- | ---: |
| C1 | Conv2D | 28×28×1 | 6 个 5×5 核 | 28×28×6 | 156 |
| S2 | MaxPooling2D | 28×28×6 | 2×2 | 14×14×6 | 0 |
| C3 | Conv2D | 14×14×6 | 16 个 5×5 核 | 10×10×16 | 2,416 |
| S4 | MaxPooling2D | 10×10×16 | 2×2 | 5×5×16 | 0 |
| C5 | Conv2D | 5×5×16 | 120 个 5×5 核 | 1×1×120 | 48,120 |
| F6 | Dense | 120 | ReLU + Dropout(0.5) | 84 | 10,164 |
| Output | Dense | 84 | Softmax | 10 | 850 |

## 训练配置

- **优化器**：Adam
- **损失函数**：Categorical Crossentropy
- **回调函数**：
  - `ModelCheckpoint` — 保存验证集最优权重，防止训练末期过拟合
  - `ReduceLROnPlateau` — 验证集 Loss 停滞时自动降低学习率
  - `EarlyStopping` — 连续 5 轮无改善则提前终止（`restore_best_weights=True`）

## 评估方式

1. Loss / Accuracy 训练曲线
2. 测试集混淆矩阵
3. 错误样本可视化与归因分析（如 5 误判为 3、8 误判为 5）

Notebook 末尾附有 11 道自测题，覆盖预处理原理、卷积层参数量推导、Dropout 机制、早停与学习率衰减、以及 MNIST 到真实场景（银行支票识别）的领域适应问题。
