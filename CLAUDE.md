# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository

**GitHub:** https://github.com/eggshellpress-a11y/claude-test-project
**Branch:** main

### Git workflow
- Commit and push after every meaningful change — never leave a session with unpushed work
- Commit messages: imperative mood, short subject line, bullet-point body for multi-part changes (e.g. "Add sound effects to Tic Tac Toe")
- Stage specific files by name rather than `git add .`
- Always `git push` immediately after committing so GitHub reflects the latest state

## Project Structure

This is a collection of self-contained web games and mini-projects, each built as a single HTML file with embedded CSS and JavaScript. No build tools, bundlers, or dependencies — everything runs directly in the browser by opening the file.

## Architecture Pattern

Each game/project follows this structure within a single `.html` file:
- **CSS** — embedded in `<style>`, using Google Fonts via `@import`
- **HTML** — semantic markup, minimal DOM structure
- **JS** — embedded in `<script>`, vanilla JS only, no frameworks or libraries

State is managed with plain module-level variables. No localStorage persistence (scores reset on page reload by design).

## Easter Tic Tac Toe (`easter-tictactoe.html`)

**Game logic:**
- `board` — flat 9-element array, values are `'egg'`, `'bunny'`, or `null`
- `makeMove(index, player)` — single entry point for all moves; calls `checkWinner()` and `endGame()` or advances turn
- `checkWinner(b?)` — checks `WINNING_LINES`; accepts an optional board param for use inside minimax
- `minimax(b, depth, isMax)` — recursive minimax; bunny maximizes, egg minimizes

**AI modes:**
- Easy: 40% chance of calling `bestMove()`, otherwise `randomMove()`
- Hard: always `bestMove()` via full minimax (unbeatable)

**Rendering:** DOM is mutated directly — no virtual DOM. Cells get CSS classes (`egg-cell`, `bunny-cell`, `winner-cell`, `taken`) to drive visual state.
