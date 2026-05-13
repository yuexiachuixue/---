# ---
基于空-频注意力混合模型的城市区域无线电地图估计研究与实现代码
其目录结构为：
├─ app.py
├─ dataset.py
├─ evaluate.py
├─ losses.py
├─ main.py
├─ models.py
├─ monitor.py
├─ train.py
├─ checkpoints/
│   ├─ ablation/
│   ├─ comparison_results.json
│   ├─ config.json
│   ├─ efficiency_results.json
│   ├─ fdanet_best.pth
│   ├─ fdanet_history.jsonl
│   ├─ fdanet_training_curves.png
│   ├─ fdanet_visualization.png
│   ├─ radiogan_best.pth
│   ├─ radiogan_history.jsonl
│   ├─ radiogan_training_curves.png
│   ├─ radiogan_visualization.png
│   ├─ radiounet_best.pth
│   ├─ radiounet_history.jsonl
│   ├─ radiounet_training_curves.png
│   ├─ radiounet_visualization.png
│   ├─ radiovit_best.pth
│   ├─ radiovit_epoch20.pth
│   ├─ radiovit_history.jsonl
│   ├─ radiovit_training_curves.png
│   ├─ radiovit_visualization.png
│   └─ smoke/
├─ sjj/
│   ├─ antennas/
│   ├─ antennasWHeight/
│   ├─ buildings_complete/
│   ├─ buildingsWHeight/
│   ├─ gain/
│   └─ roads/
├─ templates/
│   └─ index.html
说明：

app.py
Flask Web 演示入口
通过浏览器上传 5 张输入图，调用模型预测无线电地图，并返回可视化结果
main.py
训练/评估/对比/可视化的命令行主入口
支持 --mode train、--mode compare、--mode eval、--mode visualize
models.py
定义四种模型：FDANet、RadioUNet、RadioGAN、RadioViT
包含物理先验模块 PhysicsEncoder
train.py
训练循环与优化逻辑
包括普通监督训练器 Trainer 和 GAN 训练器 GANTrainer
dataset.py
数据集加载模块
从 sjj 中读取 5 通道输入和目标信号图
evaluate.py
评估指标模块
计算 RMSE、MAE、RSRP MAE（dB）、PSNR、SSIM 等
losses.py
复合损失函数模块
包含像素损失、频谱损失、梯度损失，以及 GAN 对抗损失
monitor.py
训练进度监控模块
包括进度条、GPU/内存统计、曲线图保存、训练摘要
index.html
Flask 前端页面模板

用于展示上传表单和模型预测结果
检查点目录 checkpoints
comparison_results.json
不同模型对比结果汇总
config.json
训练或评估配置参数
efficiency_results.json
性能/效率对比结果
fdanet_best.pth、radiounet_best.pth、radiogan_best.pth
各模型最佳权重文件
radiovit_best.pth、radiovit_epoch20.pth
Vision Transformer 模型权重
*_history.jsonl
训练历史记录，包含每 epoch 的指标
*_training_curves.png
训练曲线图
*_visualization.png
预测可视化示例
ablation/
归档消融实验结果与模型
smoke/
小样本/冒烟测试结果

数据集目录 sjj
antennas/
基站位置图
antennasWHeight/
基站高度图
buildings_complete/
建筑物二值图
buildingsWHeight/
建筑物高度图
roads/
道路图
gain/
信号增益（Ground-truth）
