# AGENTS（本分支定制版）

本分支 `docs/valuation-algorithms` 只维护 `valuation_algorithms.md`（估值方法论文档）这一份文件。`main` 分支保留给上游仓库（github.com/wangzhe3224/valueinvest）定时同步，**不要在 main 上提交本文档**，以免与上游同步产生冲突。

## 分支切换注意

本分支是孤立分支（orphan，与 main 无共同历史），仓库其余文件在本分支上处于**未跟踪**状态。切回 main 需要强制切换：

```
git checkout -f main
```

未跟踪文件与 main 内容一致，强制切换不会丢失改动；如在本分支上有未提交的文档修改，先提交再切换。日常在 main 同步上游（`git pull`）不受影响。

## 修改 valuation_algorithms.md 之前

1. 查看文档开头「版本说明」登记的库版本与核验日期。
2. 对照该版本源码逐项核验要改动的公式、常数、默认值与阈值，至少覆盖：
   - `valueinvest/valuation/`（24 个方法）
   - `valueinvest/cyclical/valuation/`（4 个周期方法，需 `CyclicalStock` 输入）
   - `valueinvest/valuation/base.py` 与 `valueinvest/cyclical/valuation/base.py`（±15% / A股±20% 等评估阈值）
3. 写进文档的每个数字都必须能在源码中找到出处，不允许凭记忆编写阈值。
4. 改完后更新「版本说明」中的版本号与核验日期，并保持附录 A 的方法对照表同步。

## 文档约定

- **自包含**：不依赖本库的任何类或 API，读者用公开财报数据即可复算；附录 A 仅是库方法名到章节的对照，供本项目用户使用。
- 每个方法固定七段式：一句话定义 / 公式 / 输入变量表 / 计算步骤 / 关键假设 / 适用范围 / 局限与注意事项。
- 明确区分「产出公允价值的方法」与「风险/质量筛选方法」，后者不得写成估值。
- 文档为中文；公式使用代码块；项目内部约定（如 ±15% 阈值）需注明是项目约定而非方法论本身。
