# Decision Log: Key Architectural Decisions

## Core Architecture Decisions

### Decision 1: React Class Component for App
**Date**: 2020 Q1 | **Status**: ✅ Active | **Impact**: High

**Decision**: Use React Class Component instead of functional component for main App
**Rationale**:
- Lifecycle hooks needed (componentDidMount, componentDidUpdate, componentWillUnmount)
- Performance control via shouldComponentUpdate
- Easier to manage 100+ state properties
- Established patterns at the time

**Alternatives Considered**:
- Functional component + hooks: Too new at the time, hooks still evolving
- Redux: Over-engineered for drawing app needs

**Trade-offs**:
- ✅ Full lifecycle control
- ✅ Performance optimization
- ✅ Centralized state management
- ❌ Class component patterns less popular now
- ❌ Not compatible with newer React features

**Revisit Status**: Considered in React 19 upgrade but kept for stability

---

### Decision 2: Jotai for UI-Specific State
**Date**: 2023 Q2 | **Status**: ✅ Active | **Impact**: Medium

**Decision**: Adopt Jotai for UI toggles (dialogs, sidebars, menus) instead of AppState
**Rationale**:
- Lightweight primitive atoms
- Automatic subscription optimization
- Cleaner than Context API props drilling
- Smaller bundle than Redux/Zustand

**Alternatives Considered**:
- Keep everything in AppState: Would clutter state tree
- Redux: Too heavyweight for UI toggles
- MobX: Implicit reactivity concerns
- Zustand: Good but Jotai atoms more granular

**Trade-offs**:
- ✅ Fine-grained subscriptions
- ✅ Simple API (atoms)
- ✅ Small bundle impact (+15KB)
- ❌ Dual state management complexity
- ❌ Learning curve for new developers

**Current Status**: Hybrid approach working well

---

### Decision 3: Socket.io for Real-time Collaboration
**Date**: 2021 Q1 | **Status**: ✅ Active | **Impact**: Very High

**Decision**: Use Socket.io for real-time sync instead of WebRTC P2P
**Rationale**:
- Server provides single source of truth
- Easier conflict resolution (last-write-wins initially)
- Fallback to polling for unreliable connections
- Mature ecosystem with good documentation

**Alternatives Considered**:
- WebRTC: P2P complexity, NAT traversal issues
- WebSockets raw: No fallback, less mature
- Server-Sent Events: Unidirectional
- CRDT libraries: Overkill for drawing operations

**Trade-offs**:
- ✅ Reliable delivery
- ✅ Built-in reconnection
- ✅ Server-side conflict handling
- ❌ Server infrastructure cost
- ❌ Latency for geographically distant users
- ❌ Potential bottleneck at scale

**Revisit Status**: Working well, considering CDNs for latency reduction

---

### Decision 4: Firebase for Cloud Persistence
**Date**: 2021 Q2 | **Status**: ✅ Active | **Impact**: High

**Decision**: Use Firebase (Firestore + Storage) instead of custom backend
**Rationale**:
- Zero backend maintenance
- Real-time Firestore listeners
- Built-in authentication
- Global CDN for storage
- Generous free tier for experimentation

**Alternatives Considered**:
- Custom Node.js backend: DevOps overhead
- Supabase: Good but Postgres less ideal for JSON docs
- MongoDB Atlas: Requires backend code
- DynamoDB: AWS-only, more complex

**Trade-offs**:
- ✅ No backend to maintain
- ✅ Global infrastructure
- ✅ Real-time listeners built-in
- ✅ Easy to scale
- ❌ Vendor lock-in
- ❌ Billing complexity
- ❌ Limited query flexibility

**Revisit Status**: Considering multi-cloud support for resilience

---

### Decision 5: AppStateObserver Pattern for Subscriptions
**Date**: 2023 Q4 | **Status**: ✅ Active | **Impact**: Medium

**Decision**: Custom observer pattern instead of Redux selectors or MobX
**Rationale**:
- Precise subscription control (single property, arrays, selectors)
- Supports both callback and Promise patterns
- Lightweight implementation
- Works with class component state

**Alternatives Considered**:
- Redux selectors: Required Redux refactor
- MobX observers: Implicit reactivity
- RxJS: Heavy for simple use case
- React Query: Designed for server state

