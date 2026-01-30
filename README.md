# GitHub Actions Dummy Repository

This repository contains GitHub Actions workflows that automatically send webhook notifications for various GitHub events.

## 🎯 Purpose

This is a dummy repository created for the TechStaX Developer Assessment. It demonstrates automated webhook integration using GitHub Actions.

## 📡 Workflows

### 1. Push Event Webhook (`push-webhook.yml`)
- **Trigger**: When code is pushed to any branch
- **Action**: Sends a webhook with push event details
- **Format**: `{author} pushed to {branch} on {timestamp}`

### 2. Pull Request Event Webhook (`pull-request-webhook.yml`)
- **Trigger**: When a pull request is opened, closed, synchronized, or reopened
- **Action**: Sends a webhook with PR details
- **Format**: `{author} submitted a pull request from {from_branch} to {to_branch} on {timestamp}`

### 3. Merge Event Webhook (`merge-webhook.yml`) 🌟
- **Trigger**: When a pull request is successfully merged
- **Action**: Sends a webhook with merge details
- **Format**: `{author} merged branch {from_branch} to {to_branch} on {timestamp}`
- **Note**: This is a bonus feature for extra points!

## 🔧 Setup Instructions

### 1. Fork/Clone this Repository

```bash
git clone https://github.com/Abrar090909/action-repo.git
cd action-repo
```

### 2. Configure Webhook URL

1. Go to your repository **Settings** → **Secrets and variables** → **Actions**
2. Click **New repository secret**
3. Add the following secret:
   - **Name**: `WEBPACK_URL`
   - **Value**: Your webhook receiver URL (e.g., `https://your-app.onrender.com/webhook`)

### 3. Test the Workflows

#### Test PUSH Event
```bash
# Make any change
echo "# Test" >> TEST.md

# Commit and push
git add .
git commit -m "Test push webhook"
git push origin main
```

#### Test PULL REQUEST Event
```bash
# Create a new branch
git checkout -b test-branch

# Make a change
echo "# Test PR" >> TEST_PR.md

# Commit and push
git add .
git commit -m "Test PR webhook"
git push origin test-branch

# Create PR via GitHub UI or CLI
gh pr create --title "Test PR" --body "Testing pull request webhook"
```

#### Test MERGE Event
```bash
# Merge the PR created above via GitHub UI or CLI
gh pr merge <pr-number> --merge
```

## 📊 Webhook Payload Format

### PUSH Event
```json
{
  "event_type": "push",
  "author": "username",
  "branch": "main",
  "timestamp": "2026-01-30T10:00:00Z",
  "request_id": "unique-uuid"
}
```

### PULL REQUEST Event
```json
{
  "event_type": "pull_request",
  "author": "username",
  "action": "opened",
  "from_branch": "feature-branch",
  "to_branch": "main",
  "timestamp": "2026-01-30T10:00:00Z",
  "request_id": "unique-uuid"
}
```

### MERGE Event
```json
{
  "event_type": "merge",
  "author": "username",
  "from_branch": "feature-branch",
  "to_branch": "main",
  "timestamp": "2026-01-30T10:00:00Z",
  "request_id": "unique-uuid"
}
```

## 🔍 Viewing Workflow Results

1. Go to the **Actions** tab in your GitHub repository
2. Click on any workflow run to see details
3. Check logs to verify webhook was sent successfully

## 📚 Related Repositories

- **[webhook-repo](https://github.com/Abrar090909/webhook-repo)**: Flask webhook receiver and UI dashboard

## 🛠️ Technologies

- **GitHub Actions**: CI/CD automation
- **cURL**: HTTP requests for webhook delivery
- **UUID**: Unique request ID generation

## 📝 Notes

- All workflows use `curl` to send POST requests to the webhook endpoint
- Each request includes a unique `request_id` to prevent duplicates
- Timestamps are in ISO 8601 format
- The webhook URL must be publicly accessible

## 👤 Author

**Abrar**
- GitHub: [@Abrar090909](https://github.com/Abrar090909)

---

**TechStaX Developer Assessment** | GitHub Webhook Integration Demo
