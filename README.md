# Setup mongodb on cloud
- https://cloud.mongodb.com/ 
- https://www.mongodb.com/docs/mongodb-shell/

# Insert database
```
db.products.drop();
use products;

var items = ["card", "envelope", "stamps", "book", "pen", "notebook", "pencil", "eraser", "sharpener", "folder"];
var categories = ["stationery", "stationery", "stationery", "books", "stationery", "books", "stationery", "stationery", "stationery", "office supplies"];
var countries = ["Viet Nam", "USA", "China", "Lao", "Thai Lan", "Anh", "Đức", "Hà Lan", "Nga", "Ấn độ"];

var records = [];
for (var i = 0; i < 50000; i++) {
    var record = {
        name: items[Math.floor(Math.random() * items.length)],
        qty: Math.floor(Math.random() * 100) + 1,
        date: new Date().getTime(),
        category: categories[Math.floor(Math.random() * items.length)],
        contry: countries[Math.floor(Math.random() * items.length)],
    };
    records.push(record);
}

db.products.insertMany(records);

dn.runCommand({collStats: "products"});
```
# execution plan (chiến lược thực thi)

```
db.products.find({ name: "card", qty: 15 }).explain("excutionStats");
```

# Index

1. Đánh chỉ mục một trường:
  + Ưu điểm: Đơn giản dễ bảo trì, tiết kiệm không gian lưu trữ, phù hợp cho việc truy vấn dữ liệu trên 1 trường thường xuyên.
  + Nhược điểm: Không hiệu quả cho việc truy vấn nhiều trường, các truy vấn phức tạp khó tối ưu

2. Đánh chỉ mục trên nhiều trường (tối đa là 5 trường):
  + Ưu điểm: Tối ưu hóa thời gian truy vấn cho trường hợp truy vấn nhiều trường. 
  + Nhược điểm: Tốn không gian lưu trữ. việc I/O trên DB sẽ mất nhiều thời gian xử lý hơn.

 
----> Qui tắc: Truy vấn phải chứa chỉ mục bên trái dựa trên thứ tự tạo chỉ mục.

Ví dụ:

```
db.products.createIndex({name: 1, qty: -1, category: 1});
```

![image](https://github.com/user-attachments/assets/f80c9bf4-774a-43bc-b2a1-f3825a06ead5)






