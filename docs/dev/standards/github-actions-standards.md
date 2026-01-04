# GitHub Actions Standards

> CI/CD patterns and best practices using GitHub Actions.

---

## Overview

GitHub Actions automates:
- **CI (Continuous Integration)**: Build and test on every change
- **CD (Continuous Deployment)**: Deploy when code is merged

---

## Recommended Pipeline Structure

### Two-Workflow Pattern

```yaml
# .github/workflows/ci.yml - Runs on PRs
# .github/workflows/deploy.yml - Runs on push to main
```

### CI Workflow (Pull Requests)

```yaml
# .github/workflows/ci.yml
name: CI

on:
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Type check
        run: npm run typecheck

      - name: Lint
        run: npm run lint

      - name: Test
        run: npm test

      - name: Build
        run: npm run build
```

### Deploy Workflow (Main Branch)

```yaml
# .github/workflows/deploy.yml
name: Deploy

on:
  push:
    branches: [main]
  workflow_dispatch:  # Manual trigger

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Deploy to VPS
        uses: appleboy/ssh-action@v1.0.3
        with:
          host: ${{ secrets.VPS_HOST }}
          username: ${{ secrets.VPS_USER }}
          key: ${{ secrets.VPS_SSH_KEY }}
          script: |
            cd /path/to/project
            git pull origin main
            docker compose up -d --build
```

---

## Workflow Triggers

### Common Triggers

```yaml
on:
  # On push to specific branches
  push:
    branches: [main, develop]

  # On pull requests
  pull_request:
    branches: [main]

  # Manual trigger
  workflow_dispatch:

  # Scheduled (cron)
  schedule:
    - cron: '0 0 * * *'  # Daily at midnight
```

### Path Filters

```yaml
on:
  push:
    paths:
      - 'src/**'
      - 'package.json'
    paths-ignore:
      - '**.md'
      - 'docs/**'
```

---

## Secrets Management

### Required Secrets

Store in: Settings → Secrets and variables → Actions

| Secret | Description |
|--------|-------------|
| `VPS_HOST` | Server IP or hostname |
| `VPS_USER` | SSH username |
| `VPS_SSH_KEY` | Private SSH key |
| `ENV_FILE` | Full .env file contents |

### Using Secrets

```yaml
steps:
  - name: Deploy
    env:
      API_KEY: ${{ secrets.API_KEY }}
    run: |
      echo "Using API key..."
```

### Never Do
- Commit secrets to repository
- Echo secrets in logs
- Use secrets in PR workflows from forks

---

## Job Dependencies

### Sequential Jobs

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps: [...]

  deploy:
    needs: test  # Waits for test to pass
    runs-on: ubuntu-latest
    steps: [...]
```

### Parallel Jobs

```yaml
jobs:
  lint:
    runs-on: ubuntu-latest
    steps: [...]

  test:
    runs-on: ubuntu-latest
    steps: [...]

  deploy:
    needs: [lint, test]  # Waits for both
    runs-on: ubuntu-latest
    steps: [...]
```

---

## Caching

### Node.js Dependencies

```yaml
- uses: actions/setup-node@v4
  with:
    node-version: '20'
    cache: 'npm'  # Automatic caching
```

### Custom Caching

```yaml
- uses: actions/cache@v4
  with:
    path: |
      ~/.npm
      node_modules
    key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
```

---

## Environment Protection

### Production Environment

```yaml
jobs:
  deploy:
    environment: production  # Requires approval
    runs-on: ubuntu-latest
```

Configure in: Settings → Environments → production
- Add required reviewers
- Add deployment branch rules

---

## Common Patterns

### Conditional Deployment

```yaml
deploy:
  if: github.ref == 'refs/heads/main'
  runs-on: ubuntu-latest
```

### Matrix Builds

```yaml
jobs:
  test:
    strategy:
      matrix:
        node-version: [18, 20, 22]
    steps:
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}
```

### Reusable Workflows

```yaml
# .github/workflows/reusable-test.yml
on:
  workflow_call:

jobs:
  test:
    runs-on: ubuntu-latest
    steps: [...]

# .github/workflows/ci.yml
jobs:
  test:
    uses: ./.github/workflows/reusable-test.yml
```

---

## Docker Deployment Pattern

### Build and Deploy

```yaml
- name: Deploy
  uses: appleboy/ssh-action@v1.0.3
  with:
    host: ${{ secrets.VPS_HOST }}
    username: ${{ secrets.VPS_USER }}
    key: ${{ secrets.VPS_SSH_KEY }}
    script: |
      cd ${{ secrets.PROJECT_PATH }}
      git pull origin main

      # Load environment
      cat > .env << 'EOF'
      ${{ secrets.ENV_FILE }}
      EOF

      # Build and start
      docker compose up -d --build --remove-orphans

      # Cleanup
      docker image prune -f
```

### Health Check After Deploy

```yaml
- name: Health check
  run: |
    sleep 30
    curl --fail https://myapp.com/health || exit 1
```

---

## Debugging

### Enable Debug Logging

Add secret: `ACTIONS_STEP_DEBUG` = `true`

### SSH Debugging

```yaml
- name: Setup tmate session
  uses: mxschmitt/action-tmate@v3
  if: failure()
```

---

## Security Best Practices

### Do
- Use `actions/checkout@v4` (specific version)
- Store secrets in GitHub Secrets
- Use environment protection for production
- Limit permissions with `permissions:` key

### Don't
- Use `@main` or `@master` for actions
- Echo secrets in logs
- Run untrusted code from forks with secrets
- Skip security scans

### Minimal Permissions

```yaml
permissions:
  contents: read
  pull-requests: write
```

---

## Workflow Template

```yaml
name: CI/CD

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'

      - run: npm ci
      - run: npm run typecheck
      - run: npm run lint
      - run: npm test
      - run: npm run build

  deploy:
    needs: test
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    environment: production
    steps:
      - uses: actions/checkout@v4

      - name: Deploy
        uses: appleboy/ssh-action@v1.0.3
        with:
          host: ${{ secrets.VPS_HOST }}
          username: ${{ secrets.VPS_USER }}
          key: ${{ secrets.VPS_SSH_KEY }}
          script: |
            cd ${{ secrets.PROJECT_PATH }}
            git pull
            docker compose up -d --build
```

---

## Quick Reference

```yaml
# Triggers
on:
  push:
    branches: [main]
  pull_request:
  workflow_dispatch:

# Job dependencies
jobs:
  deploy:
    needs: [test, lint]

# Conditions
if: github.ref == 'refs/heads/main'
if: failure()
if: success()

# Secrets
${{ secrets.MY_SECRET }}

# Environment variables
env:
  NODE_ENV: production
```
