# dar-ci-notify

Reusable GitHub composite action for Telegram deploy notifications, shared across all personal + work (Faro) repos.

## Usage

Add near the end of your deploy/CI workflow, as the last step of a job (works even if earlier steps failed, since `if: always()` is used):

```yaml
- name: Notify Telegram
  if: always()
  uses: arayaroma/dar-ci-notify/telegram-deploy@main
  with:
    bot-token: ${{ secrets.TELEGRAM_BOT_TOKEN }}
    chat-id: ${{ secrets.TELEGRAM_CHAT_ID }}
    project: faro-api
    status: ${{ job.status }}
    environment: production
```

## Required secrets (set per repo)

```
gh secret set TELEGRAM_BOT_TOKEN --repo <owner>/<repo>
gh secret set TELEGRAM_CHAT_ID --repo <owner>/<repo>
```

Same bot/chat already used by dar-billing-pubsub's bill-tracker webhook — reused here for a different purpose (outbound notifications only, no webhook receiving).
