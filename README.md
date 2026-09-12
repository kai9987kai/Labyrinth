# Cognitive Labyrinth v4

**Cognitive Labyrinth** is a browser-based procedural maze, reflection, self-regulated learning, and productivity experiment built entirely with **HTML, CSS, and vanilla JavaScript**.

Rather than treating the maze as only a puzzle, Cognitive Labyrinth combines navigation with strategically placed reflection nodes, adaptive prompts, session analytics, journaling, offline coaching, optional AI coaching, deterministic maze generation, and persistent progress.

Version 4 substantially redesigns the original project while retaining its core idea: **move, think, reflect, adapt, and continue**.

---

# Overview

Each session generates a procedural maze containing reflection nodes.

As you navigate the maze, the application records your route and periodically prompts you to reflect on:

- Current goals
- Problems and blockers
- Learning progress
- Planning
- Decision making
- Project development
- Retrieval and recall
- Strategy changes
- Transfer of knowledge
- Next actions

Your responses become part of a persistent journal.

Cognitive Labyrinth can operate completely offline using its built-in **Local Coach**, or optionally communicate with an OpenAI-compatible server-side proxy for more advanced AI-generated reflection.

---

# Version 4

Cognitive Labyrinth v4 is a major architectural upgrade.

It introduces:

- Improved maze-generation architecture
- Multiple maze algorithms
- Deterministic seeded generation
- Adaptive reflection prompts
- Improved Local Coach
- Secure optional AI coaching
- Advanced run analytics
- Session history
- Personal best tracking
- Persistent elapsed time
- IndexedDB storage
- localStorage fallback
- Improved import/export
- Better accessibility
- Improved keyboard controls
- Touch/swipe controls
- Focus mode
- Daily deterministic mazes
- Better route analysis
- Improved hint and solver systems
- Configurable maze complexity
- Improved mobile behaviour
- More robust state restoration
- Better error handling

The entire application remains contained within a **single HTML file**.

No build process is required.

---

# Core Concept

Cognitive Labyrinth combines several ideas:

```text
Procedural Maze
      ↓
Navigation
      ↓
Reflection Nodes
      ↓
Prompt Selection
      ↓
User Reflection
      ↓
Local / AI Coaching
      ↓
Journal
      ↓
Behaviour + Route Analytics
      ↓
Adaptation
```

The maze therefore acts as both:

1. A spatial puzzle
2. A pacing mechanism for structured reflection

---

# Main Features

## Procedural Maze Generation

Each session creates a complete navigable maze.

Version 4 uses a wall-bitmask maze representation rather than treating each square simply as a wall or floor tile.

This produces cleaner topology and makes maze analysis significantly easier.

Supported generation systems include:

- Recursive Backtracker
- Randomized Prim

Different algorithms produce different structural characteristics.

Recursive Backtracker typically creates:

- Longer corridors
- Deep branches
- Fewer junctions

Randomized Prim typically produces:

- More branching
- More local choices
- Denser navigation patterns

---

# Seeded Generation

Every maze can be generated from a deterministic seed.

Example:

```text
kai9987kai-2026
```

Using the same:

- Seed
- Maze size
- Maze algorithm
- Complexity settings

will regenerate the same maze.

Seeds make it possible to:

- Replay a maze
- Share a maze
- Compare route efficiency
- Run experiments
- Benchmark algorithms

---

# Daily Maze

Cognitive Labyrinth can generate a deterministic daily maze.

The date contributes to the seed, meaning everyone using the same configuration for that date can reproduce the same maze.

This creates a simple daily challenge mode without requiring a server.

---

# Configurable Maze Sizes

Supported maze dimensions include configurations such as:

```text
10 × 10
14 × 14
20 × 20
26 × 26
32 × 32
```

Larger mazes produce substantially longer optimal routes and more navigation opportunities.

---

# Loop Generation

Traditional perfect mazes contain exactly one route between any two cells.

Cognitive Labyrinth can optionally introduce loops.

Loops create:

