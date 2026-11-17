# 核心数据

状态：最小字段设计建议，尚未建库。更新：2026-11-17。
需求、配送规则及待确认事项见[需求与页面设计](requirements.md)。金额建议使用整数“分”；时间由云端生成，营业时间按 Asia/Shanghai 解释。

| 数据 | 建议字段 | 说明 |
| --- | --- | --- |
| 用户身份 | id、微信身份标识、role | 学生 / 经营者；角色由可信云端配置，初始经营者授予方式待实现时确定 |
| 商品 | id、name、description、priceFen、isOnSale、createdAt、updatedAt | 图片可选；不引入复杂库存 |
| 订单 | id、studentId、phone、remark、items、quantityTotal、goodsAmountFen、deliveryFeeFen、totalAmountFen、deliveryDate、deliveryLocation、deliveryWindow、status、createdAt、requestId | 手机号必填，备注可选；配送信息保存快照 |
| 订单商品项 | productId、nameSnapshot、unitPriceFen、quantity、subtotalFen | 嵌入订单保存；商品后续修改不改变历史值 |

## 数据约束建议

- 数量为正整数，订单至少包含一个商品；提交时检查商品仍在售。
- 云端从可信身份取得 studentId，从商品记录读取价格并计算金额，不采用客户端提交的价格或总价。
- goodsAmountFen 为商品项小计之和；totalAmountFen 为商品金额与配送费之和。
- deliveryLocation 保存订单提交时适用的配送地点快照。最终是一处固定地点还是两个可选地点尚待确认，页面与数据实现均不得提前假定。
- 单份配送费及多份免配送费规则待确认；不写死为 1 元或 2 元，也不默认为免费。测试时使用明确标注的配置值。
- V1 订单业务状态仅需“已提交”；不引入待支付→已支付状态流。未接支付不等于已付款；未来支付状态与订单业务状态分开设计。
- 建议以用户身份与 requestId 唯一约束防止同次提交重试生成重复订单；确认创建后返回相同订单结果。
- 商品写入限经营者；订单创建与金额写入经云函数；订单读取按本人 / 经营者权限限定。手机号不得放入公开商品响应。
