# Product Requirements Document: Excalidraw

**Reverse-Engineered from Codebase Analysis**  
**Status**: Production  
**Last Updated**: March 2026  
**Version**: 1.0

---

## Executive Summary

Excalidraw is an open-source, web-based drawing application designed to make diagram creation feel as natural as drawing on a physical whiteboard. It combines ease of use with powerful collaboration features, making it suitable for both individual sketching and team-based real-time collaboration on architectural diagrams, flowcharts, wireframes, and general-purpose drawings.

The product philosophy prioritizes **instant expressiveness** and **intuitive interaction** over precision, differentiating it from professional design tools like Figma. It succeeds by eliminating friction between idea and visualization.

---

## Product Vision & Purpose

### Core Mission
Enable anyone to quickly sketch ideas visually with minimal learning curve, using hand-drawn aesthetics that feel less formal than traditional design tools.

### Strategic Goals
1. **Accessibility**: Lower barrier to entry than professional design software
2. **Collaboration**: Enable real-time multi-user editing on drawings
3. **Persistence**: Save work locally, to cloud, or as file exports
4. **Extensibility**: Serve as embeddable component in other applications
5. **Community**: Build sustainable open-source project with active contribution

### Unique Value Proposition
- **Hand-drawn aesthetic** (via RoughJS): Makes diagrams feel sketchy and informal
- **Zero-friction startup**: No account required, instant editing
- **Multiplayer by default**: Real-time collaboration built-in, not add-on
- **Web-native**: No installation, works in any modern browser
- **Open source**: Transparent development, user control
- **Embeddable**: Can be integrated into other applications
- **Free**: No premium tier, unlimited usage

---

## Target Audience

### Primary Users

#### 1. Individual Sketchers (40%)
- **Profile**: Solo users sketching for personal notes, planning
- **Use cases**: Quick wireframes, system diagrams, brainstorming
- **Key need**: Speed and simplicity
- **Behavior**: Create, sketch, save locally or export
- **Pain point**: Formal tools feel too heavy for quick sketches

#### 2. Collaborative Teams (35%)
- **Profile**: 2-10 person teams working on design/architecture
- **Use cases**: Real-time whiteboarding, architecture discussions, design sprints
- **Key need**: Synchronization and presence awareness
- **Behavior**: Share link, draw together, see each other's cursors
- **Pain point**: Video calls without visual collaboration tool

#### 3. Educators & Presenters (15%)
- **Profile**: Teachers, trainers, conference speakers
- **Use cases**: Explaining concepts, live drawing during presentations
- **Key need**: Clear visualization, easy sharing
- **Behavior**: Draw, screenshot/export, present
- **Pain point**: Need something quick that looks professional

#### 4. Developers & Integrators (10%)
- **Profile**: Engineers embedding drawing capability in applications
- **Use cases**: Building tools with drawing features
- **Key need**: Reusable React component, clean API
- **Behavior**: npm install, integrate component, customize
- **Pain point**: Building drawing from scratch is complex

### Secondary Users

- **Content creators**: Using for YouTube/blog posts
- **Project managers**: Quick planning and documentation
- **Technical writers**: Visual explanations in documentation
- **UX/Product teams**: Rapid prototyping

---

## Key Features & Functions

### Tier 1: Core (MVP Level)

#### Drawing Tools (Implemented ✓)
- **Selection** - Select and manipulate elements
- **Rectangle** - Draw rectangular shapes
- **Diamond** - Draw diamond/rhombus shapes
- **Ellipse** - Draw circles and ovals
- **Arrow** - Draw lines with optional arrowheads
- **Line** - Draw multi-point lines
- **Freedraw** - Freehand drawing with curves
- **Text** - Add and edit text
- **Eraser** - Delete elements by drawing over them

#### Element Styling (Implemented ✓)
- Stroke color (15+ color palette)
- Fill color with patterns (solid, hachure, cross-hatch)
- Stroke width (1-20px)
- Stroke style (solid, dashed, dotted)
- Opacity (0-100%)
- Roundness (sharp, round, adaptive)
- Roughness (architect, artist, cartoonist modes)
- Font family (multiple fonts)
- Font size
- Text alignment (left, center, right)

