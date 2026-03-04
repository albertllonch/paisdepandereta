# Agent Development Guide - País de Pandereta

## Project Overview

País de Pandereta is a minimalist, high-performance platform for citizen transparency in Spain. Built with SvelteKit 5, TailwindCSS 4, and TypeScript.

## Tech Stack

- **Framework**: SvelteKit 5 with Svelte 5 runes
- **Styling**: TailwindCSS 4 (utility-first)
- **Language**: TypeScript (strict mode)
- **Testing**: Vitest (unit) + Playwright (e2e)
- **Build**: Vite

## Architecture Principles

### SOLID Principles

- **Single Responsibility**: Each component does ONE thing well
- **Open/Closed**: Components are open for extension, closed for modification
- **Liskov Substitution**: Components can be swapped without breaking UI
- **Interface Segregation**: Props are minimal and focused
- **Dependency Inversion**: Use composition over inheritance

### Performance

- Lazy loading for routes and heavy components
- Virtual scrolling for long lists (>100 items)
- Image optimization with WebP
- Code splitting at route level
- No blocking on initial paint

### Security

- No user input rendered without sanitization
- CSP headers configured
- No secrets in client code
- Form validation on both client and server
- CSRF protection for mutations

### Testing

- Unit tests for utilities and stores
- Component tests with Vitest + Testing Library
- E2E tests with Playwright for critical flows
- Coverage threshold: 80% for critical paths

## Component Guidelines

### Reusability

```svelte
<!-- Bad: Hardcoded styles and content -->
<div class="bg-blue-500 p-4">
  <h1>My Blog Post</h1>
</div>

<!-- Good: Configurable via props -->
<script lang="ts">
  let { title, variant = 'default', children } = $props();
</script>

<article class="card card--{variant}">
  <h1>{title}</h1>
  {@render children?.()}
</article>
```

### Style Consistency

- Use Tailwind utilities, no arbitrary values
- Color palette: gray scale only (gray-50 to gray-900)
- Typography: Use existing scale (text-sm, text-base, etc.)
- Spacing: Use spacing scale (space-y-4, gap-2, etc.)
- Components must accept `class` prop for overrides

### File Structure

```
src/
├── lib/
│   ├── components/          # Reusable components
│   │   ├── atoms/          # Smallest units (Button, Input)
│   │   ├── molecules/      # Composites (Card, FormField)
│   │   └── organisms/      # Complex components (BlogPost, CommentSection)
│   ├── stores/             # Svelte stores
│   ├── utils/              # Helper functions
│   └── types/              # TypeScript types
├── routes/                 # SvelteKit routes
└── tests/                  # Test files mirror src structure
```

### Naming Conventions

- Components: PascalCase (BlogPost.svelte)
- Utilities: camelCase (formatDate.ts)
- Types: PascalCase with Types suffix (PostTypes.ts)
- Stores: camelCase with $ prefix usage ($blogStore)

## Git Workflow

### IMPORTANT: NEVER Push to Main

**🚨 CRITICAL: All development MUST happen on feature branches via Pull Requests. Direct pushes to main are STRICTLY FORBIDDEN.**

### Branch Naming

- `feature/blog-system`
- `feature/blog-list-component`
- `fix/blog-loading-error`
- `test/blog-component-tests`

### Commit Messages

```
feat(blog): add post listing component
fix(blog): resolve hydration mismatch
refactor(blog): extract pagination logic
test(blog): add unit tests for BlogPost
```

### Before Starting Work

```bash
# Check current status
git status
git branch

# Create feature branch (ALWAYS create a branch first!)
git checkout -b feature/your-feature-name

# Verify you're on the right branch (NOT main)
git branch
```

feat(blog): add post listing component
fix(blog): resolve hydration mismatch
refactor(blog): extract pagination logic
test(blog): add unit tests for BlogPost

````

### Before Starting Work

```bash
# Check current status
git status
git branch

# Create feature branch (ALWAYS create a branch first!)
git checkout -b feature/your-feature-name

# Verify you're on the right branch (NOT main)
git branch
````

## Multi-Agent Coordination

### How to Invoke Agents

Use the `/task` command in opencode to launch agents:

```bash
# Single feature
task Implement the blog post listing page with pagination and search

