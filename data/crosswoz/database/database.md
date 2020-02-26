# database

- 值缺失一律为 None，导出到json中显示为null，从json导入后是None。
- 周边xx具有对称性，A在B的周边里则B也在A的周边里。条目较多，显示时可截取前五个。
- 门票、评分、人均消费、价格 要用区间查询，支持 小于"<x"|大于">x"|区间(包含端点)"x-y"。
- *: 允许查询的内容。string 类型用字符串匹配，list of string 逐个匹配，int/float 涉及大小比较。**推荐菜**和**酒店设施**支持多个条件匹配，用空格分隔，如 "东北杀猪菜 锅包肉"，检索时要求两个都出现在推荐菜中。
- 出租数据库是模板，不查询，后处理时随机替换占位符。

### 景点

- 领域: "景点"
- 名称*: string
- 地址: string
- 地铁: string
- 电话: string
- 门票*: int (缺失则为None)
- 游玩时间*: string
- 评分*: float (缺失则为None)
- 周边景点*: list of string
- 周边餐馆*: list of string
- 周边酒店*: list of string



### 餐馆

- 领域: "餐馆"
- 名称*: string
- 地址: string
- 地铁: string
- 电话: string
- 营业时间: string
- 推荐菜*: list of string
- 人均消费*: int
- 评分*: float (缺失则为None)
- 周边景点*: list of string
- 周边餐馆*: list of string
- 周边酒店*: list of string



### 酒店

- 名称*: string
- 酒店类型*: string
- 地址: string
- 地铁: string
- 电话: string
- 酒店设施*: list of string
- 价格*: int (缺失则为None)
- 评分*: float
- 周边景点*: list of string
- 周边餐馆*: list of string
- 周边酒店*: list of string




### 地铁

- 名称*: string
- 地铁*: string (缺失则为None)



### 出租

```
车型：['别克', '比亚迪', '奔腾', '雪佛兰', '雪铁龙', '标致', '福特', '传祺', '本田', '现代', '吉利', '马自达', '日产', '丰田', '大众']
车牌：第一位是大写字母，后面6位是数字
```



### Query function

```python
from db import Database
db = Database()
db.query('景点', { '名称': '圆明园' })
db.query('餐馆', { '评分': [3.7, 4.0], '周边景点': '清华大学', '推荐菜': '冻豆腐 涮羊肉' })
db.query('酒店', { '价格': [None, 300], '酒店设施': '行李寄存 租车', '周边景点': '仁和公园' })
db.query('地铁', { '起点': '清华', '终点': '北大' })
db.query('出租', { '起点': '北京南站', '终点': '北京站' })
```

