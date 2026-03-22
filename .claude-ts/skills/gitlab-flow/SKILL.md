---
name: gitlab-flow
description: GitLab Flow branching strategy and CI/CD best practices. Use when managing feature branches, Merge Requests (MRs), and environment-based deployments (staging, production).
---

# GitLab Flow Expert Skill

Standardized workflow for continuous integration and delivery using GitLab.

## 🌿 Branching Strategy

| Branch | Purpose | Lifecycle |
|--------|---------|-----------|
| `main` / `master` | Stable code, reflecting what is in production (or ready for it). | Permanent |
| `feature/*` | New features, bug fixes, or experiments. | Short-lived |
| `staging` | Pre-production environment for final QA. | Permanent |
| `production` | (Optional) Explicit branch for production deployments. | Permanent |

---

## 🤝 Merge Request (MR) Best Practices
- **Atomic Commits**: Keep commits focused and logically grouped.
- **Description**: Use MR templates to describe "What", "Why", and "How".
- **Reviewers**: Assign 1-2 peers for technical review.
- **CI Pipelines**: All pipelines MUST pass before merging.
- **Squash and Merge**: Preferred for clean history on `main`.

---

## 🚀 CI/CD Integration

### .gitlab-ci.yml Structure
```yaml
stages:
  - test
  - build
  - deploy

run_tests:
  stage: test
  script:
    - npm install
    - npm test

deploy_staging:
  stage: deploy
  script:
    - ./deploy.sh staging
  only:
    - staging
```

## Best Practices
- **Never push to main**: Always use MRs.
- **Environment Variables**: Use GitLab CI/CD variables (masked/protected) for secrets.
- **Review Apps**: Use GitLab Review Apps for dynamic feature testing.
- **Shift Left**: Run security and linting checks in the earliest stage of the pipeline.
