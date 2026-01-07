# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a standalone confetti celebration webpage built as a single HTML file. It displays customizable title/subtitle text with animated confetti effects and includes a Vercel-style theme switcher for light/dark/system modes.

## Architecture

**Single-File Application**: All code lives in `index.html` - HTML structure, CSS animations, theme management, and confetti physics engine are all in one file.

**Key Systems**:

1. **Theme Management**: Runs before page render to prevent flash. Theme state persists in localStorage with three modes (light/dark/system). System mode listens for OS preference changes.

2. **Confetti Engine**: Canvas-based particle system with physics simulation. Two modes:
   - Initial load: 800ms burst sequence from bottom corners
   - Button-triggered: 50ms burst with MAX_CONFETTI (30) concurrent animation limit

3. **State Management**:
   - `activeConfettiCount`: Tracks concurrent canvas animations to enforce MAX_CONFETTI limit
   - `cooldownActive`: Prevents button spam when at capacity (2-second cooldown)

4. **URL Parameters**: `?title=X&subtitle=Y` dynamically updates content on load

## Styling

Uses Tailwind CDN with custom dark mode colors configured inline. Custom CSS keyframe animation (`buttonAppear`) for confetti button entrance after initial burst completes.

## Confetti Physics

Each particle has:
- Position (x, y), velocity (vx, vy), gravity, rotation
- Shape (square/circle/triangle/rectangle)
- Life decay system for fade-out
- Canvas cleanup when all particles complete

Cannons fire from corners (0, 1) and (1, 1) at angles -45° and -135° with 80° spread.

## Development

No build process required. Open `index.html` directly in a browser or serve with any static file server.
