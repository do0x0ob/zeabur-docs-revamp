# Quick Start

> **Suggested CTA placement:** Empty state (project, server)

Zeabur lets you get services online in minutes — no Docker, CI/CD, or any DevOps setup.

Don't have an account yet? [Sign up here](https://zeabur.com); once verified, you can let the magic begin.

---

## Get a Server Ready

Zeabur currently runs mainly on dedicated servers. You need at least one server before you can create projects and deploy services.

There are two options:

1. **Buy from Zeabur** — Go to the [Dedicated Server](https://zeabur.com/new) page, pick a plan, and get server resources at a good price.

   Docs: [Dedicated Server](https://zeabur.com/docs/en-US/dedicated-server)

2. **Register your own machine** — If you already have a machine with AWS, GCP, Hetzner, or other providers, you can [register it with Zeabur](https://zeabur.com/docs/en-US/dedicated-server/register) for unified management.


## Deploy Your First Service

Inside your project, click **Deploy New Service**. You'll see several options:

### Fastest: Deploy from Template

Click **Template**, pick one you like, click **Deploy**, and let Zeabur deploy it for you.

Not sure which to pick? These give you something to see as soon as they're up:

| Template | Use case |
|----------|----------|
| [WordPress](https://zeabur.com/en-US/templates/CV344X) | Site/blog — open it and see something right away |
| [Halo](https://zeabur.com/en-US/templates/Q6H2MA) | Chinese blog system, ready out of the box |
| [Uptime Kuma](https://zeabur.com/en-US/templates/Q764RP) | Service monitoring dashboard, nice UI when it's up |

See [Deploy from Template](https://zeabur.com/docs/en-US/template/deploy-template).

### Deploy Your Own Code: From GitHub

1. **Create a project**: From the project area, click **Create Project** and choose the target server for the project. One project can hold your frontend, backend, database, and all related **services**.
2. **Deploy from GitHub**: On the project page, click **Create Service** / **Deploy New Service**, choose **GitHub** in the dropdown, and click **Set up GitHub repository** to connect your GitHub account. Then search and select the repo you want to deploy; Zeabur will analyze your code and pick the best build method — just click **Deploy**.

### Other Options

Zeabur also supports multiple deployment methods:

- **Local project** — Drag and drop a folder to upload
- **Docker image** — Deploy any image from Docker Hub
- **Cursor** — Deploy directly from Cursor IDE  

  …and more.

## Go Live

After deployment, Zeabur gives you a URL you can open (e.g. `xxx.zeabur.app`). Once it's ready, open it to see the service you just set up.

Want to use your own domain? Add it on the service's **Networking** page; after DNS is set, HTTPS is handled automatically.

---

## Stuck?

There's an AI chat on the right. It can read your project status and build logs, point out what's wrong, and help fix it automatically.

---

## What's Next

- [Deploy from Template](https://zeabur.com/docs/en-US/template/deploy-template) — More templates and post-deploy setup
- [Deploy Flow Overview](https://zeabur.com/docs/en-US/deploy/deploy-flow) — Triggers, builds, rollbacks, and the full flow
- [Language & Framework Guides](https://zeabur.com/docs/en-US/guides/nodejs) — How your framework runs on Zeabur
- [Environment Variables](https://zeabur.com/docs/en-US/deploy/variables) — Set the variables your service needs

Questions? Go to [Zeabur Forum](https://zeabur.com/forum) or join [Discord](https://zeabur.com/dc).
