# 英语学习计划 - 前端工程师专属方案

## 问题诊断

```
当前状态                          目标状态
┌─────────────────┐              ┌─────────────────┐
│ ❌ 随机话题      │    ──────►   │ ✅ 结构化主题    │
│ ❌ 不预习不复习  │              │ ✅ 完整学习闭环  │
│ ❌ 错误重复犯    │              │ ✅ 错误追踪系统  │
│ ❌ 无workflow   │              │ ✅ AI辅助流程   │
└─────────────────┘              └─────────────────┘
```

---

## 教材精选（从你的资源中）

| 用途 | 教材 | 理由 |
|------|------|------|
| **发音核心** | American Accent Training | 美式发音圣经，系统矫正重音 |
| **发音补充** | Well Said | 针对重音、语调、连读 |
| **工作英语** | Business Partner | 职场场景对话 |
| **听力** | 21st Century Communication | 有tech相关内容 |
| **语法** | MyGrammarLab (Intermediate) | 系统修补语法 |

---

## 每周结构

```
周一 ─► iTalki课 (30min) + 复习 (30min)
周二 ─► iTalki课 (30min) + 发音练习 (30min)
周三 ─► iTalki课 (30min) + 听力练习 (30min)
周四 ─► iTalki课 (30min) + 语法练习 (30min)
周五 ─► 独立练习 (60min) - 周总结 + 录音分析
周六 ─► 独立练习 (60min) - 发音专项
周日 ─► 独立练习 (60min) - 预习下周材料
```

---

## AI 辅助录音分析 Workflow

在你的项目目录下创建这个工具：

```bash
mkdir -p ~/english-practice
cd ~/english-practice
```

### 核心脚本：`practice.sh`

```bash
#!/bin/bash

# 配置
PRACTICE_DIR="$HOME/english-practice"
DATE=$(date +%Y-%m-%d)
TIME=$(date +%H%M)

# 创建今日文件夹
mkdir -p "$PRACTICE_DIR/recordings/$DATE"
mkdir -p "$PRACTICE_DIR/analysis/$DATE"
mkdir -p "$PRACTICE_DIR/error-log"

# 录音文件
RECORDING="$PRACTICE_DIR/recordings/$DATE/${TIME}_practice.wav"
TRANSCRIPT="$PRACTICE_DIR/analysis/$DATE/${TIME}_transcript.txt"
ANALYSIS="$PRACTICE_DIR/analysis/$DATE/${TIME}_analysis.md"

echo "🎙️  开始录音练习..."
echo "📝 今日话题: $1"
echo "按 Ctrl+C 结束录音"
echo ""

# 录音 (macOS)
rec "$RECORDING" rate 16k channels 1

echo ""
echo "🔄 正在转写..."

# Whisper 转写
whisper "$RECORDING" --model medium --language en --output_format txt --output_dir "$PRACTICE_DIR/analysis/$DATE"

# 重命名转写文件
mv "$PRACTICE_DIR/analysis/$DATE/"*.txt "$TRANSCRIPT" 2>/dev/null

echo "✅ 转写完成: $TRANSCRIPT"
echo ""
echo "📊 准备AI分析..."

# 生成分析prompt
cat > /tmp/analysis_prompt.txt << 'EOF'
请分析以下英语口语练习的转写文本：

【转写内容】
$(cat "$TRANSCRIPT")

请提供以下分析：

## 1. 语法错误 (Grammar Errors)
列出所有语法错误，格式：
- 错误: "xxx" → 正确: "xxx" | 规则: xxx

## 2. 词汇问题 (Vocabulary Issues)
- 用词不当
- 更地道的表达建议

## 3. 句子结构 (Sentence Structure)
- 中式英语痕迹
- 改进建议

## 4. 总体评分 (1-10)
- 流利度:
- 准确度:
- 复杂度:

## 5. 本次重点复习 (3个最重要的错误)
请标记需要重点记忆的内容

## 6. 建议练习句 (5个)
基于错误生成练习句，供下次热身使用
EOF

echo "请将 $TRANSCRIPT 的内容发送给 Claude 进行分析"
echo "或运行: cat $TRANSCRIPT | claude"
```

### 错误追踪系统：`error-tracker.md`

```markdown
# 英语错误追踪日志

## 高频错误 (出现3次以上必须根治)

### 语法类
| 错误模式 | 正确形式 | 出现次数 | 状态 |
|----------|----------|----------|------|
| I have work... | I have been working... | 5 | 🔴 |
| He don't | He doesn't | 3 | 🟡 |

### 发音类
| 单词/短语 | 错误发音 | 正确发音 | 出现次数 | 状态 |
|-----------|----------|----------|----------|------|
| develop | de-VE-lop | di-VEL-əp | 4 | 🔴 |
| component | com-PO-nent | kəm-POH-nənt | 3 | 🟡 |

### 表达类
| 中式表达 | 地道表达 | 场景 |
|----------|----------|------|
| open the computer | turn on the computer | 日常 |
| I very like | I really like | 日常 |
```

