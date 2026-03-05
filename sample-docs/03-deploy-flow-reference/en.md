# Deploy Flow Overview

> **Suggested CTA placement:** Service details "Deployments" section

A Zeabur deployment lifecycle: **Trigger → Build → Run → Domain live**.

This is a reference doc — one question per heading — designed for AI indexing and in-app CTAs. For step-by-step operations, see the linked docs.

---

## What triggers a deployment?

| Source | Trigger |
|--------|---------|
| **GitHub** | Push to a connected branch. Use [Watch Paths](https://zeabur.com/docs/en-US/deploy/watch-paths) to limit which directories trigger a deploy |
| **Local project / Cursor** | Triggered once on upload or IDE deploy |
| **Template** | Triggered when deploying from the [Template Marketplace](https://zeabur.com/templates) |
| **Docker image** | Triggered after specifying an image name |
| **Manual** | Manually trigger redeploy from service details or deploy history |

For monorepos: the default watch path is `*` (any change triggers all services). Set frontend to `/client` and backend to `/server` so changes don't cross-trigger. Format is like `.gitignore`, but here it means "trigger" instead of "ignore".

---

## What happens during the build phase?

Zeabur auto-detects your code type (Node.js, Python, Go, etc.) and picks the right build method. If you use a Dockerfile, it builds according to that.

Build sequence: Clone source → Install dependencies → Run build → Generate container image.

Only some environment variables are available during build (Git-related special variables). Use Dockerfile `ARG` if you need to inject variables at build time.

---

## Where to check logs when a deploy fails?

In your service's **Deploy** or **Logs** tab:

- **Build logs**: Docker build, npm install, pip install failures show here
- **Runtime logs**: Post-startup crashes or runtime errors show here

You can filter by deploy version and time.

---

## How to rollback to a previous version?

In your service's **Deploy History**, select a previous successful version and click **Rollback**. That version becomes the current live version.

---

## How do default and custom domains work?

**Default domain:** After deployment, Zeabur auto-assigns a `xxx.zeabur.app` domain. Accessible within ~30 seconds, HTTPS included.

**Custom domain:** Add it in your service's **Networking** page, then point your DNS to the record Zeabur provides. HTTPS is handled automatically once DNS propagates.

See [Public Networking](https://zeabur.com/docs/en-US/networking/public).

---

## What's the difference between build-time and runtime environment variables?

- **Runtime:** Variables set in the Variables page are injected into running containers. Changes require restart or redeploy
- **Build-time:** Only Git-related special variables and Dockerfile `ARG` values are available during build
- **Priority:** Current service variables > Other services' exposed variables > Special variables

See [Environment Variables](https://zeabur.com/docs/en-US/deploy/variables).

---

## How to trigger deployments only for specific directories?

In service settings, find **Watch Paths**. Format is like `.gitignore`, but represents "trigger" instead of "ignore".

Example: set to `/client` so only changes in the `client` directory trigger this service's deployment.

See [Watch Paths](https://zeabur.com/docs/en-US/deploy/watch-paths).

---

## Does copying or exporting a project trigger a deployment?

- **Copy project:** Yes. Services auto-deploy in the new project after copying, but domains need to be re-bound
- **Export project:** No. Exports as a YAML template; you need to import and deploy separately. Exports don't include service data — use backup/restore for that

---

## Related Docs

- [Create Service](https://zeabur.com/docs/en-US/deploy/create-service)
- [GitHub Integration](https://zeabur.com/docs/en-US/deploy/github)
- [Environment Variables](https://zeabur.com/docs/en-US/deploy/variables)
- [Watch Paths](https://zeabur.com/docs/en-US/deploy/watch-paths)
- [Dockerfile Deploy](https://zeabur.com/docs/en-US/deploy/dockerfile)
- [Deploy from Template](https://zeabur.com/docs/en-US/template/deploy-template)

---

## Still have questions?

Visit the [Zeabur Forum](https://zeabur.com/forum) or join [Discord](https://zeabur.com/dc) for real-time support.
