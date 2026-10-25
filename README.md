# App starter

> A business-app skeleton: every sign-in way, a dashboard, settings pages and record pages.

Built with [Sovrium](https://sovrium.com) — a configuration-as-code interpreter: one config
file in, a complete self-hosted web application out.

## Use this template

Click **Use this template** on GitHub to copy this app into your own repository (clean
history, yours to modify), or scaffold it locally:

```bash
curl -fsSL https://sovrium.com/install | sh
sovrium init my-app-starter --template app-starter
```

## What's inside

The pages almost every business app needs, around one table of projects you rename to
your own records:

- **Every way in** — sign in with a password, an emailed link, a passkey or single sign-on;
  two-step verification, whose code is asked on its own page once the password is right;
  sign up; reset a forgotten password; accept an invitation. Each alternative is drawn
  only when `config/auth.yaml` turns it on.
- **Overview** (`/`) and **Metrics** — figures, a trend, a breakdown and the latest
  activity, all narrowed by one period selector.
- **Worklist** — the active projects in tabs, with the figures that matter and a "New" dialog.
- **Settings** — your account, your security (passkeys, two-step, signed-in devices), your
  API keys, the team with its invitations, and the workspace. Every settings page shares the
  list of sections on its left (`config/pages/_settings-nav.yaml`); on a phone it folds into
  one menu, as the top bar's links do.
- **Projects** — a list whose rows open in a side panel with Previous and Next, and a page
  per project with its facts, its tasks, its comments and an edit page.

The **Blocks** pages (`/kit/navigation`, `/kit/feedback`, `/kit/data`, a client page and two
application frames) show every other application block of the library in its stock copy —
bracketed words are the ones you replace. Every link on them was pointed at a page this app
serves — a project, the Worklist, the Metrics, a client — so none leads to a page the app
does not have; "New project" opens the Worklist, where projects are created. Keep the ones
you need, delete the rest.

Every page is made of blocks from the Sovrium library, installed with
`sovrium library add` — each file under [`library/block/`](./library/block) starts with
the line naming the block and the version it came from. They are plain config: change
them in place.

Single sign-on needs `SSO_CLIENT_ID` and `SSO_CLIENT_SECRET` from your identity provider.
Without them the app still starts; the single sign-on button cannot finish a sign-in
until you set them.

## What to try

Load the demo data first, or every table starts empty. It creates three accounts (one per
role), six projects with their tasks, a week of activity, this week's meetings, the team
directory, two clients, the payment reminders and the workspace settings, all dated
relative to today. The **Kit** pages' sample links open the first demo client and project, so
they need it too:

```bash
SOVRIUM_SEED_PASSWORD=choose-a-password sovrium seed app.yaml
sovrium start app.yaml
```

Sign in as **ana.lindqvist@starter.example** (admin), **marc.oyelaran@starter.example**
(member) or **sana.okafor@starter.example** (viewer), with the password you chose. Then:

1. On the **Overview**, switch the period between 7, 30 and 90 days and watch every panel follow.
2. Open **Projects**, click a row, and step through the list with Next.
3. Open a project's own page: add a task — it is linked to the project already — and leave a comment.
4. In **Settings → Security**, add a passkey, then sign out and back in with it.
5. As Ana, open **Settings → Team**, invite someone, and open the link the email carries: it
   lands on this app's own invitation page. Without an email provider the email is printed
   in the server log.

## Run locally

```bash
curl -fsSL https://sovrium.com/install | sh
cp .env.example .env
sovrium seed app.yaml        # needs SOVRIUM_SEED_PASSWORD in .env
sovrium start app.yaml --watch
```

Zero-config: embedded SQLite, local file storage, no variable required to boot.
[`.env.example`](./.env.example) lists the optional ones this app reads.
The first administrator comes from `AUTH_ADMIN_EMAIL` and `AUTH_ADMIN_PASSWORD` on the
first start, or from `sovrium admin create <email>`.
`--watch` reloads the app each time you save a config file.

## Deploy

Ship it to Sovrium Cloud from this directory: sign in once, then deploy. The CLI finds or
creates the app it deploys to, checks the variables it needs, bundles and uploads it, and
ends only once the app answers at its address.

```bash
sovrium login
sovrium deploy
```

Any other host works the same way: run the `sovrium` binary with this config (see the
[deployment guides](https://sovrium.com/en/docs/installation)).

> **The demo accounts are for trying the app, not for running it.** The seed gives every
> account it creates, the admin included, the one password in `SOVRIUM_SEED_PASSWORD`, and
> their addresses are in `seed/`. Before anyone else can reach the app, choose a long
> password or skip the seed, and change or delete the demo admin.

## About this repository

This repository is **auto-published from the
[Sovrium monorepo](https://github.com/sovrium/sovrium)** on every release
(source: [`src/templates/app-starter`](https://github.com/sovrium/sovrium/tree/main/src/templates/app-starter)).
Issues are welcome here; please send code contributions upstream to the monorepo so the
template stays in sync with the engine. The pinned engine release lives in
`.sovrium-version`.

License: [MIT](./LICENSE). The Sovrium engine itself is licensed separately
([BSL 1.1](https://github.com/sovrium/sovrium/blob/main/LICENSE.md)).
