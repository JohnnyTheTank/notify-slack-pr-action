# Notify Slack GitHub Action

A simple GitHub Action to send pull request notifications to Slack.

## Usage

```yaml
- name: Send notification to Slack about created Pull Request
  uses: JohnnyTheTank/notify-slack-pr-action@v1.1.0
  with:
    webhook-url: ${{ secrets.SLACK_WEBHOOK_URL }}
    pr-url: ${{ steps.create_pr.outputs.pr_url }}
    source-repo: 'my-org/my-tool'
    target-repo: 'my-org/my-repo'
    description: 'This PR includes critical bug fixes.'
```

## Inputs

| Input              | Description                                 | Required | Default                                                                                                                                                                 |
| ------------------ | ------------------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `webhook-url`      | Slack webhook URL                           | Yes      | -                                                                                                                                                                       |
| `pr-url`           | URL of the created Pull Request             | Yes      | -                                                                                                                                                                       |
| `source-repo`      | Source repository name (format: org/repo)   | Yes      | -                                                                                                                                                                       |
| `target-repo`      | Target repository name (format: org/repo)   | Yes      | -                                                                                                                                                                       |
| `message-template` | Custom message template                     | No       | `':github_green: <https://github.com/{source-repo}\|\`{source-repo}\`> created a <{pr-url}\|*new Pull Request*> for <https://github.com/{target-repo}\|{target-repo}>'` |
| `description`      | Additional description to append to message | No       | -                                                                                                                                                                       |

## Template Variables

The following variables can be used in your custom message template:

- `{source-repo}` - Source repository name (including organization)
- `{target-repo}` - Target repository name (including organization)
- `{pr-url}` - URL of the Pull Request

Example message template:
```
:github_green: <https://github.com/{source-repo}|{source-repo}> created a <{pr-url}|*new Pull Request*> for <https://github.com/{target-repo}|{target-repo}>
```

## Example with Custom Message

```yaml
- name: Send notification to Slack about created Pull Request
  uses: JohnnyTheTank/notify-slack-pr-action@v1.1.0
  with:
    webhook-url: ${{ secrets.SLACK_WEBHOOK_URL }}
    pr-url: ${{ steps.create_pr.outputs.pr_url }}
    source-repo: 'my-org/my-tool'
    target-repo: 'my-org/my-repo'
    message-template: ':rocket: New PR from {source-repo} to {target-repo}: <{pr-url}|Click here>'
    description: 'This includes changes to the deployment process.'
```

