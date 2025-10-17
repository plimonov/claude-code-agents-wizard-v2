# Claude Code Agent Orchestration System v2 🚀

A simple yet powerful orchestration system for Claude Code that uses specialized agents to manage complex projects from start to finish, with mandatory human oversight and visual testing.

## 🎯 What Is This?

This is a **custom Claude Code agent system** that transforms how you build software projects. Instead of one AI doing everything, you get four specialized agents working together:

- **🧠 Orchestrator** - The strategic brain that sees the big picture and manages todo lists
- **✍️ Coder** - The implementation specialist that writes clean, working code
- **👁️ Tester** - The visual QA that verifies everything using Playwright screenshots
- **🆘 Stuck** - The human escalation point that ensures you stay in control

## ⚡ Key Features

- **No Fallbacks**: When ANY agent hits a problem, you get asked - no assumptions, no workarounds
- **Visual Testing**: Playwright MCP integration for screenshot-based verification
- **Todo Tracking**: Always see exactly where your project stands
- **Simple Flow**: orchestrator → coder → tester → repeat until done
- **Human Control**: The stuck agent ensures you're always in the loop

## 🚀 Quick Start

### Prerequisites

1. **Claude Code CLI** installed ([get it here](https://docs.claude.com/en/docs/claude-code))
2. **Node.js** (for Playwright MCP)

### Installation

```bash
# Clone this repository
git clone https://github.com/IncomeStreamSurfer/claude-code-agents-wizard-v2.git
cd claude-code-agents-wizard-v2

# Start Claude Code in this directory
claude
```

That's it! The agents are automatically loaded from the `.claude/` directory.

## 📖 How to Use

### Starting a Project

When you want to build something, just tell Claude your requirements:

```
You: "Build a todo app with React and TypeScript"
```

Claude will automatically:
1. Invoke the **orchestrator** agent
2. The orchestrator creates a detailed todo list
3. Tasks get delegated to **coder** → **tester** in sequence
4. If ANY problem occurs, the **stuck** agent asks you what to do
5. Project continues until complete

### The Workflow

```
USER: "Build X"
    ↓
ORCHESTRATOR: Creates detailed todos
    ↓
ORCHESTRATOR: Delegates to coder
    ↓
CODER: Implements feature
    ↓
    ├─→ Problem? → STUCK AGENT → You decide → Continue
    ↓
TESTER: Visual testing with Playwright screenshots
    ↓
    ├─→ Test fails? → STUCK AGENT → You decide → Continue
    ↓
ORCHESTRATOR: Marks complete, moves to next todo
    ↓
Repeat until all todos done ✅
```

## 🛠️ Agent Details

### Orchestrator Agent
**Purpose**: Strategic planning and delegation

- Creates comprehensive todo lists
- Sees the complete project from A-Z
- Delegates tasks to specialized agents
- Tracks overall progress

**When it's used**: Automatically at the start of any multi-step project

### Coder Agent
**Purpose**: Implementation specialist

- Writes clean, functional code
- Implements specific features/tasks
- **Never uses fallbacks** - escalates problems immediately
- Returns detailed implementation reports

**When it's used**: When a coding task needs implementation

### Tester Agent
**Purpose**: Visual quality assurance

- Uses **Playwright MCP** to see rendered output
- Takes screenshots to verify layouts
- Tests interactions (clicks, forms, navigation)
- Validates at multiple screen sizes
- **Never marks failing tests as passing**

**When it's used**: Immediately after coder completes implementation

### Stuck Agent
**Purpose**: Mandatory human escalation

- **ONLY agent** that can ask you questions
- Invoked by ALL other agents when problems occur
- Presents clear options for you to choose
- Blocks progress until you respond
- Ensures no blind fallbacks or workarounds

**When it's used**: Whenever ANY agent encounters ANY problem

## 🚨 The "No Fallbacks" Rule

**This is the key differentiator:**

Traditional AI: Hits error → tries workaround → might fail silently
**This system**: Hits error → asks you → you decide → proceeds correctly

Every agent is **hardwired** to invoke the stuck agent rather than use fallbacks. You stay in control.

## 💡 Example Session

```
You: "Build a landing page with a contact form"

Orchestrator creates todos:
  1. Set up HTML structure
  2. Create hero section
  3. Add contact form with validation
  4. Style with CSS
  5. Test form submission

→ Delegates to Coder for task #1

Coder: Creates index.html
→ Reports completion

→ Orchestrator delegates to Tester

Tester: Uses Playwright to navigate to page
Tester: Takes screenshot
Tester: Verifies HTML structure visible
→ Reports success

→ Orchestrator moves to task #2

Coder: Implements hero section
Coder: ERROR - image file not found
→ Invokes Stuck Agent

Stuck Agent asks YOU:
  "Hero image 'hero.jpg' not found. How to proceed?"
  Options:
  - Use placeholder image
  - Download from Unsplash
  - Skip image for now

You choose: "Download from Unsplash"

→ Coder proceeds with your decision
... and so on
```

## 📁 Repository Structure

```
.
├── .claude/
│   ├── CLAUDE.md              # Main orchestration logic
│   └── agents/
│       ├── orchestrator.md    # Strategic planning agent
│       ├── coder.md          # Implementation agent
│       ├── tester.md         # Visual testing agent
│       └── stuck.md          # Human escalation agent
├── .mcp.json                  # Playwright MCP configuration
├── .gitignore
└── README.md
```

## 🎓 Learn More

### Resources

- **[SEO Grove](https://seogrove.ai)** - AI-powered SEO automation platform
- **[ISS AI Automation School](https://www.skool.com/iss-ai-automation-school-6342/about)** - Join our community to learn AI automation
- **[Income Stream Surfers YouTube](https://www.youtube.com/incomestreamsurfers)** - Tutorials, breakdowns, and AI automation content

### Support

Have questions or want to share what you built?
- Join the [ISS AI Automation School community](https://www.skool.com/iss-ai-automation-school-6342/about)
- Subscribe to [Income Stream Surfers on YouTube](https://www.youtube.com/incomestreamsurfers)
- Check out [SEO Grove](https://seogrove.ai) for automated SEO solutions

## 🤝 Contributing

This is an open system! Feel free to:
- Add new specialized agents
- Improve existing agent prompts
- Share your agent configurations
- Submit PRs with enhancements

## 📝 How It Works Under the Hood

This system leverages Claude Code's [subagent system](https://docs.claude.com/en/docs/claude-code/sub-agents):

1. **Agents are defined** in `.claude/agents/*.md` files
2. **Main logic** is in `.claude/CLAUDE.md`
3. **Playwright MCP** is configured in `.mcp.json`
4. **Claude Code automatically loads** these when you run `claude` in this directory

The magic happens because each agent has:
- **Specific tools** they can access
- **Clear responsibilities** defined in their prompts
- **Hardwired rules** about when to escalate
- **No ability** to use AskUserQuestion except the stuck agent

## 🎯 Best Practices

1. **Trust the orchestrator** - Let it create the todo list
2. **Review screenshots** - The tester provides visual proof
3. **Make decisions when asked** - The stuck agent needs your guidance
4. **Don't interrupt the flow** - Let agents complete their cycles
5. **Check the todo list** - Always visible with `/todos` command

## 🔥 Pro Tips

- Use `/agents` command to see all available agents
- The orchestrator maintains a todo list you can check anytime
- Screenshots from the tester are saved and can be reviewed
- Each agent has access to different tools - check their `.md` files to see capabilities

## 📜 License

MIT - Use it, modify it, share it!

## 🙏 Credits

Built by [Income Stream Surfer](https://www.youtube.com/incomestreamsurfers)

Powered by Claude Code's agent system and Playwright MCP.

---

**Ready to build something amazing?** Just run `claude` in this directory and tell it what you want to create! 🚀