**Trade-offs**:
- ✅ Flexible subscription patterns
- ✅ Low overhead
- ✅ Works with current architecture
- ❌ Custom implementation (maintenance)
- ❌ Not as mature as Redux/Zustand
- ❌ Learning curve for external developers

**Current Status**: Core API feature, working well

---

### Decision 6: Canvas-based Rendering (vs SVG)
**Date**: 2020 Q1 | **Status**: ✅ Active | **Impact**: Very High

**Decision**: Use HTML5 Canvas for all rendering instead of SVG
**Rationale**:
- Better performance for interactive drawing
- Smoother freehand curves
- Hand-drawn effects via RoughJS
- Better mobile performance

**Alternatives Considered**:
- SVG: Better for precision, worse for performance
- WebGL: Over-engineered initially
- Hybrid: Complexity not worth trade-offs

**Trade-offs**:
- ✅ Excellent performance
- ✅ Smooth drawing experience
- ✅ Mobile-friendly
- ❌ Export complexity (need canvas-to-image pipelines)
- ❌ Accessibility challenges
- ❌ No built-in text selection

**Current Status**: Core decision, no plans to change

---

### Decision 7: Monorepo Structure with Yarn Workspaces
**Date**: 2020 Q2 | **Status**: ✅ Active | **Impact**: High

**Decision**: Split into monorepo with packages instead of single repo
**Rationale**:
- Separate embeddable library from app
- Shared utilities (@excalidraw/common, @excalidraw/element, @excalidraw/math)
- Independent versioning and releases
- Examples co-located with source

**Alternatives Considered**:
- Single repo: Hard to separate library concerns
- Separate repos: Version synchronization pain
- Turborepo: Not mature enough at the time

**Trade-offs**:
- ✅ Clear package boundaries
- ✅ Independent releases
- ✅ Library consumers get only what they need
- ✅ Examples stay up-to-date
- ❌ More complex setup
- ❌ Build system complexity
- ❌ Cross-package testing

**Current Status**: Working well, considering Turborepo for performance

---

### Decision 8: Vite Over Webpack (2024)
**Date**: 2024 Q1 | **Status**: ✅ Active | **Impact**: High

**Decision**: Migrate from Webpack to Vite for development and production
**Rationale**:
- 10x faster dev server startup
- Instant HMR (hot module replacement)
- Native ESM in dev
- Simpler configuration
- Better production builds

**Alternatives Considered**:
- Keep Webpack: Maintenance burden
- Parcel: Good but less mature
- Rollup: Would still need wrapper
- esbuild directly: Less integration

**Trade-offs**:
- ✅ Dramatically faster iteration
- ✅ Simpler build config
- ✅ Better error messages
- ✅ Active community
- ❌ Newer technology (less battle-tested)
- ❌ Some plugins still maturing

**Current Status**: Smooth migration, very successful

---

### Decision 9: TypeScript Strict Mode
**Date**: 2022 Q1 | **Status**: ✅ Active | **Impact**: Medium-High

**Decision**: Enable TypeScript strict mode for type safety
**Rationale**:
- Catch type errors at compile time
- Better refactoring safety
- Improved IDE support
- Documentation via types

**Alternatives Considered**:
- Loose mode: Less safety
- Flow: Different tooling

**Trade-offs**:
- ✅ Fewer runtime errors
- ✅ Better refactoring
- ✅ Self-documenting code
- ❌ Initial migration effort
- ❌ More verbose in some cases
- ❌ Strictness learning curve

**Current Status**: 95% of codebase in strict mode

---

### Decision 10: Custom AppState over Redux/Zustand
**Date**: 2020 Q1 | **Status**: ✅ Active (Evolving) | **Impact**: Very High

**Decision**: Custom AppState pattern instead of established state management
**Rationale**:
- Minimal boilerplate
- Tight coupling with domain (perfect for App)
- Easier to understand than Redux actions
- Smaller bundle than Redux

**Alternatives Considered**:
- Redux: Overkill for single app
- Zustand: Good but emerged later
- MobX: Less predictable
- Recoil: Facebook-specific

**Trade-offs**:
- ✅ Minimal overhead
- ✅ Domain-specific
- ✅ Easy to add AppStateObserver later
- ❌ Not as battle-tested
- ❌ Custom implementation maintenance
- ❌ Harder for external developers to understand

**Current Status**: Working well, being enhanced with Jotai for UI state

---

## Integration Decisions

### Decision 11: AI Integration via API (not local)
**Date**: 2023 Q2 | **Status**: ✅ Active | **Impact**: Medium

