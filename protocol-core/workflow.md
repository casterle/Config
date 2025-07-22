# Copilot Workflow Protocol

This file outlines a dual-buffer protocol for interacting with Copilot safely, modularly, and reversibly.

---

## 🧠 Memory Architecture

- 🪟 **Workflow Buffer**  
  Permanent memory layer for command parsing, UI rules, and behavior scaffolding.  
  Cannot be cleared by system commands to avoid accidental loss.

- 🗂️ **Instructions Buffer**  
  Mutable content layer that stores session-specific instructions.  
  Can be cleared only with explicit `C` command confirmation.

<!--
Rationale:
Separating protocol logic from behavioral guidance enforces modular control and guarantees recoverability.
-->

---

## 🎮 Command Parsing Rules

- Accept only **uppercase**, **single-letter** commands
- Must begin the line, followed by CR or LF
- Parsed only from the focused text/edit window

<!--
Design Note:
This replicates CLI interpreter syntax for deterministic input control and avoids accidental command execution.
-->

---

## 🖥️ Text/Edit Window Behavior

- Two focused text editors: Workflow and Instructions
- Commands affect only the active editor
- Workflow editor disables the `C` command entirely

---

## 🖱️ Simulated Command Strip

- Commands displayed as inline buttons for visibility: [`A`] [`S`] [`M`] [`L`] [`C`]  
- Positioned at bottom of buffers and responses

---

## 🔁 Reversibility & Log Persistence

- Instruction decisions are stored per version in log files (`instruction-log-vX.X.md`)
- Users can replay or fork sessions at will
- Supported commands:
  - `Replay session v1.0`
  - `Fork session v1.0 into v1.1`

---

## 🧾 Quoting Convention

- User quotes Copilot using `>` to preserve clarity in multi-turn protocols

---

## 📌 Current Focus Version

- Active protocol version: `v1.0`
- MCP discussion paused at `v1.1-mcp-pending`
