# butler-web-checkout

Buy, order or book on a real website — the merchant kind that blocks bots — with a stealth
browser, a login that survives between runs, email/SMS two-factor, and a single-use card at
checkout.

One Butler skill. The [Butler Skill Hub](https://github.com/Virtual-Protocol/butler-skills)
lists this repo in its `skills.json` and re-resolves the ref every build, so a merge here
reaches Butlers on the next one.

- `SKILL.md` — the playbook; sections and frontmatter per the hub's
  [SKILL_STANDARD.md](https://github.com/Virtual-Protocol/butler-skills/blob/main/SKILL_STANDARD.md)
- `CHANGELOG.md` — one line per version; every change bumps `version` in SKILL.md

No `duty.py`: `modes: ["one-off"]`. A standing order is a duty built with `bevo-automation`,
and `## Limits` says so instead of shipping a schedule here.

`web-checkout` itself is a **container primitive**, not part of this skill: `bevo-docker` owns
`api/scripts/web-checkout.mjs` and `bevo-server` mints the browser session. This repo holds
only the how-to — hence the reserved name; the hub name is `butler-web-checkout`.

## Validate before merging

```bash
curl -sSLO https://virtual-protocol.github.io/butler-skills/tools/validate.py
python3 validate.py --standalone . --maintainer
```

`--maintainer` is required: `butler-` is the maintainer-reserved namespace. Keep the
downloaded validator out of the commit — `.gitignore` already lists it.

`replay.py` needs a `duty.py` and prints "nothing to replay" here, so CI is a single step:

```yaml
- uses: Virtual-Protocol/butler-skills/.github/actions/validate@main
  with:
    maintainer: "true"
```