---

## iTalki 课程最大化利用模板

### 课前准备 (周日 15分钟)

```markdown
# iTalki 周计划

## 本周主题: [例: Code Review 场景]

## 周一课程
- 目标场景: 解释我的代码改动
- 准备的句子 (5个):
  1. I refactored this function to improve readability.
  2. This PR addresses the performance issue we discussed.
  3. Could you take a look at line 45? I'm not sure about this approach.
  4. I think we should consider using a different data structure here.
  5. Let me walk you through the changes.

## 想要练习的语法点:
- 现在完成时 (I have implemented...)
- 虚拟语气 (If we were to use...)

## 上周错误复习 (从error-tracker.md提取):
- [ ] He don't → He doesn't
- [ ] I have work → I have been working
```

### 课中记录模板

```markdown
# iTalki 课程记录
日期: YYYY-MM-DD
老师: 
主题: 

## 老师纠正的错误 ⚠️
1. 我说: "xxx"
   应该: "xxx"
   
2. 我说: "xxx"
   应该: "xxx"

## 新学的表达 ✨
1. xxx - 意思/场景
2. xxx - 意思/场景

## 发音纠正 🎤
1. 单词: xxx
   我的发音: 
   正确发音:

## 下次课要刻意练习的点
1. 
2. 
```

### 课后复习 (当天 15分钟)

```bash
# 将课中错误添加到追踪系统
echo "| xxx | xxx | 1 | 🔴 |" >> ~/english-practice/error-log/grammar.md

# 录音练习纠正后的句子
./practice.sh "iTalki复习-纠正句练习"
```

---

## 每日练习模板

### 有iTalki课的日子 (30分钟独立练习)

```
时间分配:
├── 0-10min: 发音热身 (American Accent Training 1个章节)
├── 10-20min: 录音练习 (用准备好的句子)
└── 20-30min: 课后复习 (整理错误 + 复习录音)
```

### 无iTalki课的日子 (60分钟)

```
时间分配:
├── 0-15min: 发音练习 (American Accent Training)
├── 15-30min: 听力练习 (21st Century Communication)
├── 30-45min: 录音练习 + AI分析
└── 45-60min: 语法练习 (MyGrammarLab) 或 错误复习
```

---

## 技术英语专项 - 程序员场景

### 场景库 (轮流在iTalki练习)

```markdown
## Week 1-2: 日常开发
- [ ] 描述你正在做的功能
- [ ] 解释技术选型决策
- [ ] Code Review 讨论
- [ ] 描述一个 Bug

## Week 3-4: 会议场景
- [ ] Stand-up meeting 汇报
- [ ] Sprint planning 讨论需求
- [ ] Retrospective 反馈
- [ ] 技术方案讨论

## Week 5-6: 协作沟通
- [ ] 向非技术人员解释技术概念
- [ ] 请求帮助/澄清需求
- [ ] 给出技术建议
- [ ] 拒绝不合理的需求

## Week 7-8: 面试/职业
- [ ] 自我介绍
- [ ] 描述项目经验
- [ ] 系统设计讨论
- [ ] 薪资谈判
```

### 高频技术词汇发音练习

```markdown
每日5个，录音对比:

## React 相关
- component /kəmˈpoʊnənt/
- useState /juːz steɪt/
- props /prɑːps/
- render /ˈrendər/
- virtual /ˈvɜːrtʃuəl/

## 开发通用
- repository /rɪˈpɑːzɪtɔːri/
- architecture /ˈɑːrkɪtektʃər/
- asynchronous /eɪˈsɪŋkrənəs/
- cache /kæʃ/ (不是 /keɪʃ/)
- query /ˈkwɪri/
```

---

## 12周进度里程碑

```
Week 1-4:   建立习惯 + 发音基础
            ✓ 完成 AAT Chapter 1-4
            ✓ 建立错误追踪系统
            ✓ iTalki 课程结构化
            
Week 5-8:   语法修补 + 职场场景
            ✓ MyGrammarLab 完成时态部分
            ✓ 覆盖所有日常开发场景
            ✓ 高频错误减少50%
            
Week 9-12:  流利度提升 + 复杂表达
            ✓ 可以自如讨论技术方案
            ✓ 发音主要问题解决
            ✓ 建立长期维护习惯
```

