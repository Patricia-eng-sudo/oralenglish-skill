# TEM-4 口语思辨陪练（tem4-debate-coach）

面向英语专业四级（TEM-4）口试备考的**纯对话式口语思辨陪练 Skill**。由 AI Agent 加载后，以"出题→作答→反馈"的循环陪用户练口语思辨，无需任何脚本、网页或图形界面，全程只在对话中完成。

## 1. 项目解决什么问题

英语专业四级口试要求考生对给定话题快速、有条理、地道地表达个人观点。备考中普遍存在三个痛点：

- **没有陪练对象与话题**：想练思辨却找不到合适的英文话题，也没有人逐句反馈
- **中式英语根深蒂固**：中文直译语序、中式搭配、逻辑断层、母语负迁移无人指正，练再多也难长进
- **只练不评、进步慢**：口语输出后缺少针对性的句法与用词反馈，不知道问题在哪、怎么改

本项目针对以上痛点，提供一个**随时可用的对话式思辨陪练**：AI 出英文思辨话题和参考句型，用户口头作答，AI 逐句转写、改写优化并点评，通过【继续】/【重新回答】在同一话题下循环深化，帮用户积累地道表达、修正中式英语、提升口语流畅度与逻辑性。

## 2. 主要功能

- **英文思辨话题 + 一正一反参考句型**：每轮给出一个适配专四口语、可辩论的英文 Topic，附一句肯定立场、一句否定立场的纯英文参考句型（句式支架，非标准答案），启发用户组织自己的观点
- **①【我的原句】**：原样转写用户口述英文，保留原始表达与错误
- **②【优化句】**：仅 1 版适配专四口语的改写，优先修正中式英语（中文直译语序、中式搭配、逻辑断层、母语负迁移），拒绝浅层同义词替换，核心改动加粗，口语化、不过度书面
- **③【简短点评】**：点明本次最突出的中式英语问题，并分别说明逻辑、句式、用词地道度情况
- **【继续】/【重新回答】循环**：输入【继续】进入同话题深度追问（附新的参考句型）；输入【重新回答】不换题重答，循环反馈直至【继续】

**暂不支持**：网页抓取、PDF、图形界面。

## 3. 安装方法

本 Skill 是**纯文件夹形式**，无需编译、无需依赖、无构建步骤。将 `tem4-debate-coach/` 文件夹放入支持 Skill 的 AI Agent 的技能目录即可：

```text
# 例如放在工作区用户技能目录
workspace/.user_skills/tem4-debate-coach/

# 或放入项目的 skills/ 目录（按你的 Agent 约定）
你的项目根/skills/tem4-debate-coach/
```

- 目标目录下应包含：`SKILL.md`、`agents/openai.yaml`（见下方目录结构），复制整个文件夹即可
- 安装后无额外配置；Agent 首次加载即通过 `SKILL.md` 与 `agents/openai.yaml` 识别该技能
- （仅开发校验可选）如需运行官方校验器 `quick_validate.py`，需 Python 环境并安装 `PyYAML`：`python -m pip install pyyaml`

### 目录结构

```
新建文件夹/
├── README.md                  # 本文件
└── tem4-debate-coach/         # 可开源 Skill
    ├── SKILL.md               # 技能指令与流程规则
    └── agents/
        └── openai.yaml        # OpenAI Agents SDK 技能声明（instructions 指向 SKILL.md）
```

## 4. 使用方法

1. 安装：将 `tem4-debate-coach/` 放入 Agent 技能目录（见上文）
2. 开启：对 Agent 说"开始专四口语思辨陪练"或"练一个口语话题"
3. 作答：收到 Topic 与参考句型后，口头作答（打字或语音输入均可）
4. 推进：收到 ①②③ 反馈后
   - 输入【继续】→ 进入同话题深度追问（新一轮 Topic + 参考句型）
   - 输入【重新回答】→ 不换题，重新作答，AI 再次给出 ①②③（可反复，直至【继续】）

## 5. 输入输出示例

**用户**：开始专四口语思辨陪练

**AI（出题）**：

```
**Topic:** Do you think social media does more harm than good to young people?

**Agree（肯定立场参考句型）:** From my perspective, social media does more harm than good because it constantly distracts young people from their studies and real-life relationships.

**Disagree（否定立场参考句型）:** I would argue that social media brings more benefits than harm because it helps young people connect with the world and access information instantly.
```

**用户（口述/输入）**：I think social media is good for young people, because it can make we learn many new things. And if we have problem, we can search from internet, very convenient.

**AI（反馈）**：

```
①【我的原句】
I think social media is good for young people, because it can make we learn many new things. And if we have problem, we can search from internet, very convenient.

②【优化句】
I think social media is good for young people because it **helps us learn** many new things. **For example, when we run into a problem, we can look it up online** — **that's really convenient.**

③【简短点评】
本次最典型的中式英语：① "make we learn" 是母语负迁移——误用 make 使役结构且代词用了主格（应为 help us learn）；② "search from internet" 是中文"从网上搜"的直译搭配，英文地道说法是 look it up online，且 internet 前需冠词。逻辑上你给出"学新知＋方便"两个理由，但中间缺衔接；句式偏短句罗列，合并后更连贯；用词能达意，整体自然度中等。

【继续】  【重新回答】
```

**用户**：重新回答 → 再次作答 → AI 再次输出 ①②③（循环直至【继续】）
**用户**：继续 → AI 输出同话题深度追问（附一正一反参考句型）→ 新一轮作答

## 校验

已通过官方校验器验证：

```
python scripts/quick_validate.py tem4-debate-coach
→ Skill is valid!
```
