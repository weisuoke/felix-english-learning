# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an **English learning system** (not a software project) designed for a frontend engineer (React/Next.js specialist) who needs to improve work-related English communication. The repository contains structured documentation, templates, and learning materials.

**Target English Level:** A2-B1 → B2 (work-ready communication)
**Focus Areas:** Technical discussions, meetings, code reviews, pronunciation, listening

**Weak Points Being Addressed:**
- Listening (primary focus) - very poor listening
- Pronunciation (stress patterns)
- Grammar

## Repository Structure

```
research/                    # Research docs
  ├── 20260127-gpt-research.md      # GPT-generated study plan research
  └── 20260127-opus45-research.md   # Opus-generated detailed class design

approach/                    # Learning approach
  └── listening-hell-plan.md        # Listening Sunflower Manual (4-week breakthrough plan)

italki-class/                # iTalki class materials
  ├── italki-class-structure.md      # 30-minute class structure guide
  ├── pronunciation-practice-plan.md # 2-week pronunciation practice kick-off plan
  └── tech-vocabulary-100-groups.md  # 1000+ technical terms (with IPA phonetics)

current_status.md            # Background, goals, resource list
```

## Core Methodology

The system follows **"Target Priority + Deliberate Practice + Closed-Loop Review"**:

1. **Error-Driven Learning** - Systematic tracking prevents repeated mistakes (🔴→🟡→🟢)
2. **Scenario-Based Training** - Role-playing work situations with non-technical tutors
3. **Teacher-Agnostic Design** - Technical concepts abstracted to simple analogies
4. **AI-Augmented Workflow** - Whisper (transcription) → Claude (analysis) → Error Database

## Key Structures

### iTalki 30-Minute Class Structure
```
0-3 min    Review last class's errors
3-15 min   Work-scenario role-play (core)
15-20 min  Error consolidation (Top 5)
20-25 min  Prep for next class
25-30 min  Pronunciation practice (10 words)
```

### Daily Listening Training (30 min) - Listening Sunflower Manual
```
0-5 min    Warm-up: review yesterday's "blacklist words"
5-20 min   Core: dictation training (hell itself)
20-28 min  Reinforce: shadowing (repeat after the audio)
28-30 min  Log: update the blacklist
```

### 8-Week Scene Rotation (iTalki)
1. Daily Standup → 2. Bug Explanation → 3. Requirement Clarification → 4. Code Review → 5. Asking for Help → 6. Explaining Delay → 7. Disagreeing Politely → 8. Comprehensive Review

### Error Tracking System
Status indicators: 🔴 new → 🟡 practicing → 🟢 mastered
- 3 consecutive days of correctly hearing/producing it → 🔴 promoted to 🟡
- Stable for 1 consecutive week → 🟡 promoted to 🟢

## Training Plans

### Listening (Listening Sunflower Manual)
- **Week 1-2**: Dictation hell phase - aggressively identify every word you "can't catch"
- **Week 3-4**: Speed-variation breakthrough phase - 1.25x → 1.5x speed change + shadowing
- **Materials**: National Geographic Listening and Notetaking → technical podcasts (Syntax.fm, Fireship)

### Pronunciation
- **Materials**: American Accent Training, Well Said
- **Focus**: stress placement, linking, reductions

### Speaking
- **Method**: iTalki role-play + recording analysis
- **Materials**: Business Partner, Market Leader

## Tools

```bash
# Speech-to-text transcription
pip install openai-whisper

# Audio recording
brew install sox

# Audio playback with speed control
brew install iina  # or VLC
```

## Working with This Repository

When assisting with this project:
- **Maintain the systematic methodology** - error tracking and closed-loop review are central
- **Preserve work-focused context** - all scenarios target frontend engineer communication
- **Keep teacher-agnostic design** - materials should work with non-technical tutors
- **Support the "blacklist" system** - track problematic words/phrases for repeated drilling
- **Technical vocabulary** in `tech-vocabulary-100-groups.md` includes IPA phonetics for 1000+ terms
