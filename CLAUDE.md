# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains AI BBS Sessions - a collection of 6 interactive learning agents designed to be copy-pasted into ChatGPT, Claude, or other LLMs to execute as BBS-style educational experiences. Each session is a self-contained 15-minute learning module focused on AI prompt engineering mastery.

## Architecture

### Core Structure
- **Session Files** (root): Six main learning modules (`session-1-*.md` through `session-6-*.md`)
  - Each session is a complete BBS-style terminal interface agent
  - Sessions progress from basic to advanced AI interaction techniques
  - Stateful interface with menus, progress tracking, and assessments

- **Dev Documentation** (`dev-docs/`): Development materials and facilitator guides
  - Seed files for session creation
  - Facilitator documentation and feedback systems
  - Learning framework specifications

### Session Topics
1. **Prompting Mastery**: Zero-shot prompting fundamentals
2. **Contextual Direction**: Role-based and few-shot prompting
3. **Strategic Reasoning**: Multi-step thinking and problem decomposition
4. **Orchestrated Workflow**: Complex multi-agent coordination
5. **Adaptive Partnership**: Dynamic AI collaboration patterns
6. **Warm Orchestration**: Human-AI synergy and advanced techniques

### Agent Design Pattern
Each session follows a consistent BBS-terminal interface pattern:
- Menu-driven navigation (`1-9`, `b`, `m`, `?`, `q`)
- Status bar with progress tracking and timing
- Exercise-based learning with feedback loops
- Assessment and scoring systems
- Export functionality for session summaries

## Development Guidelines

### File Structure
- Session files are standalone agents - no dependencies between files
- Each session is complete and can be used independently
- Dev-docs contain implementation details but aren't part of the user experience

### Content Standards
- BBS-style ASCII interfaces with consistent formatting
- 15-minute target duration for each session
- Progressive difficulty across the 6-session curriculum
- Interactive exercises with dynamic feedback

### Session Creation/Modification
When working with session files:
- Maintain the BBS terminal aesthetic and navigation patterns
- Preserve the stateful progress tracking system
- Keep timing constraints realistic (15-minute sessions)
- Ensure exercises provide concrete, actionable learning

## Usage Context
These agents are designed to be deployed by copying session content into LLM interfaces, not as executable code. The repository serves as source material for educational AI interaction training.