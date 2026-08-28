# 🎯 Setting up your own Quality of Hire dashboard, via Claude Code

This template ships with no real company data, every step below tells you
what to fill in for *your* organisation. Do these in order; each one gives
Claude what it needs for the next.

## ✅ Before you start

You'll need, in your own Google/Slack accounts:

- Google Drive connected in Claude (claude.ai → Settings → Connectors)
- Slack connected in Claude, for the same workspace you want check-ins sent in
- Three Google Forms (30-day / 90-day / 365-day check-in surveys) with
  auto-populating "(Responses)" Sheets — or tell Claude you want it to help you
  build these from scratch first. You will need to structure the surveys properly (this will take 90 mins approx - I based the survey questions on the 'Values' of the company (shout if you need this described in more detail) 
-GoogleSheet with hiring data (new starter names, start date, line manager, source of hire / internal/external) 

If you don't have the Forms/Sheets yet, say so up front — step 1 below covers
building them before the rest of the setup makes sense.

## 1️⃣ Open the repo in Claude Code and describe your org

Clone this repo, open it in Claude Code, and say something like:

> I want to set this Quality of Hire dashboard up for [Company Name]. Here's
> my rubric / survey questions: [paste or describe them]. My hires are tracked
> in [describe your source — a spreadsheet, an ATS export, etc].

Claude will read `CLAUDE.md` in this repo automatically and know the shape of
what it's building toward.

## 2️⃣ Give Claude your three response sheets

For each of the 30/90/365-day "(Responses)" Sheets, tell Claude the file name
or share a link so it can find the file ID via the Google Drive connector.
Claude will drop these into the `RESPONSE_SHEETS` config block in the
dashboard's script — nothing else needs to change by hand.

## 3️⃣ Give Claude your hire roster

Paste or describe your current/upcoming hires: name, role, manager, start
date, and whether each is internal or external. Claude will build the
`roster` array from this. If your roster lives in a live spreadsheet, be
aware this becomes a **hardcoded snapshot** — the dashboard doesn't
auto-sync from your source sheet, so tell Claude whenever the roster changes
and it'll update the array by hand.

## 4️⃣ Decide your voiding rules

Tell Claude if there are hires/situations you don't want surveyed — e.g.
"never survey internal hires" or "these three hires' windows already passed
before we started tracking, void them." Claude will encode these as either a
blanket rule (like the internal-hire policy) or a per-hire `voidMilestones`
override.

## 5️⃣ Publish the dashboard as an Artifact

Ask Claude to publish it. It'll declare the Google Drive `mcp` capability so
the live "Completed" status and satisfaction charts poll your real response
sheets automatically, no redeploy needed as responses come in.

## 6️⃣ Set up the Slack automations (optional) 💬

If you want automated check-in messages (to hiring managers, and/or to new
hires directly), tell Claude the cadence you want (e.g. "30/90/365 days to the
manager, plus a casual check-in to the hire themselves at day 2"). Two things
worth knowing before this step:

- **Always test wording in your own Slack DM first**, before it goes anywhere
  near a real manager or hire. Say so explicitly — don't assume Claude will
  send live without asking.
- New hires' Slack accounts often don't exist until their actual start date.
  Claude will need a **recurring cloud routine** (via the `schedule` skill),
  not a one-off scheduled message, so it can look up each person once they've
  actually joined.

## 7️⃣ Keep it maintained 🔧

Two things need manual upkeep going forward, since neither is auto-synced:

- **The roster** — tell Claude whenever a hire is added, removed, or changes
  (manager, start date, etc.)
- **Any cloud routine's hire list**, if you set up Step 6 — same reason.

Everything else (response status, satisfaction charts, "Completed" tab) is
live and self-maintaining once the sheets are connected.

> ⚠️ **Note:** this version references a `CLAUDE.md` file that doesn't exist
> yet (Step 1) and the sanitized dashboard HTML itself. If you're just pasting
> this in as a reference doc for now, that's fine — but if you want the repo
> to actually work end-to-end, those two pieces still need building. Let me
> know if you'd like those done too.

---

## 🤝 Collaboration

The whole thing was a 24 hour build approx. I keep interating it slightly, but overall happy with the output so far.

If you've got questions, want a hand adapting this to your own setup, or just want to
talk through build and implementation? Feel free to reach out — happy to
discuss. I can also send you some confidential screengrabs of the 'look and feel' if you wish. 

Best wishes,