- Alternate routes
- Additional junctions
- Navigation ambiguity
- More strategic decision making
- Less predictable optimal routes

Loop density can be configured from the interface.

---

# Farthest Exit Placement

The finish is not simply placed in an arbitrary corner.

The maze engine analyses distances from the starting point and can select an appropriately distant reachable cell.

This produces more meaningful maze traversal and avoids artificially drilling a corridor to a predetermined destination.

---

# Reflection Nodes

Reflection nodes are distributed throughout the maze.

Reaching one activates a cognitive prompt.

Nodes can encourage:

- Planning
- Monitoring
- Retrieval
- Explanation
- Reflection
- Strategy adaptation
- Transfer
- Problem decomposition
- Implementation intentions

Node placement is designed to distribute reflection through the run rather than placing prompts randomly with no relationship to progression.

---

# Adaptive Prompt Engine

The prompt system is no longer limited to selecting a random question from a small static list.

Version 4 supports multiple prompt categories.

## Planning

Examples of the underlying objective:

```text
What exactly are you trying to achieve?

What is the smallest measurable next milestone?
```

---

## Retrieval

Encourages recalling information without immediately checking an external source.

This can support learning and memory practice.

---

## Explanation

Encourages explaining a concept or problem in the user's own words.

---

## Monitoring

Encourages comparison between:

```text
Expected progress
vs
Actual progress
```

---

## Obstacle Diagnosis

Prompts help identify whether friction originates from:

- Missing knowledge
- Tool limitations
- Poor planning
- Unclear requirements
- Environment
- Motivation
- Time
- Implementation errors

---

## Transfer

Encourages connecting current learning or experience with another problem.

---

## Adaptation

Prompts ask whether the current strategy should continue or change.

---

## Implementation Intentions

The application can turn reflection into an explicit behavioural rule:

```text
If X occurs,
then I will do Y.
```

Example:

```text
If I become stuck debugging the renderer,
then I will reproduce the smallest failing case before changing more code.
```

This makes the journal more action-oriented rather than purely descriptive.

---

# Local Coach

Cognitive Labyrinth works without an internet connection.

The built-in **Local Coach** analyses reflection text using lightweight browser-side logic.

It can identify signals related to:

- Being stuck
- Planning
- Learning
- Building
- Testing
- Time pressure
- Uncertainty
- Actionability
- Problems
- Progress

The Local Coach then generates a structured response containing combinations of:

```text
Insight

Question

Next Action

Implementation Intention
```

No remote server is required.

No reflection needs to leave the browser when Local Coach mode is active.

---

# Optional AI Coach

Cognitive Labyrinth can optionally connect to an AI model through a **server-side proxy**.

The intended architecture is:

```text
Cognitive Labyrinth
        ↓
Your Proxy
        ↓
OpenAI Responses API
```

This is preferable to embedding an API key directly inside browser JavaScript.

The application can pass information such as:

- Reflection prompt
- User response
- Current run state
- Steps
- Node completion
- Position
- Session context

The response can then be added to the journal.

---

# AI Failure Fallback

If the remote AI coach fails because of:

- Network failure
- Timeout
- Invalid proxy response
- Server error
- API error

the application can fall back to the Local Coach.

This avoids losing the user's reflection because an external service is unavailable.

---

# Security

Cognitive Labyrinth v4 is designed so that API secrets do not need to be embedded directly in public browser code.

Recommended architecture:

```text
Browser
   ↓
Your controlled proxy
   ↓
AI provider
```

Sensitive credentials should remain on the server.

Proxy bearer credentials are not intended to become permanent exported journal data.

---

# Solver

The built-in maze solver calculates a route from the player's current location to the finish.

The solution can be rendered directly over the maze.

Unlike earlier behaviour, the route can be recalculated after movement so that the displayed solution remains consistent with the player's current location.

---

# Hint System

Hints reveal the next useful movement rather than automatically solving the maze.

Hints are counted as part of session analytics.

This allows route statistics to distinguish between:

