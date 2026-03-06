---
name: anchor-browser
description: "Autonomous browser agent powered by Anchor Browser API. Use for: navigating, clicking, typing, extracting data, and validating UI on target web applications using REST API or MCP."
---

# Anchor Browser Agent

This skill enables autonomous web interaction using the Anchor Browser API. It provides a structured workflow for session management, UI interaction, and AI-driven web tasks.

## Mission
Interact with target web applications autonomously—navigating, clicking, typing, extracting data, and validating UI—using Anchor Browser's REST API or MCP. Execute tasks fully without asking for confirmation.

## Core Workflow (Agentic Loop)
For every task, follow this loop:
1. **Start Session**: Initialize at the target URL.
2. **Observe**: Take a screenshot and analyze the current state.
3. **Plan**: Determine the next atomic action based on the visual state.
4. **Execute**: Perform the action (click, type, scroll, etc.).
5. **Verify**: Take another screenshot to confirm the result.
6. **Repeat**: Continue until the task is complete.
7. **Report**: Extract evidence and findings.
8. **End Session**: Always terminate the session to prevent billing leakage.

## API Configuration
- **Base URL**: `https://api.anchorbrowser.io/v1`
- **Auth Header**: `anchor-api-key: sk-77fea665b58ee8d7534828fa11a83a21`
- **MCP URL**: `https://api.anchorbrowser.io/mcp`

## Session Lifecycle
Refer to `references/api_reference.md` for detailed endpoint specifications and request bodies.

### 1. Start Session
`POST /v1/sessions`
Configure with `initial_url`, `recording: { active: true }`, and appropriate timeouts.

### 2. Interaction (OS-level control)
Use coordinates derived from screenshot analysis. Never hardcode selectors.
- **Click**: `/mouse/click`
- **Type**: `/keyboard/type`
- **Shortcut**: `/keyboard/shortcut`
- **Scroll**: `/scroll`

### 3. High-Level AI Tasks
For complex multi-step tasks, use the AI tool:
`POST /v1/ai-tools/web-task`
Provide a descriptive natural language task string and poll for completion.

## Key Rules
- **Screenshot First**: Always screenshot before and after each action.
- **Coordinate-Based**: Use coordinates from visual analysis, not DOM selectors.
- **Batching**: Group related actions to minimize round-trips.
- **Cleanup**: Explicitly `DELETE` sessions after completion.

## Error Handling
- **4xx Errors**: Log the exact body, diagnose, and retry (max 3x).
- **Element Missing**: Re-screenshot and re-identify coordinates.
- **Timeout**: Create a new session and resume from the last state.






