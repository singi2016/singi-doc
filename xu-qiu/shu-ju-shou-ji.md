# 数据列表

1. 国家省市区街道
2. 地铁
3. 机场
4. 银行

## 数据库设计

### 大洲 continent

ID|备注
-|-
1|亚洲
2|欧洲
3|北美洲
4|南美洲
5|非洲
6|大洋洲

### 国家 country

字段|类型|备注
-|-|-
planet_id|int:10|星球id(预留字段)
continent_id|int:10|大洲id
short_name|string:255|名称
full_name|string:255|中文全称
name_en|string:255|英文全称
code|string:255|区域代码
state_system|tinyint:1|国家体制 

### 地理大区

ID|备注
-|-
1|华东
2|华北
3|华中
4|华南
5|西南
6|西北
7|东北

### 省/直辖市 province

字段|类型|备注
-|-|-
country_id|int:10|国家id
region_id|tinyint:10|地理大区
name|string:255|名称
code|string:255|区域代码
attr|string:255|简称
initial|char:1|大写首字母

### 市 city

字段|类型|备注
-|-|-
province_id|int:10|省id
name|string:255|名称
code|string:255|区域代码

### 县/镇/乡 county

字段|类型|备注
-|-|-
city_id|int:10|市id
name|string:255|名称
code|string:255|区域代码

### 街道/大队/村委会 street

字段|类型|备注
-|-|-
city_id|int:10|县/镇/乡id
name|string:255|名称
code|string:255|区域代码

