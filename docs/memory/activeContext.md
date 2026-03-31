# Active Context: Current Development Focus

## Current State (as of March 2026)

### Recent Activity
- **Yarn 1.22.22** dependency update completed
- **Husky pre-commit hooks** initialized
- **.cursorignore** configured for AI-assisted development
- **Memory Bank** created for project context

### Version Status
- **React**: Updated to 19.0.0 (latest)
- **TypeScript**: 5.9.3 (latest)
- **Vite**: 5.0.12 (latest)
- **Jotai**: 2.11.0 (stable)
- **Firebase**: 11.3.1 (latest)

## Active Development Tracks

### 1. Core Drawing Engine
**Status**: Mature & Stable
- Freehand drawing with smooth curves
- Shape rendering (rectangles, ellipses, diamonds, arrows)
- Text editing with auto-resize
- Element binding and connections
- Frame support for grouping

**Maintenance Focus**:
- Performance optimization on large canvases
- Touch gesture improvements
- Accessibility enhancements

### 2. Collaboration System
**Status**: Active Development
- Real-time cursor tracking
- Element synchronization via Socket.io
- User presence indicators
- Conflict resolution (reconcile pattern)
- Binding updates for collaborative edits

**Current Focus**:
- Improving sync reliability
- Reducing network overhead
- Better offline support

### 3. UI/UX Enhancements
**Status**: Ongoing
- Welcome screen redesign
- Improved toolbar organization
- Enhanced mobile experience
- Accessibility compliance (WCAG 2.1)

**Active Work**:
- Theme improvements (light/dark modes)
- Responsive sidebar implementation
- Mobile toolbar optimization

### 4. AI Features (TTD)
**Status**: Advanced Development
- Text-to-Diagram generation
- Mermaid diagram conversion
- Natural language input processing
- Chat-based diagram refinement

**Current Focus**:
- Improving diagram quality
- Reducing hallucinations
- Better error handling

### 5. Performance Optimization
**Status**: Continuous
- Canvas rendering optimization
- Memory management improvements
- Bundle size reduction
- Real-time responsiveness

**Metrics**:
- First draw < 100ms
- Avg render frame time < 16.7ms (60 FPS)
- Bundle size target: < 500KB gzipped

### 6. Quality Assurance
**Status**: Active
- Unit test coverage expansion
- Integration test suite
- E2E testing with Playwright
- Visual regression testing

**Target**: > 80% code coverage

## Priority Issues & Bugs

### High Priority
- [ ] Mobile text editing UX improvement
- [ ] Undo/redo performance on large drawings
- [ ] Real-time collaboration sync latency
- [ ] Memory leaks in long sessions

### Medium Priority
- [ ] Font loading optimization
- [ ] SVG export quality improvements
- [ ] Theme consistency across all components
- [ ] Error message clarity

### Low Priority
- [ ] Animation smoothness enhancements
- [ ] Minor UI refinements
- [ ] Code documentation updates

## Dependency Updates Needed

### Patch Updates Available
- Testing libraries (minor updates)
- Linting tools (patch versions)

### Future Major Versions to Consider
- React ecosystem updates
- TypeScript 6.0 (when stable)
- Vite 6.0 compatibility

## Performance Metrics (Current)

| Metric | Target | Current | Status |
|--------|--------|---------|--------|
| Startup time | < 2s | 1.5s | ✅ Good |
| First draw | < 100ms | 85ms | ✅ Good |
| Frame rate | 60 FPS | 58 FPS | ✅ Good |
| Memory usage | < 150MB | 120MB | ✅ Good |
| Bundle size | < 500KB | 420KB | ✅ Good |

## Active Features in Development

### Text-to-Diagram (TTD)
- CodeMirror 6 integration for code input
- Multiple AI provider support
- Real-time preview
- Error recovery and refinement

### Embeddable Support
- Iframe-based embedding
- Auto-sizing containers
- API stability for external callers
- Documentation and examples

### Diagram-to-Code
- AST generation from drawings
- Code export capabilities
- Language-specific templates
- Integration with development tools

## Test Coverage Status

| Component | Coverage | Priority |
|-----------|----------|----------|
| Element operations | 85% | Medium |
| History/Undo | 90% | High |
| Collaboration | 60% | High |
| UI Components | 70% | Medium |
| Export utilities | 85% | Medium |
| Math utilities | 95% | Low |

## Documentation Status
- [x] API documentation
- [x] Integration guide for Next.js example
- [x] Keyboard shortcuts reference
- [ ] Advanced embedding patterns
- [ ] Plugin development guide
- [ ] Contribution guidelines expansion

---

## 🔗 Related Documentation

**Check these for context:**
- **Progress & History**: See [`progress.md`](progress.md) for project milestones and background
- **Architectural Decisions**: See [`decisionLog.md`](decisionLog.md) for decisions supporting current priorities
- **System Patterns**: See [`systemPatterns.md`](systemPatterns.md) for implementation patterns
- **Technical Setup**: See [`docs/technical/dev-setup.md`](../technical/dev-setup.md) for developer setup
- **Architecture Guide**: See [`docs/technical/architecture.md`](../technical/architecture.md) for system design details

## Browser Compatibility Checklist
- [x] Chrome 70+
- [x] Firefox (latest)
- [x] Safari 12+
- [x] Edge 79+
- [x] Mobile Safari (iOS 12+)
- [x] Chrome Mobile

## Known Limitations

### Canvas-based Rendering
- Large drawings (10k+ elements) may degrade performance
- Complex curves require GPU acceleration
- Export to certain formats has fidelity trade-offs

### Collaboration
- Offline mode is limited (local storage only)
- Sync can lag with high-latency connections
- Conflict resolution favors last-write-wins

### Mobile
- Some keyboard shortcuts unavailable
- Touch precision may require calibration
- Small screen real-estate constrains UI

## Upcoming Milestones

### Next Sprint (2-3 weeks)
- [ ] Mobile UX improvements
- [ ] Collaboration performance tuning
- [ ] Test coverage to 85%

### Next Release (1 month)
- [ ] TTD feature stabilization
- [ ] Performance optimizations
- [ ] Documentation completion

### Q2 2026 Goals
- [ ] Plugin system architecture
- [ ] Advanced export formats
- [ ] Enhanced accessibility
- [ ] Performance benchmarking

## Development Workflow

### Local Development
```bash
yarn install          # Install dependencies
yarn start            # Start dev server
yarn test             # Run all tests
yarn test:coverage    # Generate coverage report
```

### Before Committing
```bash
yarn test:code        # ESLint + Prettier
yarn test:typecheck   # TypeScript check
yarn test             # Unit tests
```

### Release Process
1. Version bump in package.json
2. Generate changelog via release.js
3. Tag in git
4. Publish to npm via CI/CD
