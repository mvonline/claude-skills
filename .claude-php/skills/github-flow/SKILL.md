---
name: github-flow
description: GitHub Flow branching strategy and Actions best practices. Use when managing feature branches, Pull Requests (PRs), and continuous deployment to main.
---

# GitHub Flow Expert Skill

Streamlined workflow for continuous delivery using GitHub.

## 🌿 The GitHub Flow

1. **Create a branch**: Create a descriptively named branch from `main`.
2. **Add commits**: Snapshot your changes with clear, atomic commits.
3. **Open a Pull Request**: Request feedback and start the review process early.
4. **Discuss and review**: Iterate based on peer feedback.
5. **Merge**: Once approved and CI passes, merge into `main`.
6. **Deploy**: Deploy to production immediately after merging to `main`.

---

## 🤝 Pull Request (PR) Best Practices
- **Early PRs**: Open as "Draft" if still in progress to get early eyes.
- **Task Lists**: Use `- [ ]` to track remaining work.
- **Reviewers**: Request reviews from relevant code owners.
- **Automated Checks**: Ensure all GitHub Actions pass (lint, test, build).

---

## 🚀 GitHub Actions CI/CD

### .github/workflows/main.yml
```yaml
name: CI
on: [push, pull_request]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install & Test
        run: |
          composer install
          ./vendor/bin/pest
```

## Best Practices
- **Branch Protection**: Require status checks and reviews before merging to `main`.
- **Secrets**: Use GitHub Secrets for sensitive data; never hardcode.
- **Optimized Runs**: Use `shivammathur/setup-php@v2` for the best PHP Action environment.
