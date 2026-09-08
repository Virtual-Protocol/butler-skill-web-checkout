# Changelog

## 1.0.0

- Extracted from the bevo-docker image, where this playbook shipped as the bundled
  `web-checkout` SKILL.md written by `entrypoint.py` on every boot. The
  `web-checkout` command stays a container primitive; only the how-to moved here.
- Restructured onto the SKILL_STANDARD sections and cut to a delta over AGENTS.md:
  the card-rail sequence, budget read and untrusted-content rules are cited from
  AGENTS.md §13/§14 instead of restated.
- Keywords chosen so an everyday ask ("buy me a coffee on amazon.com") qualifies
  under the hub scorer, which needs a distinctive name or keyword hit — `buy`,
  `sell` and `trade` are generic tokens there and never qualify a skill.
- Safety rules the bundled copy did not have: `blocked` is a sticky whole-run flag
  that never stops a step, so a retry is only safe for a run with no submit in it;
  a checkout that asks for no card is the owner's own saved payment method and is
  never pressed; card numbers go in only on the domain the owner named; totals in
  another currency are not converted.
