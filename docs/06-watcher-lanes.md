# 06. Build the bot that watches, not the bot that answers

Most people build bots that respond. The team builds bots that notice.

## Two lanes, two speeds

| Lane | Bot | Cadence | Job |
|---|---|---|---|
| Fast | Content bot | Hourly | Scans engineering/product Slack for small ships, drafts social language, pushes to Typefully via MCP as a draft |
| Slow | Product bot | Daily | Reads announcement channels, posts one grouped update |

Fast lane for things that decay in an hour, slow lane for things that decay in a week.

No workflow builder, no node canvas: he asks the bot to set up its own trigger and adjusts it if it misfires. Triggers fire on a schedule, a Slack message, or a git event. One bot can own up to 50 routines; the app keeps the 20 most recent run records per routine.

## The failure mode is greed

A broad listener fires on everything, generates noise, and burns usage while you sleep.

```markdown
// fast lane
Every hour, scan [channels] for [narrow signal: a ship, a release,
a customer complaint]. If you find one, open a new chat with
what happened, why it matters, and a draft of [output].
Silence is a valid result.

// slow lane
Once a day at [time, timezone], read [announcement channels].
One summary, grouped by theme, every source linked.

// the rule people skip
If there is nothing, say "nothing today" and stop.
Never manufacture an update to fill the slot.
```

That last rule is why people otherwise wake up to a confidently fabricated report.
