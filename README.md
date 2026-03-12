# 深度学习实验：MNIST 手写数字识别全维度对比分析

---

###  基本信息
- **架构**：MLP、LeNet-5、Strong-CNN(无/有数据增强)   
- **日期**：2026-03-10  
- **环境**：Python 3.12 (uv managed), PyTorch 2.10, CPU Only

---

###  实验目标
本实验通过构建 **2 种训练策略 × 4 组模型变体** 的实验矩阵，深度探索深度学习性能的影响因子：
1. **架构差异 (Architecture)**：对比全连接网络 (MLP) 与不同年代的卷积架构 (LeNet-5, Strong CNN)。
2. **优化策略 (Optimization)**：验证**动态学习率 (LR Scheduler)** 对不同复杂度模型收敛稳定性的贡献。
3. **数据工程 (Data Engineering)**：孤立变量验证**数据增强 (Data Augmentation)** 对现代深层 CNN 泛化能力的提升。

---

###  实验设计矩阵 (Experimental Matrix)

本实验共包含 8 组独立实验，旨在通过“交叉对比”建立完整的性能认知：

| 实验组别 | 模型架构 (Model) | 数据增强 (Aug) | 学习率策略 (LR Strategy) | 核心观察点 |
| :--- | :--- | :--- | :--- | :--- |
| **G1-Exp1** | Simple MLP | No | Fixed (0.001) | 基础性能 Baseline |
| **G1-Exp2** | LeNet-5 | No | Fixed (0.001) | 经典卷积的效率 |
| **G1-Exp3** | Strong CNN | No | Fixed (0.001) | 现代组件的增益 |
| **G1-Exp4** | Strong CNN | **Yes** | Fixed (0.001) | 数据增强的独立影响 |
| **G2-Exp5** | Simple MLP | No | **StepLR** | 动态 LR 对浅层网络的作用 |
| **G2-Exp6** | LeNet-5 | No | **StepLR** | 动态 LR 对经典卷积的作用 |
| **G2-Exp7** | Strong CNN | No | **StepLR** | 动态 LR 对深层网络的作用 |
| **G2-Exp8** | Strong CNN | **Yes** | **StepLR** | **性能极限探索 (全配置优化)** |


---

###  实验导航 (Notebook Roadmap)

| 阶段 | 单元格 (Cell) | 内容说明 |
| :--- | :--- | :--- |
| **I. 环境与配置** | Cell 2 | 库导入、硬件信息验证、随机种子锁定、全局 CONFIG 定义 |
| **II. 数据工程** | Cell 3 | `get_dataloader` 封装：支持动态开启数据增强 |
| **III. 模型库** | Cell 4 | 定义 MLP、LeNet5、StrongCNN 类及参数量统计工具 |
| **IV. 核心引擎** | Cell 5 | 封装通用 `Trainer` 类，支持自动记录 History 及 LR 调度 |
| **V. 实验执行** | Cell 6 | 全自动循环执行 8 组实验逻辑，收集实验指标 |
| **VI. 结果可视化** | Cell 7-8 | 绘制多维度 Loss/Acc 对比曲线及最终性能汇总表 |

---