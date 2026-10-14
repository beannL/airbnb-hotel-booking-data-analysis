# 短租与酒店预订数据分析：数据质量、特征选择、客户分群与欺诈检测分类

> 香港城市大学 · MSc in Electronic Commerce · IS6400 课程项目（个人独立完成）
> 技术栈：Python / pandas / scikit-learn / Matplotlib / Seaborn

## 项目简介

基于三个真实数据集，使用 Python 完成从**数据质量评估、探索性数据分析（EDA）、特征选择、无监督聚类分群到不平衡监督分类建模**的完整数据分析流程：

- **Airbnb 房源数据**：约 6.8 万条欧洲城市房源记录，覆盖房价、房源类型、容纳人数、评分等字段；
- **Hotel Booking Demand 酒店预订数据**：119,390 条葡萄牙两家酒店的预订记录、32 个字段（Antonio et al., *Data in Brief*, 2019）；
- **信用卡交易数据**：32,764 条脱敏交易记录（PCA 变换后的 V1–V28 特征），其中欺诈交易 492 条，用于不平衡分类与集成模型对比。

## Notebook 导航

建议按编号顺序阅读：

| Notebook | 内容 | 方法 |
|---|---|---|
| [01_airbnb_eda_and_data_quality.ipynb](notebooks/01_airbnb_eda_and_data_quality.ipynb) | Airbnb 描述统计、数据质量评估、价格相关性分析 | 均值/中位数/KNN 插补对比、IQR 与 Z-score 异常检测、StandardScaler 与 RobustScaler 对比、相关系数与热力图 |
| [02_hotel_booking_cancellation_analysis.ipynb](notebooks/02_hotel_booking_cancellation_analysis.ipynb) | 酒店预订渠道与取消行为分析 | 频数表、分组聚合、列联表（crosstab）、热力图 |
| [03_feature_selection.ipynb](notebooks/03_feature_selection.ipynb) | 特征选择方法对比 | 卡方检验、ANOVA F 值（Filter）；序列前向选择、随机森林 RFE（Wrapper） |
| [04_hotel_customer_segmentation.ipynb](notebooks/04_hotel_customer_segmentation.ipynb) | 酒店客户聚类分群 | K-Means、二分 K-Means、DBSCAN、层次聚类对比；肘部法则与轮廓系数选 K；客群画像 |
| [05_credit_card_fraud_classification.ipynb](notebooks/05_credit_card_fraud_classification.ipynb) | 信用卡欺诈检测：集成分类模型对比与不平衡处理 | 决策树、随机森林、Bagging、AdaBoost、Stacking 对比；准确率/精确率/召回率/F1 与混淆矩阵；`class_weight='balanced'` 类别加权 |

## 主要分析结论

**数据质量（Airbnb）**
- `review_scores_rating` 缺失率达 22.4%，其余字段缺失率很低；
- 对比三种插补方法：均值插补会明显压缩标准差（7.83 → 6.90），**KNN 插补对原始分布的保持最好**；
- IQR 法在偏态变量上识别出的异常值多于 Z-score 法，说明数据存在偏态与极端值，分析时更适合采用基于分位数的稳健方法。

**价格影响因素（Airbnb）**
- 容纳人数（accommodates）与 log 房价相关性最高（r = 0.58），其次为卧室数（0.48）与床位数（0.47）；评分与房价几乎不相关（r = 0.06）；
- Loft 均价最高、公寓最低；旧金山（SF）房价中位数最高，芝加哥最低；
- 相关不等于因果，区位、设施与需求等因素未纳入该相关性分析。

**渠道与取消行为（酒店预订）**
- Online TA 渠道预订量最大（约 47%）；不同渠道取消率差异显著：**团体订单（Groups）取消率约 61%，而直客（Direct）仅约 15%**，企业协议客户约 19%，渠道特征对取消预测有明显价值。

**客户分群（酒店预订）**
- 在 13 个预订行为特征上对比多种聚类算法后，因数据量大（约 12 万条）选用 K-Means，结合肘部法则与轮廓系数确定 K = 2；
- 类簇 1（约 69%）：**短住经济型**，平均 ADR（日均房价）约 87、特殊需求少；类簇 2（约 31%）：**长住高价值型**，平均 ADR 约 136、入住夜数更长、特殊需求与同行人数更多；
- 轮廓系数约 0.20，说明两类之间存在一定重叠、分群结构偏弱，特征工程或更细的 K 值仍有改进空间（如实保留该结果）。

**欺诈检测分类（信用卡）**
- 在欺诈占比仅约 1.5% 的不平衡样本上对比五种模型，**决策树与 Bagging 表现最好（F1 = 0.9949，召回率 0.9898）**，AdaBoost 次之（F1 = 0.9924）；随机森林在本实验浅树（max_depth=2）配置下召回率最低（0.8173），漏掉更多欺诈交易；
- 对不平衡问题，设置 `class_weight='balanced'` 后召回率由 0.9746 提升至 0.9848（漏判欺诈由 5 笔降至 3 笔），F1 由 0.9846 升至 0.9898；欺诈场景下召回率比整体准确率更重要。

## 目录结构

```
airbnb-hotel-booking-data-analysis/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   ├── README.md            # 数据集下载说明（大文件不入库）
│   └── iris.txt             # Iris 小数据集（随仓库提供）
└── notebooks/
    ├── 01_airbnb_eda_and_data_quality.ipynb
    ├── 02_hotel_booking_cancellation_analysis.ipynb
    ├── 03_feature_selection.ipynb
    ├── 04_hotel_customer_segmentation.ipynb
    └── 05_credit_card_fraud_classification.ipynb
```

## 复现方式

1. 安装依赖：`pip install -r requirements.txt`
2. 按 [data/README.md](data/README.md) 下载三个 CSV 数据集并放入 `data/` 目录；
3. 按 01 → 05 顺序运行各 notebook（Jupyter 中可 Kernel → Restart & Run All）。

## 数据集来源

- Airbnb 价格数据：Kaggle - [Airbnb Price Prediction](https://www.kaggle.com/datasets/stevezhenghp/airbnb-price-prediction)
- Hotel Booking Demand：Kaggle - [Hotel booking demand](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand)，原始出处 Nuno Antonio, Ana Almeida, Luis Nunes, *Hotel booking demand datasets*, Data in Brief, 2019
- 信用卡交易数据：课程提供的 `creditcard-reduced.csv` 为缩减版（32,764 条），母集为 Kaggle - [Credit Card Fraud Detection](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)（ULB - Université Libre de Bruxelles）
- Iris：UCI / scikit-learn 经典教学数据集

## 说明

本项目为香港城市大学 IS6400 课程个人作业整理而成：数据集与分析任务由课程指定，全部代码实现、实验对比与分析结论为个人完成；Notebook 由原始提交文件重新整理与排版，未改变分析过程与结果。
