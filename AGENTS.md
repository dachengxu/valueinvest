# AGENTS（本分支定制版）

本分支 `docs/valuation-algorithms` 只维护两个文件：

- `valuation_algorithms.md` —— 估值方法论文档
- `AGENTS.md` —— 本说明

`main` 分支保留给上游仓库（github.com/wangzhe3224/valueinvest）定时同步，**不要在 main 上提交这两个文件**，以免与上游同步产生冲突。

## 当前工作区状态

本分支是孤立分支（orphan，与 main 无共同历史）。2026-10-15 已清理工作区：仓库其余文件均已移除，当前目录只有上面两个文件。若之后从 main 恢复过上游文件，它们在本分支上会重新变为未跟踪状态。

## 分支切换

切回 main（用于同步上游）：

```
git checkout main
```

- 工作区干净（只有两个已跟踪文件）时，普通切换即可；
- 若存在未跟踪的上游文件，改用 `git checkout -f main`（未跟踪文件与 main 内容一致，不会丢改动）；
- 在本分支有未提交的文档修改时，先提交再切换。

## 核验文档时如何取库源码

本分支工作区没有库代码，核对公式/阈值前先取回（二选一）：

```
git checkout main                          # 直接切换，用完 git checkout docs/valuation-algorithms 切回
git worktree add ../valueinvest-src main   # 或另开工作区，互不干扰
```

`valueinvest/reports/` 曾被 .gitignore 忽略，如缺失可用 `git checkout origin/main -- valueinvest/reports/` 恢复。

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