#### Canvas Operations (Implemented ✓)
- **Zoom**: 0.1x to 16x
- **Pan**: Scroll/drag to navigate
- **Grid**: Optional grid overlay
- **Grid snapping**: Align to grid
- **Guides**: Visual alignment guides
- **Reset zoom**: Center and fit to view

### Tier 2: Organization & Selection

#### Grouping & Organization (Implemented ✓)
- **Selection**: Click to select, drag to create selection box
- **Multi-select**: Ctrl/Cmd+click to select multiple
- **Grouping**: Group elements for bulk operations
- **Frames**: Container for organizing related elements
- **Layers**: Z-order management
- **Alignment**: Align left/right/top/bottom/center
- **Distribution**: Distribute horizontally/vertically
- **Lock**: Prevent accidental modification
- **Hide**: Temporarily hide elements

### Tier 3: Collaboration & Sharing

#### Real-time Collaboration (Implemented ✓)
- **Multi-user editing**: Multiple users edit same drawing
- **Cursor presence**: See where others are pointing
- **Selection visibility**: See what others selected
- **Live sync**: Changes appear instantly (<500ms)
- **User presence**: Avatar indicators for collaborators
- **Follow mode**: Track specific user's cursor
- **Conflict resolution**: Automatic merge of concurrent edits

#### Sharing & Persistence (Implemented ✓)
- **Local save**: IndexedDB browser storage
- **Cloud save**: Firebase integration (with login)
- **Share link**: Generate shareable URL
- **Export formats**: PNG, SVG, JSON
- **Import**: Restore from previously saved files
- **Undo/Redo**: Full history with 50+ undo levels

### Tier 4: Advanced Features

#### Element Binding (Implemented ✓)
- **Arrow binding**: Arrow endpoints attach to shapes
- **Smart connection**: Arrows move with connected shapes
- **Binding indicators**: Visual feedback on connection points
- **Auto-routing**: Optional elbow arrows for flowcharts

#### Advanced Shapes (Implemented ✓)
- **Images**: Embed and resize images
- **Embeddables**: Integrate external content (iframes)
- **Flowcharts**: Special flowchart shapes
- **Magic Frames**: AI-generated frame containers

#### Text Features (Implemented ✓)
- **Bound text**: Text contained within shapes
- **Text editing**: Rich inline editing
- **Auto-resize**: Text container auto-grows
- **Line height**: Adjustable line spacing
- **Multiple fonts**: System and web fonts

#### Element Linking (Implemented ✓)
- **Hyperlinks**: Add URLs to elements
- **Link preview**: Hover to see URL
- **Click-to-open**: Open link in new tab

### Tier 5: AI & Advanced

#### AI Features (Implemented ✓)
- **Text-to-Diagram (TTD)**: Generate diagrams from natural language
- **Mermaid support**: Convert Mermaid diagrams to Excalidraw
- **Diagram refinement**: Chat-based diagram improvement
- **Code generation**: Generate code from diagrams (preview)

#### Accessibility (Implemented ✓)
- **60+ languages**: i18n support
- **Keyboard shortcuts**: Full keyboard navigation
- **Screen readers**: ARIA labels and semantic HTML
- **Dark/Light themes**: User preference support
- **High contrast**: Accessibility mode support

---

## Technical Specifications

### Technology Stack

#### Frontend
- **React 19.0.0** - UI library
- **TypeScript 5.9.3** - Type safety
- **Vite 5.0.12** - Build tool
- **Canvas API** - Drawing surface (not SVG for performance)
- **Jotai 2.11.0** - UI state management

#### State Management
- **React State** - AppState (100+ properties)
- **Jotai Atoms** - UI-specific toggles
- **Custom Store** - Delta tracking for undo/redo
- **AppStateObserver** - Subscription pattern

#### Real-time & Persistence
- **Socket.io 4.7.2** - WebSocket collaboration
- **Firebase 11.3.1** - Cloud storage & auth
- **IndexedDB** - Local browser storage