- Independent navigation
- Hint-assisted navigation

---

# Fog of War

Fog mode hides unexplored areas.

A configurable vision radius controls how far the player can see.

Previously explored cells can remain visible.

Fog mode increases:

- Spatial memory requirements
- Exploration difficulty
- Route-planning demands

---

# Trail

The application can visualise previously visited cells.

This makes it easier to understand:

- Route history
- Backtracking
- Exploration patterns
- Repeated areas

---

# Undo

Recent movements can be reversed.

Undo updates player position while preserving consistent run state.

---

# Focus Mode

Focus mode reduces unnecessary interface distractions while navigating or reflecting.

This can be useful for:

- Study sessions
- Long maze runs
- Mobile devices
- Concentration-oriented use

---

# Session Goal

A session can include a goal or intention.

Examples:

```text
Finish the UV layout for my environment model.

Understand the rendering bug.

Review today's lecture.

Plan the first playable prototype.

Decide what feature I should build next.
```

Reflection prompts can then be interpreted within the context of that goal.

---

# Session Profiles

Cognitive Labyrinth can support different reflection contexts such as:

- General
- Project
- Study
- Creative

Different profiles can influence the type of reflection encouraged by the system.

---

# Navigation Analytics

Version 4 tracks considerably more than simple step count.

Possible metrics include:

- Steps taken
- Elapsed active time
- Shortest possible route
- Route efficiency
- Cells visited
- Maze coverage
- Revisits
- Revisit rate
- Wall collisions
- Hints used
- Nodes completed
- Junction count
- Dead ends
- Loop count
- Structural complexity
- Completion state

---

# Route Efficiency

One useful measurement is the relationship between the player's route and the optimal route.

Conceptually:

```text
Efficiency =
Shortest Route Length
÷
Actual Route Length
```

A more direct route therefore receives a higher efficiency score.

The metric is intended as navigational information rather than a judgement of the reflection quality.

Exploration may intentionally produce lower route efficiency.

---

# Coverage

Coverage measures how much of the traversable maze the player explored.

This distinguishes two different play styles:

```text
Goal-oriented navigation

vs

Exploratory navigation
```

---

# Revisit Analysis

Repeatedly entering cells can indicate:

- Exploration
- Backtracking
- Route uncertainty
- Deliberate checking

The application records revisitation independently from raw step count.

---

# Maze Structural Analytics

Because v4 represents the maze as a graph, the application can calculate structural characteristics such as:

- Dead ends
- Junctions
- Path length
- Connectivity
- Loop count
- Route distance
- Approximate structural complexity

These metrics can also be useful for comparing generation algorithms.

---

# Session History

Completed sessions can be stored locally.

Historical information can include:

- Date
- Seed
- Maze configuration
- Completion time
- Steps
- Route efficiency
- Hints
- Reflection nodes
- Other performance metrics

---

# Personal Bests

Stored history can be used to compare current performance against previous runs.

Examples include:

- Fastest completion
- Fewest steps
- Highest route efficiency
- Largest completed maze

---

# Analytics Graph

Cognitive Labyrinth includes browser-rendered analytics visualisation.

The chart uses the HTML Canvas API and therefore does not require an external charting framework.

This keeps the project dependency-free.

---

# Journal

Every submitted reflection can be stored in the session journal.

An entry may contain:

```text
Timestamp
Seed
Maze position
Prompt
User reflection
Coach response
Coach mode
Session metadata
```

---

# Journal Search

Journal entries can be filtered or searched.

This makes longer-term reflection histories easier to inspect.

---

# Markdown Export

Journal data can be exported into a readable Markdown representation.

This is useful for:

- GitHub
- Notes
- Study records
- Project documentation
- Personal reflection archives

---

# JSON Export

A complete structured backup can be exported as JSON.

The export can contain:

```text
Application version
Settings
Maze
Player state
Run statistics
Journal
Session history
Metadata
```

JSON is useful when preserving the exact application state is more important than human readability.

---

# Import