---

## 立即行动清单

```bash
# 今天就做
□ 创建 ~/english-practice 目录结构
□ 安装 whisper: pip install openai-whisper
□ 安装录音工具: brew install sox
□ 创建 error-tracker.md
□ 告诉 iTalki 老师你要改变上课方式

# 本周日做
□ 准备下周 iTalki 4节课的主题和句子
□ 从 American Accent Training 开始第一章
□ 做一次完整的录音→转写→分析流程
```

---

需要我详细展开哪个部分？比如：
1. 具体的 Claude 分析 prompt 优化
2. American Accent Training 的使用方法
3. 针对特定技术场景的对话脚本

---

# iTalki 课堂设计指南（非技术背景老师）

## 核心策略

```
技术内容 ──► 抽象为通用沟通技能 ──► 老师可以帮助的部分

你负责: 技术准确性
老师负责: 语言准确性、发音、表达地道性
```

---

## 课堂类型设计

### 类型 1：解释类（Explaining）

**老师扮演：不懂技术的同事/客户/老板**

这正是真实场景——你经常需要向非技术人员解释技术概念。

```markdown
# 课前准备模板

## 今日场景: 向老板解释为什么项目延期

## 我准备的解释 (用简单类比):
"The current system is like an old house. We planned to just 
repaint the walls, but when we started, we found the pipes 
were broken. We need to fix the pipes first before painting."

## 我想练习的表达:
- "Let me put it this way..."
- "Think of it as..."
- "The short version is..."
- "What this means for you is..."

## 请老师帮我:
1. 纠正语法错误
2. 让表达更自然
3. 练习语调（解释时应该怎么停顿、强调）
```

**具体话题示例：**

| 技术话题 | 转化为通用话题 |
|----------|----------------|
| 解释为什么要重构代码 | 解释为什么要重新装修房子而不是修补 |
| 解释 Bug 产生的原因 | 解释为什么机器出了故障 |
| 解释技术债务 | 解释为什么需要先还"旧账"再做新事 |
| 解释 API 是什么 | 解释餐厅服务员如何在厨房和顾客之间传递信息 |

---

### 类型 2：会议场景（Meeting Simulation）

**老师扮演：会议参与者**

```markdown
# 课前准备模板

## 今日场景: 每日站会 (Daily Standup)

## 我要说的内容:
"Yesterday I worked on the user login page. I finished the 
basic layout but I'm still working on the validation part. 
Today I'll continue with that. I don't have any blockers 
right now, but I might need some help with testing later."

## 请老师:
1. 听我说完，记录语法错误
2. 告诉我哪些表达不自然
3. 我们角色扮演：你问我问题，我回答

## 可能的问题 (老师可以问):
- "When do you think you'll finish?"
- "Do you need any help?"
- "Can you explain what validation means?"
- "Is this blocking anyone else?"
```

---

### 类型 3：观点表达（Giving Opinions）

**老师扮演：有不同意见的同事**

```markdown
# 课前准备模板

## 今日场景: 我建议用新方法，但同事想用老方法

## 我的观点:
"I think we should try the new approach because it will 
save us time in the long run. The old method works, but 
it's harder to maintain."

## 我想练习的句型:
- "I see your point, but..."
- "Have you considered that..."
- "I understand the concern, however..."
- "What if we tried..."
- "I respectfully disagree because..."

## 请老师:
1. 反驳我的观点（用英语）
2. 我来回应
3. 纠正我在辩论中的语言错误
```

---

### 类型 4：发音专项（Pronunciation Focus）

**这是老师最能帮助的地方**

```markdown
# 课前准备模板

## 今日重点: 技术词汇发音

## 单词列表 (我先读，老师纠正):
1. component
2. architecture  
3. repository
4. asynchronous
5. parameter
6. variable
7. deployment
8. maintenance
9. authentication
10. configuration

## 句子练习 (包含以上单词):
1. "The component architecture needs to be refactored."
2. "I pushed the changes to the repository."
3. "This function handles asynchronous operations."

## 请老师:
1. 逐个纠正发音
2. 特别注意重音位置
3. 练习在句子中的自然发音
```

---

### 类型 5：情境对话（Situational Dialogues）

**老师扮演：各种角色**

```markdown
# 课前准备模板

## 今日场景: 请求帮助

## 背景 (告诉老师):
"I'm stuck on a problem at work. I need to ask a colleague 
for help. Please play my colleague. You're busy but friendly."

## 我会练习:
- 礼貌地打断别人
- 简洁地描述问题
- 接受或讨论建议
- 表达感谢

## 对话开始:
我: "Hey, do you have a minute? I'm running into an issue 
    and I think you might be able to help."
老师: (回应)
我: (继续)

## 请老师记录:
- 不自然的表达
- 语法错误
- 可以更礼貌/专业的地方
```

