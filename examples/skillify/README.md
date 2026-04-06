# Skillify 示例项目

这是一个真实案例的公开整理版，用来说明这套模板在实际项目中会如何落地。

## 这个示例适合拿来看什么

- 看一个项目级 `AGENTS` 和 `WORKFLOW` 会写成什么样
- 看 PRD、UI 文档、技术文档如何组成长期基线
- 看“首页转化 -> 登录 -> 补全联系方式 -> 选购 -> 支付 -> 订单”这类完整链路，如何被文档化

## 这个示例不建议直接照抄什么

- Skillify 的产品定位
- Skillify 的页面清单
- Skillify 的业务术语
- Skillify 的交付方式

这些内容属于这个项目本身，不是通用模板。

## 推荐阅读顺序

1. [AGENTS.md](AGENTS.md)
2. [WORKFLOW.md](WORKFLOW.md)
3. [docs/README.md](docs/README.md)
4. [docs/01-product-requirements.md](docs/01-product-requirements.md)
5. [docs/02-ui-design-spec.md](docs/02-ui-design-spec.md)
6. [docs/03-technical-architecture.md](docs/03-technical-architecture.md)

## 通用和专属怎么区分

- 通用思路：
  - 双目录基线快照
  - 文档先行
  - 主代理编排、子代理执行
  - 里程碑前回看基线文档
- Skillify 专属：
  - 面向中国个人创作者的 AI 智能体技能定制服务
  - 手机号和邮箱双联系方式补全
  - 方案选购页常驻 AI 顾问区
  - mock 支付与订单回看链路