Previously exported Cognitive Labyrinth sessions can be restored.

Version 4 uses stronger validation when loading imported data.

The application checks information such as:

- Structure
- Maze dimensions
- Expected arrays
- Player coordinates
- Configuration
- Version data

before applying imported state.

---

# Persistence

Version 4 uses a more robust persistence system.

Primary storage:

```text
IndexedDB
```

Fallback:

```text
localStorage
```

This allows the application to preserve considerably richer state than relying exclusively on one localStorage JSON string.

---

# Autosave

The application can automatically preserve session state.

Potentially restored information includes:

- Maze
- Seed
- Player position
- Visited cells
- Completed nodes
- Journal
- Settings
- Timer state
- Analytics
- Session history

---

# Persistent Timer

Elapsed run time can survive page restoration.

The timer is designed around accumulated active time rather than blindly starting from zero after every browser reload.

---

# Automatic Visibility Pause

When the browser tab becomes inactive, Cognitive Labyrinth can avoid treating all hidden-tab time as active maze time.

This provides more useful session timing when the user:

- Changes tab
- Minimises the browser
- Temporarily leaves the application

---

# Manual Pause

Sessions can also be manually paused.

---

# Themes

The interface supports multiple visual modes, including combinations such as:

- Dark
- Light
- System
- High contrast

Theme preferences can be stored locally.

---

# Accessibility

Version 4 includes improvements intended to make the application easier to use without relying entirely on pointer interaction.

Features include:

- Keyboard navigation
- Visible focus indicators
- ARIA semantics
- Live status messages
- Reduced-motion support
- High-contrast interface
- Larger touch targets
- Semantic controls
- Responsive layout
- Screen-reader-friendly status information

---

# Reduced Motion

The interface respects environments requesting reduced animation where possible.

Example CSS concept:

```css
@media (prefers-reduced-motion: reduce) {
    /* reduce non-essential transitions and animation */
}
```

---

# Keyboard Controls

Typical controls include:

| Key | Action |
|---|---|
| `↑` | Move up |
| `↓` | Move down |
| `←` | Move left |
| `→` | Move right |
| `W` | Move up |
| `A` | Move left |
| `S` | Move down |
| `D` | Move right |
| `H` | Hint |
| `U` | Undo |
| `Q` | Toggle solution |
| `Ctrl + Enter` | Submit reflection |
| `Cmd + Enter` | Submit reflection on macOS |

---

# Touch Controls

Mobile and tablet users can navigate using swipe gestures.

The maze also supports touch-oriented controls with larger targets.

---

# Haptic Feedback

Where supported by the browser/device, Cognitive Labyrinth can use vibration feedback for events such as:

- Movement errors
- Reflection nodes
- Maze completion
- Hints

Browsers that do not support vibration simply continue without it.

---

# Audio Feedback

Cognitive Labyrinth can generate lightweight sound effects using the Web Audio API.

No external audio assets are required.

Audio can be disabled from the interface.

---

# Responsive Interface

The interface adapts to smaller displays instead of shrinking the entire desktop layout using a global CSS transform.

This improves:

- Text rendering
- Touch behaviour
- Accessibility
- Browser zoom
- Layout consistency

---

# Zoom Controls

Maze/interface presentation can be adjusted without relying on globally scaling the entire HTML document.

---

# Shareable URLs

Maze configuration can be written into URL parameters.

A shared URL can therefore carry settings such as:

```text
seed
size
algorithm
complexity
theme
```

Explicit share-link configuration takes precedence when opening a shared maze so an unrelated local autosave does not silently replace the shared configuration.

---

# Completion Rules

A session can support different completion requirements.

For example:

```text
Reach the exit
```

or:

```text
Complete the required reflection nodes and reach the exit
```

This allows Cognitive Labyrinth to function either as a normal maze or a more structured reflection exercise.

---

# Application Architecture

Although Cognitive Labyrinth remains a single HTML file, the JavaScript is conceptually divided into subsystems.

