# Agent Orchestration System - Simple & Powerful

## 🎯 System Overview

This is a SIMPLE orchestration system with specialized agents that work together:

1. **`orchestrator`** - Manages the big picture, creates todo lists, delegates tasks
2. **`coder`** - Implements specific coding tasks
3. **`tester`** - Visually tests implementations using Playwright MCP
4. **`stuck`** - MANDATORY human escalation for ANY problems (NO FALLBACKS!)

## 🚨 CRITICAL SYSTEM RULE: NO FALLBACKS

**HARDWIRED INTO EVERY AGENT:**

When ANY agent encounters ANY problem, error, uncertainty, or failure:
- ❌ **NEVER** use fallbacks
- ❌ **NEVER** use workarounds
- ❌ **NEVER** make assumptions
- ❌ **NEVER** skip errors
- ✅ **ALWAYS** invoke the `stuck` agent immediately
- ✅ **ALWAYS** get human input before proceeding

**This is NON-NEGOTIABLE. The `stuck` agent is the ONLY path forward when problems occur.**

## 📋 How the System Works

### Step 1: Orchestrator Takes Control

When you (the main Claude instance) receive a project:

1. **IMMEDIATELY** invoke the `orchestrator` agent using the Task tool
2. Pass the complete project requirements to the orchestrator
3. The orchestrator will:
   - Analyze the full project scope
   - Create a detailed todo list using TodoWrite
   - Begin delegating tasks to specialized agents

### Step 2: Orchestrator Delegates to Coder

For each todo item requiring implementation:

1. Orchestrator invokes the `coder` agent with specific task
2. Coder implements the feature/functionality
3. If coder hits ANY problem → invokes `stuck` agent
4. Coder reports completion back to orchestrator

### Step 3: Orchestrator Delegates to Tester

After each implementation:

1. Orchestrator invokes the `tester` agent
2. Tester uses **Playwright MCP** to:
   - Navigate to the application
   - Take screenshots of rendered output
   - Verify visual correctness
   - Test interactions
   - Validate functionality
3. If tester finds ANY problem → invokes `stuck` agent
4. Tester reports results back to orchestrator

### Step 4: Stuck Agent Handles Problems

When invoked by any agent:

1. `stuck` agent receives the problem report
2. Gathers additional context if needed
3. Uses **AskUserQuestion** to get human guidance
4. Waits for human decision (BLOCKS until response)
5. Returns clear instructions to the calling agent

### Step 5: Orchestrator Continues

1. Updates todo list as tasks complete
2. Moves to next task
3. Repeats code → test → complete cycle
4. Continues until ALL todos are done

## 🔄 The Orchestration Flow

```
USER REQUEST
    ↓
[YOU] Invoke orchestrator agent
    ↓
[ORCHESTRATOR] Creates todo list
    ↓
[ORCHESTRATOR] Delegates task to coder
    ↓
[CODER] Implements feature
    ↓
    ├─→ Problem? → [STUCK] → Human input → Continue
    ↓
[CODER] Reports completion
    ↓
[ORCHESTRATOR] Delegates to tester
    ↓
[TESTER] Visual testing with Playwright MCP
    ↓
    ├─→ Failure? → [STUCK] → Human input → Continue
    ↓
[TESTER] Reports success
    ↓
[ORCHESTRATOR] Marks todo complete, moves to next
    ↓
Repeat until all todos done
    ↓
PROJECT COMPLETE
```

## 🛠️ Agent Capabilities

### Orchestrator Agent
- **Tools**: TodoWrite, Task, AskUserQuestion, Read, Glob, Grep
- **Purpose**: Strategic planning and task delegation
- **Delegates to**: coder, tester, stuck
- **Creates**: Detailed todo lists
- **Tracks**: Overall project progress

### Coder Agent
- **Tools**: Read, Write, Edit, Glob, Grep, Bash, Task
- **Purpose**: Implement specific features/functionality
- **Invokes**: stuck agent when ANY problem occurs
- **Returns**: Implementation details and file changes
- **NEVER**: Uses fallbacks or workarounds