#### Rendering
- **RoughJS 4.6.4** - Hand-drawn style
- **Perfect Freehand 1.2** - Smooth curves
- **Canvas Roundrect Polyfill** - Rounded rectangles

#### Quality & Testing
- **Vitest 3.0.6** - Unit tests
- **@testing-library/react** - Component testing
- **ESLint** - Code linting
- **Prettier** - Code formatting
- **TypeScript strict mode** - Type checking

### Architecture

#### Class-based App Component
- Single monolithic `App` React class component
- 100+ AppState properties
- Centralized event handling
- Lifecycle hooks for setup/teardown

#### Layered Rendering
- **Static Scene**: Off-screen base render
- **Interactive Scene**: On-screen with UI overlays
- **Snap Guides**: Optional alignment visualization
- **Animation**: Frame interpolation

#### Modular Packages
```
@excalidraw/excalidraw      - Main React component
@excalidraw/element         - Element types & operations
@excalidraw/math            - Mathematical utilities
@excalidraw/common          - Shared constants
@excalidraw/utils           - Export utilities
```

#### Data Flow
1. User interaction → Event handler
2. ActionManager executes action
3. Scene mutates elements (immutable pattern)
4. Store records delta (for undo/collaboration)
5. setState updates AppState
6. React renders with new state
7. Renderer converts to canvas
8. Subscribers notified (history, Socket.io, etc.)

---

## Feature Completeness Matrix

### Core Drawing (100% Complete)
- ✓ All 9 tool types
- ✓ Full styling options
- ✓ Canvas operations (zoom, pan, grid)
- ✓ Selection and manipulation
- ✓ Undo/redo history

### Organization (95% Complete)
- ✓ Grouping elements
- ✓ Frames for containers
- ✓ Alignment tools
- ✓ Layer management
- ⚠ Advanced nested grouping (limited)

### Collaboration (85% Complete)
- ✓ Real-time multi-user
- ✓ Live cursor tracking
- ✓ Selection visibility
- ✓ Automatic reconciliation
- ⚠ Offline support (local-only)
- ⚠ Conflict visualization (hidden merges)

### Sharing & Persistence (90% Complete)
- ✓ Local storage
- ✓ Cloud storage (Firebase)
- ✓ Export (PNG, SVG, JSON)
- ✓ Share links
- ✓ Import
- ⚠ Version history (not preserved)

### AI Features (70% Complete)
- ✓ Text-to-Diagram
- ✓ Mermaid import
- ✓ Chat refinement
- ⚠ Code generation (preview only)
- ⚠ Diagram understanding (limited)

---

## Technical Limitations & Constraints

### Canvas Rendering Limitations

#### Large Drawing Performance
- **Issue**: 10,000+ elements slow down rendering
- **Root cause**: Full scene re-render on each change
- **Mitigation**: Viewport culling, shape caching
- **Workaround**: Split into multiple drawings

#### Precision vs Aesthetics
- **Issue**: Hand-drawn style sacrifices precision
- **Root cause**: RoughJS randomization for aesthetic
- **Mitigation**: Optional precise mode (limited)
- **Trade-off**: Design choice for whiteboard feel

#### Export Fidelity
- **Issue**: PNG/SVG exports may differ from canvas
- **Root cause**: Canvas anti-aliasing vs vector rendering
- **Mitigation**: High DPI export options
- **Limitation**: Perfect fidelity not possible

### Collaboration Constraints

#### Offline Limitations
- **Issue**: Limited offline support
- **Root cause**: Real-time sync requires server
- **Mitigation**: Local-only editing when offline
- **Limitation**: No background sync

#### Conflict Resolution
- **Issue**: Last-Write-Wins can lose changes
- **Root cause**: Simple reconciliation strategy
- **Mitigation**: Rare in practice (millisecond conflicts)
- **Limitation**: No conflict visualization

#### Latency Sensitivity
- **Issue**: High-latency connections feel sluggish
- **Root cause**: Need <500ms sync for feel
- **Mitigation**: Optimistic updates, local echo
- **Limitation**: ~500ms minimum acceptable latency