```text
Application
│
├── Maze Engine
│   ├── Backtracker generator
│   ├── Prim generator
│   ├── Loop generation
│   ├── Graph traversal
│   ├── Solver
│   └── Structural analysis
│
├── Game State
│   ├── Player
│   ├── Visited cells
│   ├── Nodes
│   ├── Timer
│   └── Completion state
│
├── Renderer
│   ├── Maze
│   ├── Player
│   ├── Fog
│   ├── Trail
│   └── Overlays
│
├── Reflection Engine
│   ├── Prompt categories
│   ├── Prompt selection
│   └── Context adaptation
│
├── Coaching
│   ├── Local Coach
│   └── Remote Coach
│
├── Analytics
│   ├── Route metrics
│   ├── Maze metrics
│   ├── Run history
│   └── Visualisation
│
├── Persistence
│   ├── IndexedDB
│   └── localStorage fallback
│
└── Import / Export
    ├── JSON
    └── Markdown
```

---

# Maze Representation

Version 4 uses directional wall flags.

Conceptually each cell stores whether it contains walls in directions such as:

```text
North
East
South
West
```

For example:

```text
N | E | S | W
```

This makes the maze naturally representable as a graph.

The representation improves operations such as:

- Traversal
- Solver generation
- Dead-end detection
- Junction detection
- Loop analysis
- Rendering

---

# Pathfinding

Breadth-first search can be used to calculate shortest routes because each movement has equal cost.

Conceptually:

```text
Queue start cell

while queue not empty:
    inspect next cell

    for every connected neighbour:
        if neighbour not visited:
            record parent
            add neighbour to queue

reconstruct route from destination
```

---

# Deterministic Randomness

The application converts a text seed into deterministic pseudo-random numbers.

This allows procedural behaviour while preserving reproducibility.

Same configuration:

```text
Seed A
Algorithm A
Size A
```

produces the same maze.

---

# Performance

Version 4 reduces unnecessary complete-grid work during routine movement.

Instead of treating every movement as a reason to rebuild all maze state, rendering can update the cells whose presentation actually changed.

The approach becomes increasingly useful on larger grids.

---

# Why Is v4 Only Around 400 Physical Lines?

The v4 source uses a denser formatting style than earlier versions.

Line count therefore does **not** represent application complexity.

For example:

```javascript
function clamp(v,min,max){return Math.max(min,Math.min(max,v));}
```

is one physical line.

The same function formatted conventionally becomes:

```javascript
function clamp(v, min, max) {
    return Math.max(
        min,
        Math.min(max, v)
    );
}
```

The behaviour is identical.

The previous Cognitive Labyrinth source contained roughly **2,399 physical lines**, whereas v4 is much more compressed.

However, the actual file sizes are relatively close:

```text
Previous version: ~84.9 KB
Version 4:        ~82.4 KB
```

So the smaller line count does **not** mean that most of the program disappeared.

The code is simply more densely formatted.

For development, a future prettified edition could expand the same v4 code back into several thousand easier-to-read lines without adding or removing functionality.

---

# Improvements Over the Previous Version

## Previous maze approach

The earlier version used cell values such as:

```text
wall
path
node
end
```

and could repair connectivity by drilling a Manhattan route toward a fixed destination.

Version 4 uses a more explicit graph-style maze representation and intrinsically connected generation.

---

## Previous storage approach

Earlier versions primarily stored one large JSON representation in:

```javascript
localStorage
```

Version 4 introduces more capable persistence through IndexedDB with fallback support.

---

## Previous coaching

The older Local Coach mainly relied on a small set of regular-expression categories.

Version 4 expands contextual analysis and prompt categories.

---

## Previous analytics

Earlier statistics largely focused on:

```text
Steps
Time
Nodes
Hints
```

Version 4 introduces substantially richer navigation and structural analytics.

---

## Previous timer

The old timer restarted around the current runtime session.

Version 4 can preserve accumulated elapsed time across restoration.

---

## Previous solution handling

The previous solution-overlay state could become inconsistent after movement.

