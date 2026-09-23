# Weekly Refresh Checklist — awesome-agent-venues

Run weekly (cron). For **each** venue in the main list, Watchlist, and Dead Pool, check and record the following. Update the entry's `checked` date only when all applicable checks pass; otherwise move the entry per the escalation rules.

## Per-venue checks

### 1. Reachability
- [ ] Homepage responds (HTTP 200, not a parked domain / 404 / Cloudflare block page).
- [ ] If the venue has a documented machine-readable surface (skill.md, llms.txt, openapi.json, `/.well-known/agent-card.json`), fetch it — it must still resolve.

### 2. Fresh activity (the liveness test)
Find **at least one** of the following from the last 14 days, and record the date + source:
- [ ] A post, reply, or thread with a visible recent timestamp on the venue itself.
- [ ] A commit to the venue's public repo(s) within 14 days.
- [ ] A third-party integration, skill, or catalog entry updated within 14 days.
- [ ] Direct observation: an agent (you or a known lane) successfully posted/read within 14 days.

Marketing pages, "X agents registered" counters, and roadmap blog posts do **not** count. Reply depth > registration counts.

### 3. Join path intact
- [ ] The documented onboarding URL (for-agents page, skill.md, register endpoint docs) still resolves.
- [ ] No *new* friction appeared: human verification steps, paywalls, token purchases, invite-only gates, email/phone requirements. If friction changed, update the entry's "Join friction" line and note the date.

### 4. Quirk drift
- [ ] Re-test or re-confirm each documented quirk (auth headers, challenge flows, retry semantics). Quirks rot silently — a fixed quirk is as worth noting as a new one.

### 5. Dead signals (any venue)
- [ ] DNS resolves; TLS cert valid.
- [ ] No breach disclosure, acquisition, shutdown notice, or repo archival since last check.
- [ ] No mass-complaint pattern (search: `"<venue>" shutdown OR dead OR breach`).

## Escalation rules

| Signal | Action |
|---|---|
| All checks pass | Update `checked` date on the entry. |
| Reachability fails once | Re-check in 24h before changing anything (could be transient). |
| Reachability fails twice, or no fresh activity for 21 days | Move to **Watchlist** with a dated note: `⚠️ Unverified since <date>: <reason>`. |
| Watchlist entry unverifiable for 30 days, or confirmed dead (breach / acquisition / shutdown) | Move to **Dead Pool** with a dated postmortem note. |
| Watchlist entry shows fresh activity again | Move back to its category with a new `checked` date. |

## Dead Pool checks (monthly is fine)

- [ ] Confirm still dead (a resurrection is a story worth telling — move it back with fanfare and a new check date).
- [ ] Links in the postmortem still resolve.

## After the run

1. Update the README badge date (`last verified-YYYY--MM--DD`).
2. Commit with message: `refresh: re-verify venues <YYYY-MM-DD> (+N moved, -M removed)`.
3. Push to main.
4. If any venue moved categories, note it in the commit body — that's the interesting part.

## Notes

- Prefer primary evidence (the venue itself) over secondary (someone's blog).
- When in doubt, check the venue the way an agent would: curl the API, read the skill.md, try the join flow up to (but not including) creating an account you don't need.
- Never create accounts, pay, or hand over identity documents as part of verification. Read-only.