---

## 固定课堂结构（发给老师）

```
给老师的说明 (英文版):

Hi [Teacher's name],

I'd like to structure our classes to help me improve faster. 
Here's what I'm thinking:

CLASS STRUCTURE (30 minutes):
- First 5 min: I read/speak my prepared content
- Next 5 min: You point out errors and I take notes
- Next 15 min: Role-play / conversation practice
- Last 5 min: Summary of key corrections

MY GOALS:
1. Sound natural and professional
2. Fix grammar mistakes
3. Improve American pronunciation

WHAT I NEED FROM YOU:
- Please correct my errors immediately (don't let them pass)
- Focus on: grammar, word choice, pronunciation
- You don't need to understand the technical content
- Just help me express ideas clearly and naturally

I'll always prepare materials before class and send them 
to you 1 hour before we meet.

Thank you!
```

---

## 8 周话题轮换表

| 周次 | 话题类型 | 周一 | 周二 | 周三 | 周四 |
|------|----------|------|------|------|------|
| 1 | 日常沟通 | 自我介绍 | 描述工作 | 请求帮助 | 发音练习 |
| 2 | 会议场景 | 站会汇报 | 提出建议 | 回应问题 | 发音练习 |
| 3 | 解释说明 | 解释延期 | 解释问题 | 解释方案 | 发音练习 |
| 4 | 观点表达 | 同意/反对 | 给建议 | 委婉拒绝 | 发音练习 |
| 5 | 协作沟通 | 分配任务 | 确认理解 | 跟进进度 | 发音练习 |
| 6 | 问题处理 | 报告问题 | 道歉 | 提出方案 | 发音练习 |
| 7 | 职业发展 | 面试模拟 | 谈成就 | 谈目标 | 发音练习 |
| 8 | 复习周 | 复习错误 | 复习错误 | 复习错误 | 综合测试 |

---

## 具体话题脚本示例

### 示例 1：描述你正在做的工作

```markdown
# 课前准备

## 场景
同事问: "What are you working on these days?"

## 我的回答 (草稿):
"I'm currently working on improving the search feature of 
our website. Users have been complaining that search results 
are not accurate enough. So I'm trying to make the search 
smarter. It's like... you know when you search on Google and 
it somehow knows what you mean even if you make typos? I'm 
trying to do something similar but simpler."

## 我不确定的表达:
- "Users have been complaining" - 对吗？
- "make the search smarter" - 有更专业的说法吗？
- "you know when..." - 这样说自然吗？

## 请老师帮我:
1. 检查语法
2. 让描述更清晰
3. 练习自然的停顿和语调
```

### 示例 2：礼貌地拒绝

```markdown
# 课前准备

## 场景
老板想加新功能，但时间不够

## 我的回答 (草稿):
"I understand this feature is important. However, given our 
current timeline, I'm concerned we might not be able to 
deliver it with the quality we want. Could we perhaps 
include it in the next phase instead? That way we can do 
it properly."

## 我想学的表达:
- 委婉拒绝的句型
- 提出替代方案的说法
- 表达担忧但不消极

## 角色扮演:
老师扮演老板，坚持要加功能
我练习如何坚持立场但保持礼貌
```

### 示例 3：处理误解

```markdown
# 课前准备

## 场景
同事误解了我的意思

## 我的回答 (草稿):
"Oh, I think there might be a misunderstanding. What I meant 
was... Let me rephrase that. I wasn't saying we should cancel 
the project. I was suggesting we should adjust the scope. 
Does that make more sense?"

## 关键表达:
- "I think there might be a misunderstanding"
- "What I meant was..."
- "Let me rephrase that"
- "I wasn't saying X, I was saying Y"
- "Does that make sense?"

## 请老师:
模拟误解我的话，让我练习澄清
```

---

## 简化版课前模板

每节课前填写这个，发给老师：

```markdown
# iTalki Class Prep
Date: ___________
Topic: ___________

## What I'll practice today (1-2 paragraphs):
[写下你要说的内容]

## Expressions I want to use:
1. 
2. 
3. 

## Questions for you:
- Is this natural: "___________"?
- How do I pronounce: ___________?

## Role-play scenario:
You are: [角色]
Situation: [情境]

## Last class errors to review:
1. 
2. 
```

---

这样设计后，老师不需要懂技术，只需要：
- 纠正你的语言
- 扮演对话角色
- 帮你改善发音

需要我帮你写出更多具体场景的对话脚本吗？