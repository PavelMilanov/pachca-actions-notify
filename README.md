# pachca-notify-workflow

Public reusable GitHub Actions workflow for Pachca notifications.

## Reusable workflow
- Path: `.github/workflows/notify.yaml`
- Trigger: `workflow_call`
- Inputs:
  - `status` (`success` or `failure`, required)
- Secrets:
  - `PACHCA_WEBHOOK_URL` (required)

## Usage
```yaml
notify_success:
  uses: <ORG>/pachca-notify-workflow/.github/workflows/notify.yaml@v1
  with:
    status: success
  secrets:
    PACHCA_WEBHOOK_URL: ${{ secrets.PACHCA_WEBHOOK_URL_SUCCESS }}
```

```yaml
notify_failure:
  uses: <ORG>/pachca-notify-workflow/.github/workflows/notify.yaml@v1
  with:
    status: failure
  secrets:
    PACHCA_WEBHOOK_URL: ${{ secrets.PACHCA_WEBHOOK_URL_FAILURE }}
```

## Requirements
1. Repository visibility: **Public**.
2. Workflow file must stay at `.github/workflows/notify.yaml`.
3. Callers should pin by tag (`@v1`) or commit SHA.

## Release
1. Push this project to a public GitHub repository.
2. Create tag `v1` (or pin callers to commit SHA).
3. Replace `<ORG>` in callers.