Version 4 recalculates the route from the player's current position.

---

## Previous responsive scaling

Older versions used whole-document CSS scaling on desktop.

Version 4 uses a more conventional responsive layout strategy.

---

# Running Cognitive Labyrinth

No installation is required.

## Method 1 — Open the file

Open:

```text
cognitive_labyrinth_v4.html
```

in a modern browser.

---

## Method 2 — Local Web Server

Using Python:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000/cognitive_labyrinth_v4.html
```

---

## Method 3 — VS Code Live Server

Open the project in Visual Studio Code and run the HTML file using the Live Server extension.

---

# Browser Requirements

A recent browser is recommended.

Examples include:

- Google Chrome
- Microsoft Edge
- Firefox
- Safari

Some optional features depend on browser support for APIs such as:

- IndexedDB
- Web Audio API
- Vibration API
- Canvas
- Pointer events

Unsupported optional APIs are intended to degrade gracefully.

---

# Offline Operation

Most of Cognitive Labyrinth requires no internet connection.

Offline-capable systems include:

```text
Maze generation
Navigation
Solver
Hints
Fog
Trail
Journal
Local Coach
Analytics
History
Import
Export
Persistence
```

Only remote AI coaching requires a network connection.

---

# Data Privacy

When using Local Coach mode:

```text
Reflection data remains in the browser.
```

When using remote AI coaching:

```text
Reflection information submitted to the coach is sent to the configured proxy.
```

Users should understand and trust the proxy and AI service they configure before transmitting private information.

---

# Export Before Clearing Browser Data

Browser storage can be deleted by:

- Clearing site data
- Browser cleanup software
- Private/incognito browsing
- Browser profile deletion

Important journal sessions should therefore be exported periodically.

JSON export is recommended for complete backup.

Markdown export is recommended for long-term human-readable notes.

---

# Example Workflow

A typical session might look like this:

```text
1. Enter a goal.

2. Choose Project mode.

3. Generate a 20×20 maze.

4. Begin navigating.

5. Reach a reflection node.

6. Receive:
   "What is currently preventing progress?"

7. Write:
   "I keep changing the renderer before reproducing the original bug."

8. Local Coach identifies a debugging blocker.

9. Coach responds:
   Insight:
   The problem may be insufficient isolation rather than implementation complexity.

   Question:
   What is the smallest reproducible failing scene?

   Action:
   Spend 10 minutes creating that scene before modifying the renderer again.

   Implementation intention:
   If another rendering bug occurs, I will reproduce it in the smallest scene first.

10. Continue navigating.

11. Finish the maze.

12. Review:
    Steps
    Optimal route
    Efficiency
    Coverage
    Revisits
    Reflections

13. Export the journal.
```

---

# Design Goals

Cognitive Labyrinth is intended to remain:

- Experimental
- Lightweight
- Private by default
- Dependency-free
- Reproducible
- Extensible
- Accessible
- Usable offline
- Interesting as both a maze and reflective tool

---

# What Cognitive Labyrinth Is Not

Cognitive Labyrinth is not intended to be:

- Medical treatment
- Psychological diagnosis
- A substitute for professional mental-health support
- A validated cognitive assessment
- A clinical measurement instrument

Its analytics describe interaction with the application and should not be interpreted as clinical cognitive scores.

---

# Potential Research Uses

The deterministic maze and instrumentation architecture make the project potentially useful for experimentation around:

- Human navigation
- Maze topology
- Reflection timing
- Prompt design
- Self-regulated learning interfaces
- Procedural generation
- Human-computer interaction
- Behavioural telemetry
- Adaptive interfaces

Any formal research involving human participants would require appropriate experimental methodology, consent, privacy controls, and ethical review.

---

# Future Development

Potential future versions could investigate:

## Adaptive Difficulty

Automatically tune:

```text
Maze size
Loop density
Fog radius
Prompt frequency
Hint strength
```

according to previous performance.

---

## Spaced Reflection

Reintroduce previously important ideas after increasing intervals.

For example:

```text
Session 1 → immediate reflection
Session 2 → retrieval
Session 4 → transfer
Session 8 → long-term review
```

---

## Mastery Modelling

Track themes or skills across sessions rather than treating each reflection independently.

---

## Web Worker Maze Engine

Move expensive maze generation and analysis to a Web Worker for very large grids.

---

## Progressive Web App

Possible PWA capabilities:

- Installable application
- Offline caching
- Home-screen launch
- Versioned assets
- Update handling

---

## Local Language Model

A future Local Coach could optionally use a small on-device model through technologies such as:

- WebGPU
- WebNN
- ONNX Runtime Web
- WebAssembly

This would provide richer coaching while preserving local processing.

---

## Session Comparison

Future analytics could compare:

```text
Algorithm A vs Algorithm B