**Decision**: Server-side AI models instead of running models in browser
**Rationale**:
- Smaller bundle size
- Can use more powerful models
- Easier to swap providers
- Better cost control

**Trade-offs**:
- ✅ Smaller bundle
- ✅ Better model quality
- ✅ Easy provider switching
- ❌ Privacy concerns (data sent to server)
- ❌ Requires server infrastructure
- ❌ Latency for responses

**Current Status**: Working with OpenAI, Claude APIs

---

### Decision 12: Immutable Elements Pattern
**Date**: 2020 Q2 | **Status**: ✅ Active | **Impact**: High

**Decision**: Elements are immutable, mutations create new objects
**Rationale**:
- Easier to track changes for undo/redo
- Better performance with React
- Thread-safe for future worker threads
- Simpler to reason about state

**Implementation**:
```typescript
// Instead of: element.x = 100
// Use: mutateElement(element, {x: 100})
// Which returns: newElement with x: 100
```

**Trade-offs**:
- ✅ Predictable state changes
- ✅ Good for undo/redo
- ✅ React performance friendly
- ❌ Memory overhead
- ❌ More verbose code

**Current Status**: Core to architecture, no plans to change

---

## UX Decisions

### Decision 13: Whiteboard-Style Default Look
**Date**: 2020 Q1 | **Status**: ✅ Active | **Impact**: Very High

**Decision**: Hand-drawn style via RoughJS as default
**Rationale**:
- Lower friction perception (sketching)
- Unique brand identity
- Differentiates from Figma/traditional tools

**Trade-offs**:
- ✅ Unique positioning
- ✅ Draws users to simplicity
- ❌ Can't export as precise as Figma
- ❌ Not suitable for technical drawings initially

**Current Status**: Core brand identity, options for precise mode added

---

### Decision 14: No Native App, Web-First
**Date**: 2020 Q1 | **Status**: ✅ Active | **Impact**: High

**Decision**: Web-only strategy instead of Electron/native apps
**Rationale**:
- Faster iteration
- Automatic updates
- Platform independence
- Lower maintenance

**Alternatives Considered**:
- Electron desktop app: Maintenance overhead
- Native apps: Different codebases
- Progressive Web App: As enhancement

**Trade-offs**:
- ✅ One codebase
- ✅ No app store friction
- ✅ Always up-to-date
- ❌ Performance vs native
- ❌ Offline limitations (mitigated with PWA)

**Current Status**: PWA improvements planned, native apps possible via third parties

---

## Roadmap Decisions (Future)

### Planned Decision: Plugin System
**Timeline**: 2025 Q2-Q3 | **Status**: 🔵 Planning

**Proposal**: Extensible plugin architecture for domain-specific tools
**Considerations**:
- Security model for plugins
- API stability guarantees
- Package discovery and distribution
- Plugin marketplace

---

### Planned Decision: Multi-Provider Backend
**Timeline**: 2025 Q3-Q4 | **Status**: 🔵 Planning

**Proposal**: Support for alternative backends (Firebase, AWS, custom)
**Benefits**:
- Reduce vendor lock-in
- Regional data residency
- Self-hosted option

---

## 🔗 Related Documentation

**Reference these for context:**
- **Technical Implementation**: See [`docs/technical/architecture.md`](../technical/architecture.md) for how decisions are implemented
- **Tech Stack**: See [`techContext.md`](techContext.md) for technology choices made
- **System Patterns**: See [`systemPatterns.md`](systemPatterns.md) for architectural patterns resulting from decisions
- **Product Requirements**: See [`docs/product/PRD.md`](../product/PRD.md) for feature requirements tied to decisions
- **Project Progress**: See [`progress.md`](progress.md) for how decisions have evolved over time
- **Developer Setup**: See [`docs/technical/dev-setup.md`](../technical/dev-setup.md) for implementation guidance
3. **Prototype**: Small proof-of-concept
4. **Decision**: Core team approval
5. **Implementation**: Gradual rollout
6. **Monitor**: Metrics and feedback
7. **Review**: Quarterly assessment

### Recent Decision Reviews (2025)
- ✅ Vite migration: Successful, keeping long-term
- ✅ React 19: Good, monitoring for issues
- 🔍 Jotai vs custom atoms: Evaluating for next phase
- 🔍 Firebase scaling: Assessing for growth