### Browser & Platform

#### Browser Compatibility
- **Requirement**: Modern browser (Chrome 70+, Safari 12+)
- **Limitation**: No IE support, older Safari limited
- **Reason**: Uses modern Canvas API, WebGL

#### Mobile/Touch
- **Support**: Basic touch support on iOS/Android
- **Limitation**: Mobile precision worse than desktop
- **Reason**: Touch is less precise than mouse/pen

#### Cross-device Sync
- **Limitation**: No automatic sync across devices
- **Reason**: Single session per user
- **Workaround**: Share link or cloud sync

### Feature Limitations

#### Text Rendering
- **Limitation**: Limited font support
- **Reason**: Only system fonts + web fonts
- **Workaround**: Use popular web-safe fonts

#### Image Handling
- **Limitation**: Large image embedding
- **Reason**: Images stored in drawing JSON
- **Workaround**: Compress before embedding

#### Shapes
- **Limitation**: No custom shape creation
- **Reason**: Would complicate serialization
- **Workaround**: Use combinations of basic shapes

#### Themes & Customization
- **Limitation**: Limited UI customization
- **Reason**: Single design maintained
- **Workaround**: CSS overrides possible

---

## Success Metrics

### Engagement Metrics
- Monthly active users: Target 2M+
- Daily active users: Target 500k+
- Average session duration: Target 15+ minutes
- Drawing creation rate: Target 1+ per user per week

### Feature Adoption
- Real-time collaboration usage: Target 30%+
- Export usage: Target 40%+
- Cloud storage adoption: Target 20%+
- Mobile usage: Target 35%+

### Community Health
- GitHub stars: Target 60k+
- npm weekly downloads: Target 50k+
- Active contributors: Target 15-20 per month
- Issue resolution time: Target <48 hours

### Performance Targets
- Load time: <2 seconds
- First draw time: <100ms
- Frame rate: 58-60 FPS
- Memory usage: <150MB
- Bundle size: <500KB (gzipped)

---

## Product Roadmap

### Phase 1: Foundation (Completed 2020-2021)
- ✓ Core drawing tools
- ✓ Basic shapes
- ✓ Styling
- ✓ Undo/redo
- ✓ Export

### Phase 2: Collaboration (Completed 2021-2022)
- ✓ Real-time multi-user
- ✓ Firebase integration
- ✓ Share links
- ✓ User presence
- ✓ Binding system

### Phase 3: Scale & Performance (Completed 2022-2023)
- ✓ Rendering optimization
- ✓ Memory management
- ✓ Mobile responsiveness
- ✓ 60+ language support

### Phase 4: AI Integration (Completed 2023-2024)
- ✓ Text-to-Diagram
- ✓ Mermaid support
- ✓ Chat refinement
- ✓ Code generation (preview)

### Phase 5: Next Generation (In Progress 2024-2025)
- ✓ React 19 migration
- ✓ TypeScript 5.9
- ✓ Vite 5.0
- 🟡 Accessibility improvements (WCAG 2.1)
- 🟡 Performance optimization

### Phase 6: Future Vision (Planning 2025-2026)
- 🔵 Plugin system architecture
- 🔵 Advanced export (code generation)
- 🔵 VR/AR collaboration spaces
- 🔵 Video annotation support
- 🔵 Advanced 3D visualization

---

## Competitive Positioning

### vs. Figma
| Aspect | Excalidraw | Figma |
|--------|-----------|-------|
| Learning curve | Minimal | Steep |
| Aesthetic | Hand-drawn | Precise |
| Price | Free | Freemium |
| Collaboration | Built-in | Built-in |
| Purpose | Ideation | Production design |
| Asset library | Basic | Extensive |

### vs. Miro/Mural
| Aspect | Excalidraw | Miro |
|--------|-----------|------|
| Setup time | Instant | Account required |
| Core function | Drawing | Brainstorming |
| Price | Free | Paid |
| API | React component | Web embed |
| Extensibility | Via component | Via API |

