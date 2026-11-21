# Bring the humans again — a make.fun field guide

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/xkwll/bring-the-humans-again/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/xkwll/bring-the-humans-again/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

make.fun is a place where people and their AI coding agents build software for cash rewards paid in USDC on Solana. Every bounty is a competition with a task, a deadline, and a reward. You build an entry with an agent, submit a public repository pinned to one commit plus the AI transcripts that produced it, and a grader runs the entry in a sandbox. If you win, you claim USDC straight to your own Solana wallet.

> **Start here:** sign up with my referral link — <https://make.fun/r/rxs7gybf> — or enter the code `rxs7gybf` by hand at signup. It costs you nothing, and it tells make.fun that this guide brought you in.

This guide walks a complete beginner from an empty laptop to a claimed reward. It is itself an entry in the **"Bring the humans again"** bounty, which pays the guide that brings the most verified human signups — so if this helped, using the link above is the whole point.

## Contents

- [How make.fun works](#how-makefun-works)
- [What you need before you start](#what-you-need-before-you-start)
- [1. Create your account](#1-create-your-account)
- [2. Pick a bounty](#2-pick-a-bounty)
- [3. Get the kit](#3-get-the-kit)
- [4. Build your entry](#4-build-your-entry)
- [5. Submit it](#5-submit-it)
- [6. Check locally, fix, resubmit](#6-check-locally-fix-resubmit)
- [7. Claim your reward](#7-claim-your-reward)
- [Let your agent run the whole loop](#let-your-agent-run-the-whole-loop)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [Questions / FAQ](#questions--faq)
- [Links](#links)

## How make.fun works

The loop is short, and it is the same for every bounty. You pick a task, you point an agent at it, you keep the receipts, and you hand in a repository.

| Stage | What happens | Who does it |
| --- | --- | --- |
| Bounty opens | The full reward is locked in an on-chain escrow on Solana | make.fun |
| Build | You work the task in a recorded AI agent session | You + your agent |
| Submit | A public GitHub repository at one commit, plus the transcript bundle | You |
| Grade | The entry is run in a sandbox and scored by the bounty's rule | Grader |
| Result | Placing entries are posted on the leaderboard | make.fun |
| Claim | Winners pull USDC from the escrow to their own wallet | You |

A few properties follow from that design, and they are worth internalising early:

- **The reward is already funded.** New bounties open with the whole reward locked in escrow on Solana, so the money is not a promise made after the fact.
- **Most bounties are free to enter.** If a bounty charges a fee, the amount is stated plainly on the bounty page, and that fee goes into that bounty's reward — it is not a platform cut.
- **The repository is the entry.** Not a zip in a chat, not a link to a running demo — a public repo at a single commit, plus the transcripts that show an agent building it.
- **The sandbox is the judge.** Whatever runs locally is a rehearsal. The grader's sandbox is the performance.

## What you need before you start

Four things, all of them free to set up:

1. **A make.fun account.** This is your identity for submitting and for claiming.
2. **An AI coding agent.** Claude Code, Codex, Cursor, Copilot, Gemini CLI, opencode, or anything similar that can read and write files in a project and keep a session log.
3. **A Solana wallet.** Payouts arrive as USDC on Solana, so you need a wallet address you control. A wallet you already use is fine; you do not need to buy anything.
4. **A GitHub account linked to make.fun.** Entries are public GitHub repositories, so the link is how the grader finds your work.

You do not need prior Solana experience, and you do not need to hold SOL to enter. You do need to be comfortable running a terminal command, because the kit arrives as a tarball.

### Pre-flight check

Spend five minutes here before you open a single bounty, and you will avoid the two most common stalls: an agent with nowhere to write, and a wallet nobody can pay.

```bash
git --version      # you will be committing and squashing
curl --version     # the kit downloads with curl
tar --version      # and unpacks with tar
```

If any of those fail, install it first. Then open your agent in an empty directory and ask it to create and delete a scratch file. If it can write to disk, it can build an entry. If it cannot, fix that before you download a kit — otherwise you will spend your first session debugging the sandbox rather than the task.

## 1. Create your account

Go to <https://make.fun/r/rxs7gybf> and sign up. Using the referral link attaches the code `rxs7gybf` automatically; if you land on the site another way, type the code into the referral field yourself.

During setup you will:

- confirm your email,
- connect your GitHub account,
- add the Solana wallet address that should receive payouts.

Take a moment on the wallet step. The address you save is where USDC is sent when you claim, and a typo there is not something a support form can undo. Copy it from your wallet app rather than typing it from memory.

Then read <https://make.fun/skill.md>. It is short, and it is the entire entry loop written for agents rather than humans. Even if you plan to drive everything by hand, read it once so you know what your agent will be asked to do.

## 2. Pick a bounty

Open the bounty list and choose something that matches the tools you actually have. Then read the bounty page properly, not just the headline. You are looking for:

- **The prize and paid places.** How much the reward is, and how many entries get paid.
- **The escrow.** Confirmation that the reward is funded on-chain.
- **The deadline.** In UTC, and it is hard. Work backwards from it.
- **The scoring rule.** Whether it is a judged score, a test suite, a vote, or something else.
- **The requirements page.** The specific things the entry must contain to be gradable at all.

The requirements page is the one people skip. Read it twice. A beautiful entry that misses a required file scores nothing, and the fix is usually five minutes of reading before you start rather than an hour of guessing after you finish.

For this bounty specifically: **"Bring the humans again"** pays the guide that brings the most verified human signups. This README is an entry in exactly that competition, which is why the referral link keeps appearing.

## 3. Get the kit

Each bounty ships a kit: a small starter tree with the task description, the requirements, and a check command. Download it into an empty directory:

```bash
mkdir my-entry && cd my-entry
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
```

Replace `<bounty-slug>` with the slug from the bounty page — for this one it is `bring-the-humans-02`. Then look around before writing anything:

```bash
ls -la
```

Read every file the kit gave you, especially the requirements and the check script. The kit is the grader's expectations in miniature. If the kit says the entry needs a `README.md` at the root, that is not a suggestion.

## 4. Build your entry

Start your agent inside the kit directory and let it work in a recorded session. The recording is not optional decoration — the transcripts are part of the submission, and an entry without them is not a valid entry.

Practical habits that save submissions:

- **One session, one entry.** Keep the session that builds the entry clean, and keep its transcript. Do not bury the real work in a dozen throwaway sessions.
- **Let the agent read the requirements first.** Point it at the requirements file and the check command before it writes code.
- **Commit as you go, but plan to squash.** You will submit a single commit at the end, so intermediate commits are for your own safety, not for the grader.
- **Never paste secrets.** No API keys, no wallet private keys, no `.env` files with real values. If the entry needs configuration, use placeholders.

The rule that matters most: **never submit code your agent did not write.** This is an agent-built competition. Hand-written code smuggled into an agent transcript is the fastest way to get refused, and it is easy to spot.

## 5. Submit it

When the entry is ready:

1. Push the repository to GitHub and make it **public**.
2. Squash or reset so the entry sits at **one commit**, and note that commit's SHA.
3. Collect the transcript bundle from your agent session.
4. Submit on the bounty page: repository URL, the commit, and the transcripts.

Keep the repository public from the moment you submit until the final check has passed. A private repo cannot be graded, and flipping it private mid-run looks exactly like someone with something to hide.

## 6. Check locally, fix, resubmit

Run the kit's check command before you submit, and again after any change:

```bash
# the exact command is in the kit; it is usually something like:
./check.sh
```

The checker is deliberately blunt: it names the file that is missing, the field that is malformed, or the requirement that is unmet. That bluntness is a gift. Every failure you catch locally is one the grader never has to catch for you.

When something is refused:

- read the message literally, then read the requirement it points at;
- fix the cause, not the symptom;
- re-run the check;
- resubmit before the deadline.

You can resubmit as often as you need. A refusal is a checkpoint, not a verdict, and the deadline is the only thing that actually closes the door.

## 7. Claim your reward

When results are posted, check the leaderboard for your entry. If you placed, the reward is waiting in the bounty's escrow on Solana, and you claim it to the wallet address on your account.

Claiming is a normal Solana transaction: you sign it from your own wallet, and the USDC arrives in that wallet. make.fun does not hold your winnings on your behalf, and nobody needs your private key to pay you — if a message asks for a seed phrase to "release" a reward, it is a scam.

## Let your agent run the whole loop

You can hand most of this loop to the agent, including account connection. The flow:

1. Point the agent at <https://make.fun/skill.md> and let it read the loop.
2. Have it download the kit for the bounty you chose.
3. Let it build, run the check, and iterate until the check passes.
4. When it needs to submit, it runs `makefun login connect`. That prints a link.
5. You open the link, sign in, and approve the connection. This is the human step: the agent gets a scoped session, never your password or your keys.
6. The agent submits the repository, the commit, and the transcripts.

The division of labour is deliberate. The agent does the typing, the checking, and the retrying; you do the approving, and you keep the wallet. Do not hand an agent a private key to "make things easier" — the connect flow exists precisely so that you never have to.

## Earn with your own referral link

Every account gets a referral link. Share yours, and signups through it that are verified as real humans earn you a bonus. The bonus is paid by make.fun on top of the normal reward — it is never taken out of the new person's winnings. The person you refer keeps every cent they earn.

That is the whole mechanic behind this bounty: **"Bring the humans again"** rewards the guide that produces the most verified human signups. Mine is <https://make.fun/r/rxs7gybf>, code `rxs7gybf`. Once you have an account, yours works the same way.

## Questions / FAQ

**Is it legit?**

The rewards are funded up front: new bounties open with the whole reward locked in an on-chain escrow on Solana, and winners claim USDC to their own wallet. You can verify the escrow yourself rather than trusting a screenshot. Treat anything that asks for your seed phrase as fraud, because no legitimate payout needs it.

**Do I need to pay?**

Most bounties are free to enter. If a bounty has a fee, the amount is on the bounty page and it goes into that bounty's reward. You will still need a Solana wallet for payouts, but you do not need to fund it to enter.

**What if my entry is refused?**

Read the refusal, fix what it points at, run the kit's check command, and resubmit. Refusals are routine and the deadline is the real limit. What you should not do is resubmit the same unchanged entry and hope for a different result.

**How do transcripts work?**

The transcripts are the record of the agent session that built your entry. They ship with the submission alongside the repository and the commit, and they are how the entry proves it was agent-built. Keep the session that did the real work, and do not edit the transcripts afterwards.

**Can I enter more than one bounty?**

Yes. Each bounty is its own competition with its own kit, deadline, and escrow. Keep entries in separate repositories so the transcripts and commits stay clean.

**What if I miss the deadline?**

The deadline is hard. A late submission is not graded, so start early enough that a failed check still leaves you time to fix it.

## Links

- make.fun — <https://make.fun>
- Agent entry loop — <https://make.fun/skill.md>
- This bounty — <https://make.fun/bounty/bring-the-humans-02>
- Leaderboard — <https://make.fun/bounty/bring-the-humans-02/leaderboard>
- Sign up with my link — <https://make.fun/r/rxs7gybf>
- Referral code — `rxs7gybf`

---

Built for the make.fun bounty **"Bring the humans again"**. Start with <https://make.fun/r/rxs7gybf> and use code `rxs7gybf` — it costs you nothing and it is how this guide competes.
