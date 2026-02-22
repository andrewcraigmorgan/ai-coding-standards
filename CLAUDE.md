# Global Instructions

- Never add Claude as a contributor in any files (package.json, README, etc.)
- Never include copyright notices or attribution claiming Claude wrote the code
- All code written belongs to the user

## Bitbucket

Use the Bitbucket MCP tools (`mcp__bitbucket__bb_*`) for all Bitbucket operations.

### Creating PRs
1. Fetch default reviewers: `bb_get /repositories/{ws}/{repo}/default-reviewers`
2. Filter out the author (Andrew Morgan / andrewmorganmtc) - authors can't review their own PR
3. Create PR with remaining reviewers, destination branch `staging`

### Merging PRs
- **Wait for CI pipeline to pass before merging**
- Always use `"close_source_branch": true`
- Use `"merge_strategy": "merge_commit"`

## Git Workflow Standards

### Branch Naming

```
feature/add-checklist-scheduling
bugfix/fix-authentication-redirect
hotfix/critical-security-patch
chore/update-dependencies
refactor/restructure-components
```

### Commit Message Format

```
type(scope): description

- feat: new features
- fix: bug fixes
- docs: documentation changes
- style: formatting changes
- refactor: code restructuring
- test: adding/updating tests
- chore: maintenance tasks

Examples:
feat(api): add checklist instance generation endpoint
fix(mobile): resolve authentication token refresh issue
```

## Coding Standards

### TypeScript/JavaScript Linting Rules

**CRITICAL:** Follow these rules to avoid pre-commit failures:

1. **No `console.log`** - Only `console.warn` and `console.error` are allowed. For tests, remove console statements entirely.

2. **No unused variables** - Every declared variable must be used. In catch blocks, use `catch {` (no variable) instead of `catch (error) {` if you don't use the error.

3. **No unused imports** - Remove any imports that aren't used in the file.

4. **Run lint before committing** - Always run `npm run lint` to check for issues before staging files.

```typescript
// BAD - will fail pre-commit
console.log('Debug info')
try { ... } catch (error) { /* error unused */ }

// GOOD
console.warn('Warning message')  // or remove entirely
try { ... } catch { /* no variable needed */ }
```

### Quick Reference

| Rule                  | Value              |
| --------------------- | ------------------ |
| Indentation           | 4 spaces (no tabs) |
| Max line length       | 120 characters     |
| Line endings          | LF (Unix-style)    |
| PHP standard          | PSR-12             |
| JS/TS semicolons      | None               |
| JS/TS quotes          | Single quotes      |
| JS/TS trailing commas | Always             |

## Security Standards

- **Never store plaintext passwords** - always use proper hashing
- **Environment variables** for secrets (never commit .env files)
- **Input validation** on all requests
- **Authorization checks** in all controllers
- **Use UUIDs** instead of predictable IDs where appropriate

## Performance Standards

- **Eager loading** to prevent N+1 queries
- **Database indexes** on foreign keys and frequently queried columns
- **Pagination** for large result sets
- **Queue jobs** for heavy operations