### Tester Agent
- **Tools**: Task (for Playwright MCP), Read, Bash
- **Purpose**: Visual testing with Playwright MCP
- **Tests with**: Screenshots, DOM inspection, interactions
- **Invokes**: stuck agent when ANY test fails
- **Returns**: Pass/fail with screenshot evidence
- **NEVER**: Marks failing tests as passing

### Stuck Agent
- **Tools**: AskUserQuestion, Read, Bash, Glob, Grep
- **Purpose**: MANDATORY human escalation point
- **Used by**: ALL agents when problems occur
- **Provides**: Human decisions to unblock agents
- **ONLY agent**: Allowed to use AskUserQuestion

## 💡 Usage Examples

### Example 1: Building a Web Application

```
User: "Build a simple todo app with React"

You (main Claude):
→ Invoke orchestrator agent with requirements

Orchestrator:
→ Creates todo list:
  1. Set up React project structure
  2. Create TodoList component
  3. Create TodoItem component
  4. Add state management
  5. Style the application
  6. Test all functionality

→ Invokes coder for task #1

Coder:
→ Runs: npx create-react-app todo-app
→ ERROR: npx command not found
→ Invokes stuck agent

Stuck:
→ Asks human: "npx not found. How to proceed?"
→ Options: Install Node.js / Use different setup / Skip npm
→ Human chooses: "Install Node.js"
→ Returns to coder: "Install Node.js first"

Coder:
→ Continues with Node.js installation
→ Completes React setup
→ Reports back to orchestrator

Orchestrator:
→ Invokes tester

Tester:
→ Uses Playwright MCP to navigate to http://localhost:3000
→ Takes screenshot
→ Verifies React app loads
→ Reports success to orchestrator

Orchestrator:
→ Marks task #1 complete
→ Moves to task #2
→ Continues...
```

### Example 2: Testing Failure Flow

```
Orchestrator:
→ Invokes tester after coder completes UI

Tester:
→ Uses Playwright MCP to load page
→ Takes screenshot
→ SEES: Button is misaligned, wrong color
→ Invokes stuck agent with screenshot

Stuck:
→ Asks human: "Button styling incorrect (see screenshot). Fix?"
→ Options: Fix alignment & color / Accept as-is / Redesign
→ Human chooses: "Fix alignment & color"
→ Returns to tester

Tester:
→ Reports back to orchestrator: "Test failed, needs fix"

Orchestrator:
→ Invokes coder to fix button styling

Coder:
→ Updates CSS
→ Reports completion

Orchestrator:
→ Invokes tester again to re-verify
```

## 🎯 Your Role (Main Claude Instance)

As the main Claude instance, you are the ENTRY POINT:

1. **Receive** user's project request
2. **Invoke** the orchestrator agent immediately
3. **Monitor** progress as agents work
4. **Relay** final results back to user when orchestrator completes

**DO NOT:**
- Try to implement tasks yourself
- Skip the orchestrator
- Let agents work without orchestration
- Allow fallbacks when problems occur

**ALWAYS:**
- Start with the orchestrator agent
- Let specialized agents do their jobs
- Ensure stuck agent is invoked for ALL problems
- Trust the orchestration system

## 🚀 Getting Started

When a user gives you a task:

1. Understand the requirements
2. Use the Task tool to invoke the `orchestrator` agent
3. Pass the complete requirements in your prompt
4. Let the orchestration system take over
5. Report final results when orchestrator completes

Example invocation:
```
Task tool with:
  subagent_type: "orchestrator"
  prompt: "Build a todo application with React. Requirements: [detailed requirements here]"
```

## ✅ System Success Criteria

The system is working correctly when:
- ✅ Orchestrator creates comprehensive todo lists
- ✅ Coder implements features without fallbacks
- ✅ Tester verifies with Playwright screenshots
- ✅ Stuck agent gets human input for ALL problems
- ✅ NO agent proceeds blindly past errors
- ✅ Projects complete successfully with quality code

## 🔥 Remember

This is a SIMPLE but POWERFUL system:
- Orchestrator = Brain (planning & delegation)
- Coder = Hands (implementation)
- Tester = Eyes (visual verification)
- Stuck = Voice (human guidance)

Keep it simple. Trust the agents. Get human input when needed. Build amazing things! 🚀
