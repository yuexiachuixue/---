# 基于空-频注意力混合模型的城市区域无线电地图估计研究与实现代码

## 说明
数据集采用公开的大规模无线电地图数据集RadioMapSeer，请自行下载并将各文件放在sjj文件下

## 目录结构

```text
├─ app.py                       # Flask Web 演示入口，通过浏览器上传 5 张输入图，调用模型预测无线电地图并返回可视化结果
├─ dataset.py                   # 数据集加载模块，从 sjj 中读取 5 通道输入和目标信号图
├─ evaluate.py                  # 评估指标模块，计算 RMSE、MAE、RSRP MAE（dB）、PSNR、SSIM 等
├─ losses.py                    # 复合损失函数模块，包含像素损失、频谱损失、梯度损失及 GAN 对抗损失
├─ main.py                      # 训练/评估/对比/可视化命令行主入口，支持 --mode train、compare、eval、visualize
├─ models.py                    # 定义四种模型（FDANet、RadioUNet、RadioGAN、RadioViT），包含物理先验模块 PhysicsEncoder
├─ monitor.py                   # 训练进度监控模块，包含进度条、GPU/内存统计、曲线图保存、训练摘要
├─ train.py                     # 训练循环与优化逻辑，包含普通监督训练器 Trainer 和 GAN 训练器 GANTrainer
├─ checkpoints/
│   ├─ ablation/                # 归档消融实验结果与模型
│   ├─ comparison_results.json  # 不同模型对比结果汇总
│   ├─ config.json              # 训练或评估配置参数
│   ├─ efficiency_results.json  # 性能/效率对比结果
│   ├─ fdanet_best.pth          # FDANet 最佳权重文件
│   ├─ fdanet_history.jsonl     # FDANet 训练历史记录（每 epoch 指标）
│   ├─ fdanet_training_curves.png # FDANet 训练曲线图
│   ├─ fdanet_visualization.png # FDANet 预测可视化示例
│   ├─ radiogan_best.pth        # RadioGAN 最佳权重文件
│   ├─ radiogan_history.jsonl   # RadioGAN 训练历史记录
│   ├─ radiogan_training_curves.png
│   ├─ radiogan_visualization.png
│   ├─ radiounet_best.pth       # RadioUNet 最佳权重文件
│   ├─ radiounet_history.jsonl
│   ├─ radiounet_training_curves.png
│   ├─ radiounet_visualization.png
│   ├─ radiovit_best.pth        # RadioViT 最佳权重文件
│   ├─ radiovit_epoch20.pth     # RadioViT epoch20 权重
│   ├─ radiovit_history.jsonl
│   ├─ radiovit_training_curves.png
│   ├─ radiovit_visualization.png
│   └─ smoke/                   # 小样本/冒烟测试结果
├─ sjj/
│   ├─ antennas/                # 基站位置图
│   ├─ antennasWHeight/         # 基站高度图
│   ├─ buildings_complete/      # 建筑物二值图
│   ├─ buildingsWHeight/        # 建筑物高度图
│   ├─ gain/                    # 信号增益（Ground-truth）
│   └─ roads/                   # 道路图
└─ templates/
    └─ index.html               # Flask 前端页面模板，展示上传表单和模型预测结果
