# Agent Workflow Guide - How to Use Multiple Agents

## Overview

This guide explains how to invoke multiple AI agents to work on the País de Pandereta project in parallel.

## Quick Start

### 1. Single Agent (Sequential Development)

Use for simple features or when you want full control:

```bash
task Implement a complete blog system with listing, article pages, and search
```

### 2. Multiple Agents (Parallel Development)

Launch multiple agents simultaneously to work on different parts of a feature:

```bash
# Agent 1: Foundation (start first, others depend on this)
task Set up blog data types, stores, and utilities with TypeScript

# Agent 2: Base Components (can start in parallel)
task Create reusable blog atoms: Button, Badge, Tag components

# Agent 3: Composite Components (wait for #1 if needed)
task Create BlogCard, BlogList, and SearchBar molecules

# Agent 4: Page Implementation (wait for #2 and #3)
task Implement /blog route with listing and article detail pages

# Agent 5: Testing (can start once components exist)
task Write comprehensive tests for blog stores and components
```

## Coordination Rules

When using multiple agents:

1. **Start with foundation first** - Data layer and base types
2. **Claim files** - Each agent reports what files they're modifying
3. **No overlapping work** - Check AGENTS.md for component patterns
4. **Branch per feature** - Agents will create branches automatically
5. **Review before merge** - Test each agent's work before merging

## Example: Building the Blog System

### Phase 1: Foundation

```bash
task Create blog types and interfaces in src/lib/types/ following AGENTS.md patterns
```

**Agent Responsibilities:**

- Create `src/lib/types/blog.ts`
- Define Post, Tag, Author interfaces
- Add utility types for filters/sorting

### Phase 2: Data Layer

```bash
task Set up Svelte 5 runes store for blog posts with CRUD operations
```

**Agent Responsibilities:**

- Create `src/lib/stores/blogStore.ts`
- Implement loading states and error handling
- Add search and filter functionality

### Phase 3: Atoms (Base Components)

```bash
task Create blog atom components: Button, Input, Badge following Tailwind guidelines
```

**Agent Responsibilities:**

- Create components in `src/lib/components/atoms/`
- Ensure reusability with props
- Add basic tests

### Phase 4: Molecules (Composite Components)

```bash
task Create BlogCard, BlogList, and SearchBar using atom components
```

**Agent Responsibilities:**

- Create components in `src/lib/components/molecules/`
- Use atoms for consistency
- Implement responsive design

### Phase 5: Pages

```bash
task Implement /blog listing page and /blog/[slug] detail page
```

**Agent Responsibilities:**

- Create routes in `src/routes/blog/`
- Wire up stores and components
- Add loading and error states

### Phase 6: Testing

```bash
task Write Vitest tests for all blog components and stores
```

**Agent Responsibilities:**

- Unit tests for utilities
- Component tests for atoms/molecules
- Integration tests for pages

## Best Practices

### Before Launching Agents

1. Read `AGENTS.md` thoroughly
2. Ensure project builds: `npm run check`
3. Check existing components to avoid duplication
4. Define clear boundaries for each agent

### While Agents Work

1. **Monitor git branches** - Each agent creates their own
2. **Review PRs** - Don't auto-merge; review quality
3. **Test integration** - Run `npm run test` after merging
4. **Check for conflicts** - Agents should coordinate via AGENTS.md

### After Agents Complete

1. Run full test suite: `npm run test`
2. Check code quality: `npm run lint && npm run check`
3. Test manually: `npm run dev`
4. Merge branches and push

## Troubleshooting

### Agents Step on Each Other

**Problem:** Two agents editing the same file

**Solution:**

- Restart with clearer boundaries
- Use `task` with specific file paths
- Have one agent own shared components

### Merge Conflicts

**Problem:** Agents created conflicting changes

**Solution:**

- Resolve locally
- Coordinate via commit messages
- Use feature flags for gradual rollout

### Tests Fail

**Problem:** Agent code breaks existing tests

**Solution:**

- Fix immediately before merging
- Ensure agents write tests alongside code
- Run `npm run test:watch` during development

## Example Session

```bash
# 1. Check project status
npm run check

# 2. Launch foundation agent
task Create blog TypeScript types and interfaces in src/lib/types/

# 3. Wait for completion, review PR
# ... review code ...

# 4. Launch component agents (in new terminal tabs)
task Create Button, Input, Badge atoms in src/lib/components/atoms/
task Create blog Svelte store with runes in src/lib/stores/

# 5. Wait for completion, review PRs
# ... review both ...

# 6. Launch composite agent
task Create BlogCard and BlogList using existing atoms

# 7. Launch page agent
task Implement /blog/+page.svelte and /blog/[slug]/+page.svelte

# 8. Launch test agent
task Write comprehensive tests for all blog functionality

# 9. Run full verification
npm run test
npm run check
npm run lint

# 10. Merge all branches
```

## Tips for Success

1. **Start small** - Use single agents for your first few features
2. **Clear requirements** - Be specific in your task descriptions
3. **Review everything** - Never auto-merge agent code
4. **Test incrementally** - Run tests after each agent completes
5. **Document changes** - Update README or docs when agents add features

## Questions?

- Check `AGENTS.md` for coding standards
- Review existing components before creating new ones
- Use clear, specific task descriptions for agents
