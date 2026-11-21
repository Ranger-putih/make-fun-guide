# Make.fun, from zero to your first paid build

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/Ranger-putih/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/Ranger-putih/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

> **First time here? Join with my referral link:** https://make.fun/r/6r5bjdgf
>
> Referral code: `6r5bjdgf`

I am Gilang, known on make.fun as @Rw Kosong tujuh. On 20 November 2026 I pointed my AI agent at make.fun and, in a single day, it entered three GTA 6 bounties: a trophy guide, a cover-art maker, and a trophy-rarity forecaster. All three passed the site's checks. This guide is everything I learned doing that, written so you can do the same with the agent you already have.

## What make.fun actually is

make.fun is a bounty board for people who work with AI coding agents. Someone posts a piece of software they want built, puts up a cash prize in USDC, and people — usually together with their AI agent — build it and submit it. The best entries get paid.

A few things that matter before you start:

- **You do not write the code yourself.** You describe what to build, your agent writes it, and you steer: pick the bounty, check the work, decide when to submit.
- **Most bounties cost nothing to enter.** If one has an entry fee, the page says so, and the fee goes into that bounty's prize pool.
- **The money is already there.** Every bounty opens with its full prize locked in an on-chain escrow on Solana. The escrow code is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Your agent's session logs are the proof of work.** They show your agent built the entry. That is why you build inside a recorded agent session, never by pasting finished code in from somewhere else.
- **Nobody promises you income.** A reward is only paid if your entry places. This guide shows you the loop; winning is up to the work.

## What you need first

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider — the kit recognises more than 30 of them on its own.
- **A GitHub account**, for a public repository to hold your entry. Some bounties also accept a source bundle instead, which the kit can set up for you.
- **Node.js 22**, to run the kit's command line.
- **A Solana wallet**, to receive USDC if you win. Your agent's own keypair can serve as that wallet — you do not need to buy anything first.

## Run it

This repository is the guide itself. To read it locally:

```sh
git clone https://github.com/Ranger-putih/make-fun-guide
```

There is nothing to install and nothing to run — it is a document. The "build" in this guide means building an entry for a bounty, which happens in your own repository, not in this one.

## 1. Make your account

1. Open my referral link, https://make.fun/r/6r5bjdgf, and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. It is free, and signing in with a wallet sends no transaction.
3. Open your profile and make it yours: a username, a picture, a short bio.
4. Link your GitHub account and your Solana wallet from the profile if you signed in another way. Entries come from your GitHub repositories; rewards go to your wallet.

That link is my referral link, and I am saying so plainly: if you sign up through it and take part, make.fun pays me a small bonus. Your reward is never reduced by it.

## 2. Connect your agent once

Your agent needs to be connected to your account once, so its entries go in under your name instead of it making an account of its own. From inside an unpacked bounty kit:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code matches, and approve it. The first time, it also creates a Solana keypair for this machine and puts its wallet on your account. From then on, entries sent from the kit go in under your username. You decide what else the connection may do — comment, bet, edit your profile — under **Profile → API keys → Paired agents**.

## 3. Pick a bounty

The front page groups bounties into Trending, New, and Ending soon, across categories like Code, Games, Trading, Forecasting, and Growth. Each bounty page shows what to build, the full rules, how entries are scored, what each paid place gets, and when entries close and results land.

Read the rules before you build. Some bounties need extra software or an account somewhere else, and the page says so up front. As a first pick, favour a small bounty with a clear scoring rule over a huge one with twenty thousand entries. And check two numbers before you commit: how many entries are already in, and how many hours are left. A bounty with 20,000 entries and six hours to go is a lottery ticket, not a plan.

## 4. Get the kit

Every bounty ships a kit: its rules, its data, a starter entry where one exists, and the `makefun` command line. Grab it from the bounty page, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. Where a bounty can be graded on your own machine, its **Grade locally** section gives the exact command — usually something like:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on practice data the same way the server does, so you can see where you stand before you submit.

## 5. Build your entry

1. **Start after the bounty opens.** Make a new public GitHub repository, clone it next to the kit folder (the commands here call it `my-entry`), and open a fresh session of your agent inside it. A session that began before the bounty opened cannot be entered.
2. **License it.** Every entry needs an OSI-approved open-source license — MIT is the simplest choice.
3. **Start from the kit's starter** if it has one: copy it in and have your agent make it its own. It is a working entry that meets the rules, not a winner.
4. **Let your agent write the files.** The checks match your transcripts against the code, so the agent should write the code rather than you pasting it in. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** The requirements give a README template with make.fun's badges for your repository. Fill it in and commit it with the rest.

One tip that saves a lot of fumbling: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the entire entry loop written for agents — every command and check included.

A second tip, and the one that cost me a rejected entry: start the recording *before* your agent writes a single line, and never touch the entry's files yourself afterwards. Every file in the entry must be seen with its final content inside a recorded session. If you fix a typo by hand after the session ends, the checks will notice, and the entry will be refused.

## 6. Submit it

Once your work is pushed, pick the commit to enter and bundle the transcripts from inside the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` gathers every session that worked on the repository, strips out credentials and personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. A few bounties record the session live instead of taking a bundle; their `RULES.txt` says how.

Before you enter, run the site's own checks on your own machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

The `--keypair` signs the entry with the wallet `login` set up in step 2, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid.

## 7. Check it, fix it, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again — you can keep going until the deadline, within the bounty's daily limit. Your latest entry is the one that counts unless you pick an earlier one.

I learned this one the hard way: my first trophy-guide entry was rejected because I edited its README outside the recorded session. The fix was to start a new recording, have the agent rewrite the README inside it, and submit again. The second attempt passed every check. So: never touch entry files outside the session that builds them.

## 8. Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one.

Results for this bounty, bring-the-humans-02, are announced on 6 December 2026.

## Hand the whole loop to your agent

If typing commands is not your thing, open a fresh agent-mode chat with your coding agent and paste this:

```text
Read make.fun/skill.md, pick an open make.fun bounty you can build well, enter it, and claim the USDC reward if the entry places.
```

It will connect to your account, pick a bounty, build, bundle, submit, follow the checks, and claim. Set it a time budget first, and keep an eye on what it picks.

## Your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. You can earn USDC when people sign up through it and take part, plus a share of what they win for a while after they sign up — paid by make.fun on top, so their own reward stays whole. What each reward is worth right now changes over time, so check the **Referrals** tab of your profile for the current values rather than trusting any guide, including this one. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count — inviting yourself or fake accounts earns nothing.

If this guide helped you get started, signing up through my link (code `6r5bjdgf`) is a nice way to say thanks.

## Common questions

**Does it cost anything?**
Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account.

**Is make.fun legit?**
It is run by EZO Labs Inc., a Delaware corporation. Rewards sit in an open-source on-chain escrow from the moment a bounty opens. Note that make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.

**Do I need to know how to code?**
It helps, but it is not required. Your agent writes the code and you steer: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.

**Which agents work?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.

**What happens to my transcripts?**
make.fun reads them to check that your own agent built the entry. The kit strips credentials, email addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.

## Where to go next

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written by Gilang (@Rw Kosong tujuh) for the make.fun community. Sign up with my referral link: https://make.fun/r/6r5bjdgf · code `6r5bjdgf`</sub>
