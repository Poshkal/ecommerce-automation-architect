---
name: ecommerce-automation-architect
description: "设计欢迎、弃单、物流通知或报表自动化，排查重复发送、同意丢失和恢复问题时使用"
---

# 跨境电商自动化架构

## When to use

设计欢迎、弃单、物流通知或报表自动化，排查重复发送、同意丢失和恢复问题时使用。

## Preconditions

确认输入、当前版本、可用工具及本次授权范围。历史案例只作方法依据，不能替代当前验证。缺少关键输入时先做可独立完成的只读检查，再列阻塞。

## Procedure

1. 确认事件源、目标系统、消息目的、允许测试范围、同意与退订事实来源。
2. 绘制触发→过滤→幂等→发送→回执→审计链路，明确字段映射、TTL与最小数据。
3. 定义重复事件、超时、429、永久拒绝、撤回同意及死信处理；回执不明先查询而非再次发送。
4. 以合成事件本地回放，并在授权隔离环境验证同意字段从购物车到弃单事件持续可读；设计不等于持久化成功。
5. 只有同意、抑制名单、幂等、回执与监控验证通过且用户授权启用后才能激活；否则交付草案。

## Tool permissions

本地设计、合成回放和授权只读配置检查；正式启用、发送或连接新账号另需授权。

## Failure handling

同意不明/事件字段丢失/权限不足时BLOCKED并禁用发送路径；保留失败事件脱敏摘要。

## Deliverables

按下方输出契约交付本技能步骤中要求的清单、草稿/方案及证据；未执行项单列。

## Acceptance criteria

同意未预勾选、退订生效、重复事件不重复发送、故障可恢复均有证据；未接通平台不得PASS端到端。

## Hard boundaries

不泄露密钥、客户隐私或非公开商业资料，不覆盖用户已有工作。读取权限不等于外发权限；生产变更按用户明确授权执行。

## Response contract

输出 `STATUS`、`SCOPE`、`EVIDENCE`、`CHANGES`、`TESTS RUN`、`OPEN RISKS`、`NEXT HUMAN ACTION`。逐项区分 PASS / NEED FIX / BLOCKED / NOT VERIFIED；历史记录、mock、本次本地与平台实测分列。

## Evidence and examples

阅读 [历史案例](references/cases.md) 时只加载与任务相关的案例；证据索引见其中链接。
