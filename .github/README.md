# GitHub Actions Configuration

## Required Secrets

Configure the following secrets in your GitHub repository settings:

### NPM_TOKEN
**Required for:** Publishing to npm registry
**How to get:** 
1. Go to https://www.npmjs.com/
2. Login to your account
3. Go to Settings → Access Tokens
4. Generate a new token with "Automation" type (or "Classic" with publish permissions)
5. Copy the token and add it as `NPM_TOKEN` in GitHub repository secrets

### CICD_TOKEN (Optional)
**Required for:** Pushing version bumps and tags back to repository
**How to get:**
1. Go to GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Generate a new token with `repo` scope
3. Copy the token and add it as `CICD_TOKEN` in GitHub repository secrets

**Alternative:** If not set, GitHub's default `GITHUB_TOKEN` will be used, but it won't trigger subsequent workflows.

## Workflows

### CI/CD Pipeline (`ci-cd.yml`)
Runs on:
- Push to `main` branch
- Manual trigger via workflow_dispatch

Features:
- ✅ Multi-version Node.js testing (18, 20, 22)
- ✅ Security audit
- ✅ Test coverage reporting
- ✅ CHANGELOG validation
- ✅ Automated versioning
- ✅ GitHub releases with CHANGELOG notes
- ✅ npm publishing with provenance

### PR Validation (`pr-validation.yml`)
Runs on:
- Pull requests to `main` branch

Features:
- ✅ Multi-version Node.js testing (18, 20, 22)
- ✅ Lint and formatting checks
- ✅ Security audit
- ✅ Dependency freshness check
- ✅ Test coverage threshold
- ✅ Semantic PR title validation
- ✅ CHANGELOG update reminder

## Release Process

### Manual Release
1. Go to Actions → CI/CD Pipeline → Run workflow
2. Select release type (patch/minor/major)
3. Workflow will:
   - Run all tests
   - Validate CHANGELOG
   - Bump version
   - Create git tag
   - Create GitHub release
   - Publish to npm

### Automatic Release (on merge to main)
1. Merge PR to `main`
2. Workflow automatically:
   - Bumps patch version
   - Creates release
   - Publishes to npm

## Best Practices

1. **Always update CHANGELOG.md** before merging to main
2. **Use semantic commit messages** for PRs (feat:, fix:, chore:, etc.)
3. **Version format in CHANGELOG**: `## [X.Y.Z] - YYYY-MM-DD`
4. **Test locally** before pushing: `npm run lint && npm test && npm run build`
5. **Review coverage reports** in PR checks
