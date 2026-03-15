---
name: post-event-networking
description: Post-event networking follow-up and relationship management. Use when the user attended an event (hackathon, conference, mixer, meetup, dinner, summit, happy hour) and wants to follow up with new connections. Handles LinkedIn contact scanning, personalized message drafting, LinkedIn message sending, social media post drafting (LinkedIn, Xiaohongshu/小红书, Twitter/X), and follow-up reminders with voice learning. Use when user says "I went to [event]", "scan my new contacts", "networking follow-up", "event follow-up", "draft messages for people I met", "post about [event]", "who did I connect with", or "follow up from [event]". Do NOT use for general LinkedIn browsing or social media posting unrelated to events.
---

# Post-Event Networking

## Workflow

### Step 1: Collect Event Context
Gather (ask if not provided):
- Event name, type (hackathon / conference / mixer / meetup), date(s)

### Step 2: Scan LinkedIn Connections
1. Open LinkedIn connections sorted "Recently added" via browser (`profile=openclaw`)
2. Collect connections added on/after event date (expand ±1 day to catch edge cases)
3. Present numbered list: name, title/company, connected date

### Step 3: Categorize by Action
Ask user to categorize by **what they want to do** (default all to 👋):

- ☕ **Coffee invite** — want to meet IRL. Add user's location-based coffee line.
- 🤝 **Collab** — user provides context: "we talked about X, I want to follow up on Y." Use their answer to write a deeply personalized message.
- 👋 **Stay in touch** — light, friendly, offer to share events. No context needed.

User can say: "Monica — collab, we talked about AI communities. Erwan — coffee. Rest stay in touch."

**Auto-detect Chinese contacts → write message in Chinese.**

### Step 4: Draft Messages
1. Read `references/voice-notes.md` for user's established writing style
2. Draft messages matched to action tier + voice profile:
   - ☕ Coffee: personalized + location-based coffee invite
   - 🤝 Collab: reference actual conversation topics user provided + specific collab ask
   - 👋 Stay in touch: short, warm, offer to share events
3. Present all drafts for review

### Step 5: Choose Send Method
Ask: **"Which ones do you want me to send on LinkedIn, and which do you want to send yourself?"**

Options:
- "send all" → send everything via LinkedIn browser
- "send the warm ones, I'll do collab myself" → send warm, provide collab as text
- "I'll send them all" → just provide drafts
- Specific names → send only those

**CRITICAL: Never send without user explicitly choosing. Stop immediately if user says stop. Report which were sent and which remain.**

#### Sending via LinkedIn
1. Navigate to compose: `linkedin.com/messaging/compose/?recipient=[profileURN]`
2. Type approved message in compose box
3. Click Send
4. Confirm: "✅ Sent to [Name]"
5. Move to next

### Step 6: Draft Social Posts (if requested)
Offer posts for:
- **LinkedIn** — professional recap, tag people, highlight themes
- **Xiaohongshu/小红书** — Chinese, visual/personal, lifestyle angle, hashtags (湾区活动, 科技圈, networking, 硅谷生活)
- **Twitter/X** — punchy, 1-2 takeaways, build-in-public energy

Study recent post trends on each platform before drafting. If user has event photos, suggest using them — especially for Xiaohongshu.

### Step 7: Log and Remind
1. Append event + contacts to `memory/networking.md`
2. Log all drafted messages to `memory/networking-drafts.md`
3. Set **1-month follow-up reminder** via cron for ☕ and 🤝 contacts
4. Include person names, event name, and context in reminder text

### Step 8: Learn from Feedback Loop
After user sends their own messages:
1. Check LinkedIn sent messages via browser, or ask user to paste what they sent
2. Compare drafts vs actual for each contact
3. Update `references/voice-notes.md` with:
   - What user changed (tone, length, phrases, structure)
   - What user kept (validates the draft)
   - New patterns (language switching, emoji preferences, value offers)
4. Apply all learnings to future drafts — the skill gets smarter every time

## Event Log Format (`memory/networking.md`)

```
## [Event Name] — YYYY-MM-DD
Type: hackathon | conference | mixer
Contacts:
- ☕ Name — Title @ Company
- 🤝 Name — Title @ Company — [collab context]
- 👋 Name — Title @ Company
Posts: [links or "pending"]
Follow-up: YYYY-MM-DD
Drafts: see memory/networking-drafts.md
```

## Voice Profile
Before drafting any message, read `references/voice-notes.md`. Key rules:
- Chinese contacts → write in Chinese (casual, use ！and 啊)
- Use 😊 or :D — never 🙌
- Always offer value: "I'll share any fun events I come across"
- Collab messages MUST have conversation context from user — never guess
- Short for stay-in-touch, longer for collab
- Add humor naturally: "haha", ":D"
- Use "hii" for casual/Chinese contacts, "Hey" for others

## Troubleshooting

### LinkedIn not loading
Cause: Browser session expired
Solution: Re-authenticate with `profile=openclaw` or ask user to attach Chrome relay

### Send button disabled
Cause: Message field empty or not focused
Solution: Click into message field first, then type, then click Send

### User aborts sending
Stop immediately. Report which messages were sent and which remain. Never retry without asking.

### No conversation context for collab tier
Do NOT guess or use LinkedIn bio as substitute. Ask user: "What did you talk about with [Name]? What do you want to follow up on?"
