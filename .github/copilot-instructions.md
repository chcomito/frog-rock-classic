# Frog Rock Classic - AI Coding Agent Instructions

## Project Overview

Frog Rock Classic is a web-based game implementing a classic Frogger-style gameplay. The project uses vanilla HTML, CSS, and JavaScript with a simple static file structure—no build tools or frameworks required.

### Architecture

- **index.html** - Single-page entry point; contains HTML structure and embeds game logic
- **styles.css** - Game UI styling (board, frog, obstacles, score display)
- **public/** - Static assets directory (reserved for images, sounds, or additional resources)

## Key Development Patterns

### Game Loop Architecture

- Use a `requestAnimationFrame`-based game loop for smooth 60fps rendering
- Update game state (entity positions, collisions) separately from rendering
- Collision detection occurs during update phase before re-render

### Entity Management

- Frog entity: player-controlled character with directional movement (arrow keys or WASD)
- Obstacles: stateless moving entities (cars, logs) that cycle off-screen and respawn
- Goals: end zones where frog must safely reach
- Use object literals for entities with properties: `{ x, y, width, height, speed, type }`

### Input Handling

- Listen for `keydown` events (not keypress - repeat delay is problematic for games)
- Apply velocity on key press; reset on key release for responsive controls
- Prevent default browser behavior for arrow keys (`event.preventDefault()`)

### Canvas Rendering (if used) vs DOM Elements

- Currently set up for DOM-based rendering (CSS positioning)
- If performance requires: migrate to Canvas2D with `<canvas>` element in HTML and 2D context drawing

### Styling Conventions

- Use CSS Grid or Flexbox for board layout
- Frog sprite: centered positioning within its grid cell
- Obstacles: absolute positioning with CSS animations or transform for movement
- Z-index layering: obstacles (1) < frog (2) < UI (3)

## Common Tasks & Commands

### Starting Development

1. Open `index.html` in browser (or use VS Code Live Server extension)
2. Modify HTML structure in `<body>` (game board container, score display)
3. Add styles to `styles.css` incrementally
4. Write game logic in `<script>` tag at end of `index.html`

### Adding New Features

- **New obstacles**: Define entity properties; add to update/collision systems; style in CSS
- **Score/lives tracking**: DOM element in HTML; update on game events (goal reached, collision)
- **Difficulty levels**: Modify obstacle speed multiplier; persist to localStorage if needed
- **Sounds**: Placeholder data attributes on entities; integrate Web Audio API or `<audio>` elements

### Debugging

- Use browser DevTools Console for game state inspection
- Log entity positions during collisions: `console.log({frog, obstacle, collides})`
- Inspect DOM in Elements tab to verify positioning and z-index
- Check Performance tab for animation frame timing

## Project-Specific Conventions

### Naming

- Prefixed CSS classes: `.game-board`, `.game-frog`, `.game-obstacle--car`, `.game-score`
- JavaScript variables: `gameState`, `frogEntity`, `obstacleList`, `isGameRunning`
- HTML IDs: `#game-container`, `#score-display` (use sparingly; prefer classes)

### State Management (Simple Approach)

```javascript
const gameState = {
  score: 0,
  lives: 3,
  level: 1,
  frogPosition: { x: 0, y: 0 },
  obstacles: [],
  isGameOver: false,
  isPaused: false
};
```

### Data Flow

1. **Input** → Update frogPosition velocity
2. **Physics** → Apply velocity; clamp bounds; move obstacles
3. **Collision Detection** → Check frog vs obstacles/goals
4. **State Update** → Modify gameState (score, lives, level)
5. **Render** → Update DOM positions and UI text

## File Organization

If the project expands:
- Keep game logic in `index.html` `<script>` until ~500 lines
- Beyond that: extract to `public/game.js`, `public/entities.js`, `public/collision.js`
- Consider a simple module pattern or ES6 modules if using a bundler

## Integration Points

- **localStorage**: Persist high scores or game settings (optional)
- **Responsive Design**: Media queries in CSS for mobile/tablet viewport sizes
- **Accessibility**: Keyboard-only controls already in place; add ARIA labels for score/status

## Next Steps for Agents

When implementing features:
1. Identify which phase (Input/Physics/Collision/Render) your change affects
2. Update both the state and the DOM representation
3. Test with browser DevTools to confirm positioning and collision logic
4. Verify keyboard input responsiveness isn't blocked by event listeners
