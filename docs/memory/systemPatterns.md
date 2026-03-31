# System Patterns: Excalidraw Architecture

## Core Architecture Patterns

### 1. Class Component with Centralized State
**Pattern**: React Class Component as state container
```
App (React.Component<AppProps, AppState>)
  └─ Manages 100+ AppState properties
  └─ Exposes setAppState() via Context
  └─ Triggers renders via setState()
```

**Why**: 
- Lifecycle hooks (componentDidMount, componentDidUpdate, componentWillUnmount)
- Performance: Memoization and selective updates
- Centralized event handling for complex interactions

**Key Class Properties**:
- `scene: Scene` - Element storage and management
- `renderer: Renderer` - Canvas rendering orchestration
- `actionManager: ActionManager` - UI action dispatch
- `history: History` - Undo/redo stack
- `api: ExcalidrawImperativeAPI` - Public API for embedders

### 2. Hybrid State Management
**Pattern**: Jotai atoms + React state + AppStateObserver
```
├─ React state (AppState) - Global UI state
├─ Jotai atoms - UI-specific toggles (sidebar, dialogs, etc)
└─ AppStateObserver - Reactive subscriptions
```

**Subscriptions**:
```typescript
api.onStateChange("selectedElementIds", (ids, appState) => {})
api.onStateChange(["zoom", "scrollX"], (appState) => {})
api.onStateChange((state) => state.zoom.value, (value) => {})
```

**Why**: 
- Multiple subscription patterns for flexibility
- Separates UI state from business logic
- Enables external consumers to react to specific changes

### 3. Lifecycle Stages

#### Constructor
- Initialize default AppState
- Create managers (ActionManager, Scene, History, Library)
- Register actions

#### componentDidMount
- Setup event listeners (keyboard, pointer, wheel, touch)
- Setup ResizeObserver for responsive updates
- Subscribe to store increments for history
- Emit `editor:mount` event
- Initialize scene and restore data

#### componentDidUpdate
- Flush AppStateObserver subscriptions
- Sync props to state (theme, language, view mode)
- Emit change events (scroll, zoom, collaboration)
- Handle tool/mode transitions

#### componentWillUnmount
- Invalidate API (mark as destroyed)
- Destroy renderer and scene
- Clear all emitters and listeners
- Clear caches (ShapeCache, SnapCache)
- Stop animation trails

### 4. Event-Driven Architecture
**Multiple Emitters**:
```
onChangeEmitter           → (elements, appState, files)
onPointerDownEmitter      → (tool, pointerState, event)
onPointerUpEmitter        → (tool, pointerState, event)
onScrollChangeEmitter     → (scrollX, scrollY, zoom)
onUserFollowEmitter       → (userToFollow, action)
missingPointerEventCleanupEmitter
editorLifecycleEvents     → (mount, unmount, initialize)
```

### 5. Data Flow Patterns

#### Rendering Pipeline
```
setState() or triggerRender()
  ↓
render() method executes
  ↓
getRenderableElements() calculates visible elements
  ↓
LayerUI renders with updated context
  ↓
componentDidUpdate() flushes subscriptions
  ↓
Emitters trigger callbacks
```

#### Action Flow
```
User interaction (keyboard, pointer, menu)
  ↓
Handler calls action via ActionManager
  ↓
Action mutates Scene or AppState
  ↓
Store emits increment
  ↓
History records change
  ↓
triggerRender() forces update
  ↓
Components re-render
```

### 6. Context Provider Hierarchy
```
ExcalidrawAPIProvider (Imperative API)
  └─ EditorJotaiProvider (Jotai store)
    └─ InitializeApp (i18n, theme)
      └─ App (Main component)
        └─ TunnelsProvider (Portal tunnels)
          └─ Multiple Context Providers:
            ├─ ExcalidrawAPIContext
            ├─ ExcalidrawAppStateContext
            ├─ ExcalidrawElementsContext
            ├─ ExcalidrawActionManagerContext
            └─ ... (8+ more)
```

### 7. Scene Management
**Scene**: Manages element storage and updates
```typescript
scene.getNonDeletedElements()     // Active elements
scene.getElementsIncludingDeleted() // With deleted
scene.getSelectedElements(state)  // User selected
scene.triggerUpdate()             // Force render
scene.onUpdate(callback)          // Subscribe to changes
```

### 8. Rendering Architecture
**Layers**:
1. **staticScene** - Off-screen base element rendering
2. **interactiveScene** - On-screen with user interactions
3. **animation** - Interpolation between states
4. **renderSnaps** - Snap guides and alignment lines

### 9. Collaboration Patterns
```
Local changes
  ↓
Store increment (Durable + Ephemeral)
  ↓
History records (for undo)
  ↓
Socket.io broadcasts to peers
  ↓
Remote receive + reconcile
  ↓
Bound text and elements update
```

**Key State**:
- `collaborators: Map<socketId, Collaborator>`
- `selectedElementIds: Record<elementId, true>`
- `userToFollow: Collaborator | null`

### 10. Portal Tunnel Pattern
**Pattern**: Cross-hierarchy component rendering without prop drilling
```typescript
// Define tunnel
MainMenuTunnel: tunnel()

// Render from anywhere via tunnel
<MainMenuTunnel.Out />

// Inject content from container
<MainMenuTunnel.In>
  <MenuContent />
</MainMenuTunnel.In>
```

**Use Cases**:
- Welcome screen hints
- Dialog confirmations
- Footer content
- Sidebar triggers

## Key Design Principles

| Principle | Implementation |
|-----------|----------------|
| **Separation of Concerns** | Actions, Scene, Renderer, UI Components |
| **Immutability** | Elements immutable, mutations via newElementWith() |
| **Performance** | Selective renders, caching (ShapeCache), batched updates |
| **Extensibility** | ActionManager for custom actions, plugin exports |
| **Accessibility** | ARIA labels, keyboard nav, screen reader support |
| **Testability** | Pure functions, dependency injection via context |

## Performance Optimizations

1. **Memoization** - `React.memo()` with shallow comparison
2. **Batched Updates** - `flushSync()` for critical state changes
3. **Lazy Rendering** - Visible elements only via viewport calculation
4. **Shape Caching** - Pre-computed element shapes cached
5. **RAF Throttling** - Animation frame throttling for smooth updates
6. **Debouncing** - Debounced resize and scroll handlers

## Extension Points

- **Actions**: Register custom actions via `api.registerAction()`
- **Components**: Override UI via render props (TopLeftUI, TopRightUI)
- **Callbacks**: Props for onChange, onExport, onPointerUpdate, etc
- **API Methods**: Imperative methods like updateScene(), mutateElement(), etc

---

## 🔗 Related Documentation

**Learn more about specific aspects:**
- **Detailed Architecture**: See [`docs/technical/architecture.md`](../technical/architecture.md) for data flow diagrams and rendering pipeline
- **Implementation Details**: See [`activeContext.md`](activeContext.md) for current development focus
- **Architectural Decisions**: See [`decisionLog.md`](decisionLog.md) for why these patterns were chosen
- **Product Requirements**: See [`docs/product/PRD.md`](../product/PRD.md) for feature requirements these patterns support
- **Getting Started**: See [`docs/technical/dev-setup.md`](../technical/dev-setup.md) for hands-on implementation guide
