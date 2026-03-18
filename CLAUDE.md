# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains a single tic-tac-toe game implemented as a self-contained HTML file:

- **tictactoe.html** - Full-featured tic-tac-toe with 2-player (PvP) and vs AI modes

It is a single-file HTML application with inline CSS and JavaScript. No build process, package manager, or external dependencies are required.

## GitHub Repository

**Repository:** https://github.com/adaymecunha/tictactoe-games

All changes are tracked in git with clean commit messages. This allows easy reverting and maintains a complete project history.

### Git Workflow

When making changes:

```bash
# Make your code changes, then:
git add <files>           # Stage changes
git commit -m "Description of change"
git push origin master    # Push to GitHub
```

### Viewing History

```bash
git log                   # View commit history
git diff HEAD~1          # Compare current with last commit
git checkout <hash>      # Revert to a specific commit
```

## Running the Games

Open either HTML file directly in a web browser:
- Double-click the `.html` file, or
- Right-click → "Open with" → select your browser

No local server or build step is needed.

## Architecture

Both games follow the same structure:

**Game State:**
- `board` - 9-element array representing the grid (indices 0-8)
- `current` - Current player ('X'/'O' or 'P'/'M')
- `gameOver` - Boolean flag for game state
- `scores` - Object tracking wins and draws across games

**Core Logic:**
- `WINS` - Array of 8 winning combinations (rows, columns, diagonals)
- `checkWin()` - Checks if current board state matches any winning combination
- `play(i)` - Core turn logic: places mark, checks win/draw, switches player
- `reset()` - Clears board for next game, preserves scores
- `updateScores()` - Refreshes score display

**AI (tictactoe.html only):**
- `bestMove()` - Returns AI's next move using priority strategy:
  1. Win if possible
  2. Block opponent from winning
  3. Take center (position 4)
  4. Take random corner
  5. Take random edge
  6. Return -1 if board full
- `aiMove()` - Executes AI turn with 350ms delay for UX

## Modifying the Games

**Change winning conditions:** Edit the `WINS` array in the `<script>` section.

**Adjust AI difficulty:** Modify `bestMove()` function or add randomization to strategic choices.

**Customize styling:** Edit the `<style>` section. Color scheme uses CSS custom properties embedded as hex values.

**Add new modes:** Duplicate the mode-toggle button structure and add corresponding game logic branches in `setMode()`.

**Score persistence:** Currently stored in memory only. To save scores across sessions, add `localStorage` calls in `updateScores()` and initialization.
