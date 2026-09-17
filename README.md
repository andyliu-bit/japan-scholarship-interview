# japan-scholarship-interview

面向**日本大学院（修士・博士）研究型奖学金**的日语面试准备 skill。

核心思路：面试崩掉的最大原因通常不是能力不足，而是"能说的事实"与"不能说的事实"边界模糊就上场。因此全部工作从**事实台账**开始，也以与台账的核对结束。

## 适用 / 不适用

**适用**
- 面试语言为日语的研究型奖学金（含研究计划的发表与质疑）
- 大学内部、民间财团、政府系均可

**不适用**
- 不含研究计划的学部生・语言学校生奖学金面试（那类面试问的是家计、来日理由、生活规划，本 skill 的结构会跑偏）
- 入学考试本身的对策
- **英语面试的表达层**：事实控制・研究叙事・问答体系・时长三级制・核验**照常适用**；
  不覆盖的是日语特有的表达规范、危险词的日语词表、日语的字数速率基准。详见 SKILL.md「适用范围」

## 安装

本仓库的根目录就是 skill 本体（`SKILL.md` 在根）。**目录名需保持 `japan-scholarship-interview`。**

Claude Code：

```bash
git clone https://github.com/andyliu-bit/japan-scholarship-interview.git ~/.claude/skills/japan-scholarship-interview
```

Codex：

```bash
git clone https://github.com/andyliu-bit/japan-scholarship-interview.git ~/.agents/skills/japan-scholarship-interview
```

### 或者作为 plugin 安装

```
/plugin marketplace add andyliu-bit/japan-scholarship-interview
/plugin install japan-scholarship-interview@andyliu-skills
```

本仓库同时是一个 plugin marketplace。根目录的 `SKILL.md` 会被作为单个 skill 加载（仓库没有 `skills/` 目录，这是该布局生效的前提）。

skill 主体是纯 Markdown、相对路径、无外部依赖、无 OS 特定命令，**兼容支持 Agent Skills / `SKILL.md` 约定的运行时**；各运行时额外需要的清单文件（如 Codex 的 `agents/*.yaml`）按需自行添加，本仓库不预置。

## 使用

自然语言提出即可（"帮我准备奖学金面试""出一份想定问答"）。也可指定模式：

| 模式 | 用途 |
|---|---|
| `--full` | 完整流程 |
| `--script` | 只写发表原稿 |
| `--qa` | 只出想定问答 |
| `--mock` | 只跑模拟面试并评分 |
| `--check` | 只做原稿／幻灯片／问答／申请书的一致性核验 |

## 更新与反馈

**plugin 安装的**：`/plugin update japan-scholarship-interview`。
更新只在 `.claude-plugin/plugin.json` 的 `version` 变化时才会推送，所以内容没变时不会有更新提示。

**直接 clone 的**：到该目录 `git pull`。

**发现规则有问题**：欢迎开 [issue](https://github.com/andyliu-bit/japan-scholarship-interview/issues)。
特别欢迎「规则把正确的做法判成了违规」这类反馈——开发过程中这类错误出现过不止一次，
而且只有真实使用才会暴露（见 `tests/runs/README.md` 的教训一节）。

## 目录

```text
SKILL.md                        总控：画像判定、模式、流程、边界、输出权限
references/
  fact-control.md               画像・信息收集・主张台账・评审视点分析
  narrative-and-qa.md           研究叙事（理工／人文社科分支）・五级问答体系
  japanese-expression.md        日语表达规范（横切：产出日语文本前必读）
  deliverables.md               发表原稿・幻灯片・时长三级制・委派契约
  rehearsal-and-audit.md        模拟面试・两遍核验・当天应对・失败模式
assets/                         可填模板（会被复制进用户产物）
tests/fixtures/                 虚构人物 ×3（仅测试用，真实任务不得加载）
tests/runs/                     运行记录 ×7 ＋ 索引
.claude-plugin/                 plugin 与 marketplace 清单
```

产物写入用户工作目录下的 `./interview-prep/`。

## 许可证

MIT。可自由使用、修改、再分发，保留版权声明即可。详见 [LICENSE](LICENSE)。

## 隐私

- **写盘前检查目标目录是否受版本管理、是否可能公开**（存在 `.git`、公开仓库、同步盘）。可能公开时先提示改用私有目录。
- factsheet **不记录证件号码、住址、证件与成绩单扫描件、银行信息**。
- 不把个人信息写入本 skill 目录，不发送到外部服务。
- **不自动修改 `.gitignore`**，除非用户授权。

## 边界

- 不编造不存在的业绩、经历、数值。不确定处保留 `【要確認】`，交付时统一列出。
- **不给出合格概率的数字。** 准备度、风险项、相对强弱的判断可以给。
- 面向学校・财团的联络与提交**只做到草稿为止**，发送与提交由本人决定。
- 幻灯片渲染、假名注音：环境中有专用技能则委派，否则按最小规格自理。**未确认渲染／未确认读音，不宣称完成。**

## 测试

三个虚构夹具，分工覆盖不同分支。各自末尾定义回归检查点，并列出**本夹具无法覆盖**的规则。

| 夹具 | 覆盖的分支 | 检查点 |
|---|---|---|
| `fictional-persona.md` | 理工・博士 3 年・线下发表 7 分・汉字圈重点词注音 | 16 |
| `fictional-persona-humanities.md` | 人文社科・修士 2 年・线上纯质疑・非汉字圈全假名・L4 的 max 分支 | 13 |
| `fictional-persona-english.md` | 英语场次——验证"不覆盖英语表达规范"到底不覆盖什么 | 9 |

运行记录在 `tests/runs/` 下。**先看 [`tests/runs/README.md`](tests/runs/README.md)**——它汇总了 7 次运行、34 个已修复问题，以及仍未覆盖的分支。

**该夹具仅供测试。真实任务中不得加载，不得引用其内容作为用户事实。**

## 已知限制（V1）

- 表达层只覆盖日语；英语场次的**表达质量**本 skill 不负责（其余环节照常适用）。
- 时长的最终验收依赖**本人真实朗读**，skill 只能给字数预算与结构预算。
- 核验分两遍：机械检查可自动跑，**语义审阅必须逐段人工或模型完成**，无法全自动。
- **回归检查点由模型执行流程后逐项判定，不是自动化测试。** 判定结果是人可复核的记录，不构成自动化保证；其中写盘变体的关键判定有命令输出作为客观依据。
- **尚未验证的分支**：委派给外部技能后的实际验收、连续验收失败转降级。详见 [`tests/runs/README.md`](tests/runs/README.md)。
- **全假名／罗马字**已实际转写验证；但**转写的读音正确性没有日语母语者复核**，真实使用时必须逐词向本人确认。
- **时长**：目前只验过字数预算侧，**没有本人朗读实测的记录**。真实通过标准仍是朗读。
- 公开仓库从单个提交开始，不含开发历史。开发历史保留在作者的私有仓库。详见 [`tests/runs/README.md`](tests/runs/README.md)「关于仓库历史」。