Fog vs no fog

Small vs large maze

Morning vs evening session

Hint-assisted vs independent runs
```

---

## Replay

Store movement events and reconstruct a completed run visually.

---

## Heatmaps

Render frequently visited regions to show:

- Backtracking
- Exploration
- Decision points
- Navigation difficulty

---

## Event-Based State Architecture

Future versions could store gameplay as events:

```text
RUN_STARTED
MOVED
HIT_WALL
NODE_REACHED
REFLECTION_SUBMITTED
HINT_USED
UNDO
FINISHED
```

This would enable deterministic replay and richer analysis.

---

# Development Philosophy

A key goal of version 4 was not simply adding more code.

The focus was instead on improving:

```text
Architecture
Correctness
Capabilities
Robustness
Security
Accessibility
Research grounding
Extensibility
```

A shorter implementation can still contain more functionality when duplicated or inefficient logic is replaced with stronger abstractions.

Therefore:

```text
Lines of code ≠ feature count
Lines of code ≠ quality
Lines of code ≠ complexity
```

Useful measures are instead:

- Correct behaviour
- Testability
- Maintainability
- Performance
- User experience
- Reliability
- Feature coverage

---

# Project Structure

The current edition intentionally remains simple:

```text
Cognitive-Labyrinth/
│
├── cognitive_labyrinth_v4.html
└── README.md
```

The HTML file contains:

```text
HTML
CSS
JavaScript
```

in a single portable application.

---

# Technology

Cognitive Labyrinth v4 uses standard browser technologies:

```text
HTML5
CSS3
JavaScript
Canvas API
IndexedDB
localStorage
Web Audio API
Pointer Events
URLSearchParams
Fetch API
```

No JavaScript framework is required.

No package manager is required.

No build pipeline is required.

---

# Why Single-File?

Keeping Cognitive Labyrinth as a single file provides several advantages:

- Easy distribution
- Easy backup
- Easy GitHub Pages deployment
- No dependency installation
- Simple experimentation
- Works locally
- Easy version snapshots
- Minimal hosting requirements

The architecture can still be split into modules later if the project becomes sufficiently large.

---

# Project Status

**Version:** 4.x  
**Architecture:** Single-file browser application  
**Primary language:** JavaScript  
**UI:** HTML + CSS  
**Dependencies:** None required  
**Offline mode:** Yes  
**Remote AI:** Optional  
**Persistent storage:** IndexedDB with fallback  
**Maze generation:** Procedural and deterministic  
**Reflection system:** Adaptive  
**Analytics:** Integrated  

---

# Summary

Cognitive Labyrinth v4 transforms the project from a procedural maze with reflection prompts into a more complete experimental cognitive-workflow platform.

It now combines:

```text
Procedural Generation
+
Navigation
+
Reflection
+
Self-Regulated Learning Concepts
+
Offline Coaching
+
Optional AI Coaching
+
Journaling
+
Persistence
+
Behavioural Analytics
+
Accessibility
+
Reproducibility
```

while remaining a portable browser application that can run from a single HTML file.

The central idea remains simple:

> Navigate the maze, encounter a problem, reflect on it, convert the reflection into an action, and continue.