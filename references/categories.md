# Auto-Categorization Rules

Maps merchant/product keywords to iCost category names.
Rules are applied in order; first match wins.

## Transaction Type Overrides (check tx_type first)

| tx_type contains | Type    | Category | Sub-category |
|-----------------|---------|----------|--------------|
| 退款             | 收入    | 其他      | 退款          |
| 红包             | 收入    | 其他      | 红包          |
| 亲属卡           | 支出    | 其他      | 亲属卡        |
| 零钱充值          | 转账    | 其他      | 零钱充值       |
| 零钱提现          | 转账    | 其他      | 零钱提现       |
| 转账             | 支出    | 转账      | 个人转账       |

## Keyword → Category Mapping

| Keywords (merchant + product)                                         | 一级分类 | 二级分类    |
|----------------------------------------------------------------------|---------|-----------|
| 餐, 饭, 面, 烤, 火锅, 奶茶, 咖啡, 茶饮, luckin, 麦当劳, 肯德基, 包子, 粥, 饺, 牛肉, 鱼, 西餐, 汤包, 豆花, 米线, 烧烤, 串, 食堂 | 餐饮 | 三餐 |
| 盒马, 超市, 便利店, 名创, 京东, 拼多多, 淘宝, 天猫                          | 购物 | 网购/超市  |
| 骑行, 运动, 健身, 跑步, 马拉松, 游泳, 球, 羽毛球, 钓鱼                       | 运动 | 运动健身   |
| 滴滴, 出行, 地铁, 公交, 高铁, 机票, 加油, 停车, 充电桩                       | 交通 | 出行      |
| 电费, 供电, 电网, 燃气, 水费                                              | 居家 | 水电燃气   |
| 物业                                                                   | 居家 | 物业      |
| 保险                                                                   | 金融 | 保险      |
| 健康平台, 医院, 药店, 诊所                                                | 医疗 | 医疗健康   |
| 动物园, 探险, 宝宝巴士, 游乐, 摇摇车, 亲子                                  | 娱乐 | 亲子娱乐   |
| 美发, 理发, 美容, 美甲, 优剪                                              | 个护 | 美发美容   |
| 顺丰, 快递, 邮政, 圆通, 中通, 韵达                                         | 购物 | 快递      |
| 腾讯云, 阿里云, 服务器, 域名, cdn                                          | 数码 | 云服务    |
| 教育, 学习, 培训, 课程, 书店                                              | 教育 | 教育培训   |
| 话费, 流量, 移动, 联通, 电信                                              | 通讯 | 话费流量   |

## Default

If no keyword matches → `其他 / 待分类`

## Usage Note

These are suggested defaults. The user's actual iCost category names may differ.
When in doubt, use a broad category like `购物` or `其他` rather than a specific one that may not exist.