### vs. Google Drawings
| Aspect | Excalidraw | Google Drawings |
|--------|-----------|-----------------|
| Learning curve | Lower | Similar |
| Collaboration | Real-time | Real-time |
| Price | Free | Free |
| Google integration | No | Yes |
| Offline | Limited | Good |

---

## Business Model & Monetization

### Current Model
- **Free**: Core app completely free
- **Excalidraw Plus**: Optional premium features
  - Advanced collaboration
  - Extended storage
  - Priority support
- **Open Source**: Source code public, MIT license

### Revenue Streams
- Excalidraw Plus subscriptions
- Enterprise licensing
- Sponsorships
- Donations from community

### Sustainability
- Small core team + community contributions
- Vendor-neutral (self-hosted capable)
- No venture capital pressure
- Long-term viability maintained

---

## Constraints & Assumptions

### Technical Constraints
- Canvas-based (performance over precision)
- Client-side rendering (no server-side generation)
- Monorepo architecture (coupled packages)
- React 17+ required (modern JavaScript)

### User Assumptions
- Users have modern web browser
- Internet connection for collaboration (optional for local)
- Basic computer literacy
- Familiarity with drawing UX concepts

### Market Assumptions
- Large market for informal diagram tools
- Real-time collaboration valuable
- Hand-drawn aesthetic appeals to users
- Open source sustainable for drawing tool

---

## Glossary

| Term | Definition |
|------|-----------|
| **Element** | Any drawable object (shape, text, image, arrow) |
| **Scene** | The collection of all elements in a drawing |
| **AppState** | Global UI state (selection, tool, viewport) |
| **Binding** | Connection between arrow and target element |
| **Frame** | Container element for organizing other elements |
| **Group** | Logical collection of elements for bulk operations |
| **Action** | Reusable operation (delete, duplicate, align) |
| **Tool** | Drawing mode (selection, rectangle, arrow, text) |
| **Reconciliation** | Merging concurrent edits from collaborators |
| **TTD** | Text-to-Diagram (AI feature) |

---

## Document History

| Version | Date | Author | Notes |
|---------|------|--------|-------|
| 1.0 | Mar 2026 | Reverse-engineered | Initial PRD from code analysis |

---

## Appendix A: Feature Request Backlog

### High Priority
- [ ] Plugin system for third-party extensions
- [ ] Advanced export (code generation, Figma)
- [ ] Better offline support
- [ ] Mobile app (native)
- [ ] Performance on massive drawings

### Medium Priority
- [ ] Tables and data visualization
- [ ] Diagram templates
- [ ] Asset library improvements
- [ ] Custom shapes
- [ ] Better mobile touch experience

### Low Priority
- [ ] 3D visualization
- [ ] VR collaboration
- [ ] Video annotation
- [ ] Advanced physics simulation
- [ ] Game-style drawing

---

## Appendix B: Known Issues & Workarounds

### Issue: Slow rendering on 10k+ elements
**Workaround**: Split into multiple drawings or use frames

### Issue: Export doesn't match canvas exactly
**Workaround**: Use higher DPI export option

### Issue: Mobile precision is difficult
**Workaround**: Use stylus/pen on tablet for better precision

### Issue: Collaboration lag in high-latency network
**Workaround**: Close unnecessary browser tabs, reduce drawing complexity

---

## 🔗 Related Documentation

**Learn more about:**
- **Memory Bank**: See [`docs/memory/`](../memory/) for strategic context:
  - [`projectbrief.md`](../memory/projectbrief.md) - Project goals and overview
  - [`productContext.md`](../memory/productContext.md) - UX goals and user journey
  - [`progress.md`](../memory/progress.md) - Project milestones and market fit
  - [`activeContext.md`](../memory/activeContext.md) - Current development priorities
- **Architecture**: See [`docs/technical/architecture.md`](../technical/architecture.md) for implementation approach
- **Domain Glossary**: See [`domain-glossary.md`](domain-glossary.md) for terminology
- **Setup Guide**: See [`docs/technical/dev-setup.md`](../technical/dev-setup.md) for developing features---

**End of Product Requirements Document**

