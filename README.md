# turbo prune lockfile bug reproduction

Minimal reproduction for `turbo prune --docker` producing a broken pnpm lockfile when pnpm overrides interact with packages that have **multiple peer-dependency resolution variants.

## Reproduce

```bash
pnpm install --frozen-lockfile  # succeeds - lockfile is valid
pnpm turbo prune server --docker
pnpm --dir out/json install --frozen-lockfile  # FAILS: ERR_PNPM_LOCKFILE_MISSING_DEPENDENCY
```

## Expected

The pruned lockfile should contain all snapshot entries needed by the included packages.
