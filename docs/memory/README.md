# Excalidraw Memory Bank

Complete project context and reference documentation for the Excalidraw drawing application.

## 📚 Files Overview

### 1. **projectbrief.md** (40 lines)
High-level project overview and business context
- What is Excalidraw?
- Main goals and features
- Architecture type (monorepo)
- Target users and success metrics

### 2. **techContext.md** (132 lines)
Technology stack and development setup
- Frontend framework (React 19, TypeScript 5.9, Vite 5)
- State management (Jotai, AppState, AppStateObserver)
- Real-time & persistence (Socket.io, Firebase)
- Build tools and dependencies
- Key commands for development

### 3. **systemPatterns.md** (217 lines)
Core architecture patterns and design principles
- Class component with centralized state
- Hybrid state management approach
- Full lifecycle stages (constructor → unmount)
- Event-driven architecture with multiple emitters
- Data flow patterns for rendering and actions
- Scene management and rendering layers
- Collaboration patterns
- Portal tunnel pattern for UI composition

### 4. **productContext.md** (202 lines)
UX goals and user experience philosophy
- 8 core UX goals (expressiveness, discoverability, collaboration, etc.)
- User journey stages (Discovery → Creation → Collaboration → Export)
- Interaction patterns (pointer, keyboard, touch)
- Success metrics for engagement and usability
- Visual design language and future roadmap

### 5. **activeContext.md** (180 lines)
Current development status and focus areas
- Current version (0.18.0) with latest stack
- 6 active development tracks (drawing, collaboration, UI, AI, performance, QA)
- Performance metrics and status
- Priority issues and bugs
- Test coverage by component
- Development workflow and release process

### 6. **progress.md** (270 lines)
Project milestones and historical context
- 6 major phases completed (Foundation → Next Generation)
- Feature completion timeline
- Community growth metrics (60k GitHub stars, 2M MAU)
- Technical debt status
- Performance improvements over time
- User feedback evolution
- Current pain points and lessons learned

### 7. **decisionLog.md** (355 lines)
Key architectural and strategic decisions with rationale
- 12 core decisions made with alternatives considered
- React class component for App state
- Jotai for UI-specific state
- Socket.io for real-time collaboration
- Firebase for cloud persistence
- Canvas-based rendering (vs SVG)
- Monorepo with Yarn workspaces
- Vite over Webpack
- And 5 more critical decisions
- Future decisions being planned

---

## 🎯 Quick Reference

### For Understanding the Project
**Read in order**: projectbrief.md → techContext.md → systemPatterns.md

### For Contributing
**Read**: activeContext.md → progress.md → decisionLog.md

### For Making Changes
**Reference**: systemPatterns.md + decisionLog.md

### For UX Work
**Focus**: productContext.md

---

## 📊 Content Statistics

| File | Lines | Size | Topics |
|------|-------|------|--------|
| projectbrief.md | 40 | 2.1 KB | Overview, goals, features |
| techContext.md | 132 | 4.7 KB | Stack, versions, commands |
| systemPatterns.md | 217 | 6.3 KB | Architecture, patterns, design |
| productContext.md | 202 | 5.8 KB | UX goals, interaction patterns |
| activeContext.md | 180 | 5.8 KB | Current focus, status, metrics |
| progress.md | 270 | 6.6 KB | Timeline, milestones, metrics |
| decisionLog.md | 355 | 12 KB | Decisions, rationale, trade-offs |
| **Total** | **1,396** | **43.1 KB** | **Complete reference** |

---

## 🔑 Key Takeaways

### Architecture
- **Class component** (App.tsx) with 100+ AppState properties
- **Hybrid state**: React state + Jotai atoms + AppStateObserver subscriptions
- **Event-driven**: 8+ emitters for different concerns
- **Scene-based**: Elements managed separately from UI state

### Stack
- **Frontend**: React 19, TypeScript 5.9, Vite 5
- **State**: Jotai 2.11, custom AppStateObserver
- **Real-time**: Socket.io 4.7, Firebase 11.3
- **Rendering**: Canvas via RoughJS for hand-drawn style

### Performance
- Startup: 1.5s (target 1.2s)
- Frame rate: 58 FPS (target 60)
- Bundle: 420 KB (target 350 KB)
- Memory: 120 MB (target 100 MB)

### Community
- GitHub: 60k stars, growing ~200/week
- Downloads: 50k+/week on npm
- Users: 2M monthly active, 500k daily active
- Contributors: 200+ with ~15-20 active per month

### Current Focus (2025-2026)
1. React 19 migration stabilization
2. Accessibility improvements (WCAG 2.1)
3. Performance optimization
4. Test coverage expansion (target 85%)
5. Mobile UX enhancements
6. AI features stabilization

---

## 🔗 Cross-Documentation Links

### Technical Deep Dives
- **System Architecture**: [`docs/technical/architecture.md`](../technical/architecture.md) - System design with Mermaid diagrams
- **Developer Setup**: [`docs/technical/dev-setup.md`](../technical/dev-setup.md) - Complete onboarding guide

### Product Knowledge
- **Product Requirements**: [`docs/product/PRD.md`](../product/PRD.md) - Complete PRD with features and roadmap
- **Domain Glossary**: [`docs/product/domain-glossary.md`](../product/domain-glossary.md) - 50+ term definitions

---

## 🚀 Getting Started

### Development
```bash
yarn install          # Install dependencies
yarn start            # Start dev server (http://localhost:5173)
yarn test             # Run tests
yarn test:code        # Lint and format check
yarn build            # Production build
```

**→ See [Developer Setup Guide](../technical/dev-setup.md) for detailed step-by-step instructions**

### Key Technologies
- **Drawing**: Perfect Freehand, RoughJS
- **State**: React, Jotai, AppStateObserver
- **UI**: Radix UI, SCSS
- **Building**: Vite, esbuild
- **Testing**: Vitest, @testing-library
- **Types**: TypeScript strict mode

**→ See [Technical Context](techContext.md) and [Architecture Guide](../technical/architecture.md) for details**

---

## 📖 References

- **GitHub**: https://github.com/excalidraw/excalidraw
- **Docs**: https://docs.excalidraw.com
- **Live App**: https://excalidraw.com
- **npm Package**: @excalidraw/excalidraw

---

## 🗺️ Documentation Map

```
Understanding Layer          Technical Layer          Product Layer
├── projectbrief.md    →    ├── architecture.md  ←   ├── PRD.md
├── techContext.md     →    └── dev-setup.md     ←   └── domain-glossary.md
├── systemPatterns.md
├── productContext.md
├── activeContext.md
├── progress.md
└── decisionLog.md
```

---

## 💡 Notes for Contributors

1. **Understand the patterns** before making changes (read systemPatterns.md)
2. **Check decisions** to understand why things are done a certain way
3. **Follow the precedent** - look at similar code before implementing
4. **Run tests** before committing - all checks must pass
5. **Reference activeContext.md** for current priorities

---

**Last Updated**: March 26, 2026
**Memory Bank Version**: 1.0
**Total Time Invested**: Complete codebase analysis + architectural documentation
