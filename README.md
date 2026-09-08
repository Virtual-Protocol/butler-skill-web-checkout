# butler-web-checkout

Buy, order or book on a real website — the merchant kind that blocks bots — with a stealth
browser, a login that survives between runs, email/SMS two-factor, and a single-use card at
checkout.

This repository is one Butler skill. It is published through the
[Butler Skill Hub](https://github.com/Virtual-Protocol/butler-skills): `skills.json` there
lists this skill by name and repo link, and every hub build re-resolves the listed ref to a
commit, so a merge here reaches Butlers on the next build. Butler containers clone the
resolved commit.

- `SKILL.md` — the playbook (frontmatter + the fixed sections; see the hub's
  [SKILL_STANDARD.md](https://github.com/Virtual-Protocol/butler-skills/blob/main/SKILL_STANDARD.md))
- `CHANGELOG.md` — one line per version; every change bumps `version` in SKILL.md

There is no `duty.py`: this skill is `modes: ["one-off"]`. A standing order ("coffee every
morning") is a duty built with `bevo-automation` after rehearsing the flow once — the skill
says so under `## Limits` rather than shipping a schedule of its own.

## What stays in the container

The `web-checkout` command itself is a **container primitive**, not part of this skill:
`bevo-docker` installs the wrapper and owns `api/scripts/web-checkout.mjs`, and
`bevo-server` mints the browser session (the stealth-browser key never reaches the
container). This repository holds only the how-to. `web-checkout` is a reserved skill name
for that reason — the hub name is `butler-web-checkout`.

## Validate before merging

No Butler account, container or registry checkout needed — the hub publishes its validator
as a standalone file:

```bash
curl -sSLO https://virtual-protocol.github.io/butler-skills/tools/validate.py
python3 validate.py --standalone . --maintainer
```

`--maintainer` is required: `butler-` is the maintainer-reserved namespace. Keep the
downloaded validator out of the commit — `.gitignore` already lists it.

`replay.py` is for skills with a `duty.py` and prints "nothing to replay" here, so CI is a
single step:

```yaml
- uses: Virtual-Protocol/butler-skills/.github/actions/validate@main
  with:
    maintainer: "true"
```
