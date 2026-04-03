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
### Single dependency (`needs: deploy`)
```yaml
notify:
  needs: deploy
  if: ${{ always() }}
  uses: PavelMilanov/pachca-actions-notify/.github/workflows/notify.yaml@v1
  with:
    status: ${{ needs.deploy.result == 'success' && 'success' || 'failure' }}
  secrets:
    PACHCA_WEBHOOK_URL: ${{ secrets.PACHCA_WEBHOOK_URL }}
```

### Multiple dependencies (`needs: [build, deploy]`)
```yaml
notify:
  needs: [build, deploy]
  if: ${{ always() }}
  uses: PavelMilanov/pachca-actions-notify/.github/workflows/notify.yaml@v1
  with:
    status: ${{ needs.build.result == 'success' && needs.deploy.result == 'success' && 'success' || 'failure' }}
  secrets:
    PACHCA_WEBHOOK_URL: ${{ secrets.PACHCA_WEBHOOK_URL }}
```

## Requirements
1. Repository visibility: **Public**.
2. Workflow file must stay at `.github/workflows/notify.yaml`.
3. Callers should pin by tag (`@v1`) or commit SHA.

## Release
1. Push this project to a public GitHub repository.
2. Create tag `v1` (or pin callers to commit SHA).
