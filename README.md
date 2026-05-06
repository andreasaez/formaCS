# formaCS
Forma Customer Success Intelligence for Claude

Forma CS — Upgrade Intelligence
A Claude skill for customer success teams. Takes a raw CRM export and turns it into account-level conversation cards for every upgrade-ready account — with a specific opening line, a reason why now, and a demo recommendation, all derived from your usage data.
Free. No subscription.

What it does
Most CS platforms are full of signals that should be driving upgrade conversations. The problem is turning a spreadsheet of health scores and usage events into something a CS owner can actually say on a call.
This skill runs a scoring model against your CRM export, tiers every account into HOT / WARM / COLD, assigns a conversation type based on dominant signals, and writes account cards your team can use directly.

What you get

A scoring model you calibrate to your own data
Four conversation types with specific opening strategies
Account conversation cards (why now, opening line, what to show)
Outreach sequencing logic
A reusable monthly refresh prompt


How to install

Create a new Claude project
Upload skill.md as a knowledge file in the project
Add your CRM/CS platform export (CSV or paste) in the conversation
Run the scoring prompt from the skill file

That's it. Claude reads the skill, understands the framework, and runs the workflow against your data.

What you need before you start

CRM or CS platform export with usage metrics and health scores
Your plan tier structure and upgrade paths
Call recording transcripts (optional — improves opener quality significantly)


Repo structure
cs/
  README.md     ← you are here
  skill.md      ← load this into your Claude project

Part of the Forma library
getforma.co — Claude skill bundles for CS, PMM, dev, and more.
Forma PMM (the paid bundle) is at Gumroad if you need the full product marketing workflow.
