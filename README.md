[![Ask DeepWiki](https://deepwiki.com/badge.svg)](https://deepwiki.com/wangzaiyu482/Fed)
基于联邦学习的隐私计算平台（医疗影像应用）

端云协同架构，支持多机构分布式模型训练，保护数据隐私的同时提升诊断精度

🌟 项目亮点
隐私保护优先
采用联邦学习（FedAvg/FedProx 等策略）实现数据不出本地，结合差分隐私技术，确保医疗影像数据隐私安全。
通过Flower框架实现端云协同，本地端仅上传模型参数更新，避免原始数据泄露。
多模态支持与性能优化
支持医学图像（如 TIFF 格式）分类任务，集成 ResNet50 等预训练模型，适配边缘设备算力限制。
通信效率优化：通过梯度稀疏化和量化压缩，单轮训练通信量控制在 10MB 以内，适配医院内网环境。
工程化与可视化
前后端分离架构：前端使用 Vue 实现参数配置和训练监控，后端基于 Spring Boot+Python 混合开发。
实时可视化：训练过程中动态展示准确率、损失值、混淆矩阵等指标，支持模型下载与评估报告生成。

📦 核心功能
模块	功能描述
联邦学习管理	支持 FedAvg、FedProx、FedMedian 等多种聚合策略，动态配置训练轮数、客户端数量等参数。
数据处理	医学图像预处理（Resize、旋转、翻转），支持自定义数据集分区（IID/Non-IID 场景）。
模型训练	本地端独立训练模型，服务器聚合全局模型，支持 ResNet50 和自定义 CNN 模型（如 CancerModel）。
可视化监控	实时展示训练进度、指标曲线（ECharts），支持历史训练记录查询。
安全与存储	MySQL 存储配置元数据，Redis 缓存高频访问数据，模型参数加密存储。
🔧 技术栈

后端
核心框架：Spring Boot（Java） + Flower（Python 联邦学习框架）
通信技术：gRPC（跨语言通信） + Redis（状态缓存）
数据库：MySQL（结构化数据） + Redis（非结构化数据）
算法实现：PyTorch（模型训练） + NumPy（参数处理）
前端
框架：Vue.js + Element-UI
可视化：ECharts + JavaScript
工具链
配置管理：YAML + 环境变量（.env）
日志监控：Log4j + Flower 内置日志系统
模型部署：Docker + Kubernetes（可选）

🚀 快速开始
1. 环境准备
bash
# 后端环境（Python）  
conda create -n fl-platform python=3.8  
conda activate fl-platform  
pip install -r requirements.txt  

# 前端环境  
npm install -g @vue/cli  
cd frontend  
npm install  
2. 配置文件
复制config_template.yml为config.yml，修改数据库连接和服务器地址：
yaml
federated:  
    server_address: "127.0.0.1:8080"  
    num_clients: 4  
    strategy: "FedAvg"  
database:  
    mysql:  
    host: "localhost"  
    port: 3306  
    username: "root"  
    password: "your-password"  

3. 启动服务
bash
# 启动后端服务器  
python startServer.py  

# 启动前端应用  
nginx部署
4. 客户端运行
bash
# 启动本地端（多个实例）  
python StartClient.py --client-id 0  
python StartClient.py --client-id 1  
📖 使用指南
参数配置：通过前端页面设置训练轮数、客户端数量、聚合策略等参数。
数据准备：将医学影像数据集按分区存储，通过DatasetUtil.py加载数据。
模型训练：启动服务器和本地端，自动开始联邦训练，过程中可查看实时指标。
模型评估：训练完成后下载全局模型，使用验证集评估准确率和隐私保护效果。
📋 示例数据
数据集结构：
plaintext
dataset/  
├── train_labels.csv  # 标签文件（包含id和label）  
└── train/           # 图像文件（.tif格式）  

示例脚本：load_data.py实现数据集分区和加载，支持自定义数据预处理逻辑。
📌 注意事项
确保所有本地端和服务器网络连通（建议使用局域网）。
医疗数据需提前进行脱敏处理，符合 HIPAA/GDPR 等隐私法规。
首次训练建议使用小数据集（如 1000 张图像）测试流程稳定性。

联系方式：邮箱xiaoxiongchong3@gmail.com
2635114408@qq.com
