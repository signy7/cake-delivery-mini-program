# cake-delivery-mini-program

为单人开发的校园定点配送微信小程序。学生与经营者共用一套应用，后端采用微信云开发。

## 当前阶段

当前为 V1：先完成商品浏览、商品管理、订单确认与订单管理，暂不接入支付。业务代码尚未实现，验收尚未执行。

核心流程：经营者维护商品 → 学生浏览并确认订单 → 云端保存 → 经营者查看订单。提交订单不代表付款成功。

## 文档入口

| 文档 | 内容 |
| --- | --- |
| [需求与页面设计](docs/requirements.md) | 业务、用户、功能与质量需求；页面职责、V1 范围、验收及待确认事项 |
| [架构与模块边界](docs/architecture.md) | 小程序、云函数、数据库及身份 / 商品 / 订单职责 |
| [核心数据](docs/data.md) | 用户、商品、订单快照与数据约束 |

## 维护约定

- [需求与页面设计](docs/requirements.md)定义产品行为和 V1 验收；架构文档划分职责；数据文档约束存储。
- 以明确确认的需求为基线；设计建议、待定事项、已实现及已验证状态分别标明。
- 需求或代码变化时同步更新相关文档；未执行的验收不标为通过。
- 不为文档完整性增加支付、复杂库存、路线、批次等范围外功能。

组织方式参考 [Human Worth README](https://github.com/KDZZZZZZ/human-worth/blob/dev/README.md)、[产品文档](https://github.com/KDZZZZZZ/human-worth/blob/dev/docs/prd.md)与[架构文档](https://github.com/KDZZZZZZ/human-worth/blob/dev/docs/backend-architecture.md)：保留集中索引、需求与方案区分、模块和数据归属，以及实现状态说明；不复用其微服务和复杂部署体系。
