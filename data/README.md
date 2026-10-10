# 数据集放置说明

为控制仓库体积，两个较大的 CSV 数据文件不随 Git 提交，请自行下载后放到本目录（`data/`）下，文件名保持如下：

| 文件名 | 大小（约） | 下载地址 |
|---|---|---|
| `Airbnb.csv` | 5 MB | https://www.kaggle.com/datasets/stevezhenghp/airbnb-price-prediction |
| `hotel_bookings.csv` | 17 MB | https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand |
| `iris.txt` | 5 KB | 已随仓库提供，无需下载 |

放置后本目录结构为：

```
data/
├── Airbnb.csv
├── hotel_bookings.csv
├── iris.txt
└── README.md
```

Notebook 中以相对路径 `../data/文件名` 读取数据，从 `notebooks/` 目录直接运行即可。
