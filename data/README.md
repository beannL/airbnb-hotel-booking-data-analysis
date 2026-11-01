# 数据集说明

所有数据集均已随仓库提供，无需另行下载。Notebook 中以相对路径 `../data/文件名` 读取数据，从 `notebooks/` 目录直接运行即可。

| 文件名 | 大小（约） | 说明 |
|---|---|---|
| `Airbnb.csv` | 5 MB | 欧洲城市 Airbnb 房源数据，用于 01 EDA 与数据质量 |
| `hotel_bookings.csv` | 17 MB | 葡萄牙两家酒店预订记录（Antonio et al., 2019），用于 02/04 |
| `creditcard-reduced.csv` | 12 MB | 信用卡交易缩减版（32,764 条），用于 05 欺诈检测 |
| `Credit_approval.csv` | 15 KB | 信用审批小数据集，课程分类练习用 |
| `iris.txt` | 5 KB | Iris 经典教学数据集 |
| `Q5BTC-USD.csv` | 32 KB | Bitcoin 2018 年收盘价，用于 06 时间序列分析 |

数据来源：
- Airbnb：Kaggle - [Airbnb Price Prediction](https://www.kaggle.com/datasets/stevezhenghp/airbnb-price-prediction)
- Hotel Booking Demand：Kaggle - [Hotel booking demand](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand)，原始出处 Nuno Antonio et al., *Data in Brief*, 2019
- 信用卡交易：课程提供的缩减版，母集为 [Kaggle Credit Card Fraud Detection](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)
- Bitcoin 收盘价：课程提供的 `Q5BTC-USD.csv`