# Multiple parallel agents
task Create BlogCard atom component
task Create BlogList molecule component
task Set up blog data store with Svelte 5 runes
task Write tests for blog components
```

### Agent Responsibilities

When multiple agents work in parallel:

1. **Shared Component Agent**: Creates base components (atoms/molecules)
2. **Page Agent**: Implements routes and page-level logic
3. **Data Agent**: Sets up stores, types, and data fetching
4. **Test Agent**: Writes tests for components and stores

### Coordination Rules

1. **No Overlapping Files**: Agents claim files in their initial response
2. **Base Components First**: Atoms must be ready before molecules use them
3. **Shared Components**: Create in `$lib/components/atoms/` or `$lib/components/molecules/`
4. **Communication**: Each agent reports what files they're modifying

### Example Multi-Agent Session

```bash
# Agent 1: Set up foundation
task Set up blog types, stores, and data layer with proper TypeScript types

# Agent 2: Create components (wait for #1 if needed)
task Create BlogCard and BlogList components following atomic design

# Agent 3: Build page
task Implement /blog route with listing, pagination, and filtering

# Agent 4: Add tests
task Write comprehensive tests for blog stores and components
```

## Testing Strategy

### Unit Tests (Vitest)

```typescript
// src/lib/utils/formatDate.test.ts
import { describe, it, expect } from 'vitest';
import { formatDate } from './formatDate';

describe('formatDate', () => {
	it('formats ISO date to Spanish locale', () => {
		expect(formatDate('2024-01-15')).toBe('15 de enero de 2024');
	});
});
```

### Component Tests

```typescript
// src/lib/components/atoms/Button.test.ts
import { render, screen, fireEvent } from '@testing-library/svelte';
import { describe, it, expect, vi } from 'vitest';
import Button from './Button.svelte';

describe('Button', () => {
	it('calls onClick when clicked', async () => {
		const onClick = vi.fn();
		render(Button, { props: { onClick, children: 'Click me' } });
		await fireEvent.click(screen.getByText('Click me'));
		expect(onClick).toHaveBeenCalled();
	});
});
```

### Running Tests

```bash
npm run test          # Run all tests
npm run test:unit     # Run unit tests only
npm run test:e2e      # Run E2E tests
npm run test:watch    # Watch mode for development
```

## Feature Development Process

### 1. Before Coding

- Read AGENTS.md
- Check existing components to avoid duplication
- Create feature branch

### 2. During Coding

- Follow Clean Code principles
- Keep components small (<150 lines)
- Use TypeScript strictly
- Write tests alongside code

### 3. Before Committing

```bash
npm run lint          # Check formatting
npm run check         # Type check
npm run test          # Run tests
```

### 4. Commit & Create Pull Request

```bash
# Stage and commit changes
git add .
git commit -m "feat(scope): description"

# Push to remote (creates branch on GitHub)
git push -u origin feature/your-feature

# Create Pull Request via GitHub CLI (or use GitHub web interface)
gh pr create --title "feat(scope): description" --body "Description of changes"

# DO NOT MERGE - Wait for review and approval
```

**CRITICAL:** Never merge your own PR. Always wait for review from another agent or human.

## Code Quality Checklist

- [ ] Component does ONE thing (SRP)
- [ ] Props are typed with TypeScript
- [ ] No magic numbers or strings
- [ ] Functions are pure where possible
- [ ] Error handling implemented
- [ ] Loading states considered
- [ ] Tests written and passing
- [ ] No console.logs in production code
- [ ] Lighthouse score > 90
- [ ] No accessibility warnings

## Security Checklist

- [ ] User input sanitized
- [ ] No XSS vulnerabilities
- [ ] No secrets in code
- [ ] Form validation on server
- [ ] Proper CSP headers
- [ ] No inline scripts

## Performance Targets

- First Contentful Paint: < 1.5s
- Time to Interactive: < 3s
- Lighthouse Performance: > 90
- Bundle size: < 200KB initial

## Questions?

If uncertain:

1. Check existing code for patterns
2. Keep it simple and minimal
3. Ask for clarification via git commit messages or comments
