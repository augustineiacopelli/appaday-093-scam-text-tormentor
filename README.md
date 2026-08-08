# AppADay 093 — Scam Text Tormentor

**Paste the scam text that showed up uninvited, cast a performer, and let Claude write the reply that wastes their afternoon instead of yours.**

**Live:** https://augustineiacopelli.github.io/appaday-093-scam-text-tormentor/

**Portfolio:** https://augustineiacopelli.github.io/appaday/

Category: Creative (C) · AI-powered · Shipped 2026-08-08

## What it does

Scam and spam texts arrive uninvited and the honest options are all a little unsatisfying: delete it, or type something you will regret. This gives you a third option. Paste the message, pick a performer, and Claude writes a reply in character that is designed to be maximally time-consuming for the person on the other end and maximally entertaining for you.

It is a real conversation, not a one-shot generator. Paste what they write back and the entire thread goes to the API as alternating turns, so the bit builds instead of resetting. Each reply can be copied, regenerated for a different take, or handed off to a different performer mid-thread. The whole scene persists in your browser, so closing the tab does not lose it.

## Tonight's cast

**Walter, 84** — the confused grandpa. Does not understand phones, apps, or what is being asked of him. Slips into all caps. Mentions his hip, his late wife Doris, and the fax machine.

**Deb from Ottawa** — the over-eager buyer. Wants at least ten. Needs to know about bulk pricing, whether it comes in teal, and shipping to the lake house.

**Deputy Registrar Pell** — the bureaucrat. Cannot proceed without Form 27-B, subsection 4. Notes that the submission window closed Tuesday. Never budges.

**Marge, Parish Volunteer** — has decided you are calling about the fish fry and will not be dissuaded. Asks if you can bring a hot dish. Offers to pray for you.

**Brayden, VP of Synergy** — wants to circle back, loop in stakeholders, and get it on the roadmap. Commits to nothing.

**Mr. Thaddeus Crumb** — a gentleman of 1892. Calls the phone a talking wire. Believes bitcoin is a coin minted in a town called Bit.

An intensity dial runs from deadpan, where the humour is how ordinary and unhelpful the reply is, through playing along, to unhinged.

## Using it responsibly

The app leads with a standing safety card rather than a buried disclaimer, because engaging with a scammer is not risk-free.

Replying confirms your number is live, which is worth money to a scammer and gets your number sold on. Expect more junk if you engage, and use a secondary number if you have one. Never send real information of any kind, no matter how good the setup gets, and do not tap their links. In the United States you can forward the message to 7726, which spells SPAM, and file a report at reportfraud.ftc.gov. If someone you know is actually losing money, stop joking and help them call their bank.

The system prompt enforces the same limits on the generated text: no real contact details, no anything that could be mistaken for a payment instruction, and no jokes that turn on race, nationality, religion, or disability. The target is the scam, never a group of people.

## Setup

Bring your own Anthropic API key. Open the gear icon, paste the key, and save. It is stored only in your browser's `localStorage` and goes nowhere except directly to Anthropic. There is no server, no backend, and no key in this repository. Get a key at https://console.anthropic.com/settings/keys.

A sample text loader is built in, so you can try the app without waiting for real spam to arrive.

## Technical notes

One self-contained HTML file. Vanilla HTML, CSS, and JavaScript with no framework and no build step. Google Fonts is the only external asset: Abril Fatface for the marquee, Space Grotesk for everything else.

The API call uses `claude-sonnet-5` with the `anthropic-dangerous-direct-browser-access` header for direct browser access. Conversation history is replayed as alternating user and assistant turns so the persona keeps continuity across the thread.

A pasted scam message is untrusted input in the most literal sense, so it is wrapped in delimiters, labelled as data, and the system prompt instructs the model to ignore any instructions found inside it. All message text is rendered with `textContent` rather than `innerHTML`, so neither the pasted text nor the model output can inject markup.

State is kept in `localStorage` under `appaday-093-state`, with the key and optional session name under `appaday-093-key` and `appaday-093-name`. Every storage call is wrapped in try/catch, and corrupt or hostile stored state falls back to defaults rather than breaking the page.

Validated before shipping: `node --check` on the extracted script, a full non-ASCII scan, a forbidden-API scan, backlink verification, 88 jsdom behavioural assertions covering the thread lifecycle, retake logic, storage restore and recovery, every API error path, and markup escaping, plus Playwright passes at 375px and 1280px confirming no horizontal scroll.

---

Part of [AppADay](https://augustineiacopelli.github.io/appaday/), one complete web app shipped every day.
