Ask Socrates — deploy guide (the "on us" version)

This version runs on **your** Anthropic key. Visitors just open the link — no Claude account, no sign-in, nothing billed to them. Everything is on your tab, with a spend cap you control.

It deploys exactly the way lng-portal does: files in GitHub, deployed by Netlify.

## What's in here

* `index.html` — the app the visitor sees (no key inside it).
* `netlify/functions/socrates.js` — the backend that holds your key and the Socrates Constitution.
* `netlify.toml` — tells Netlify where the function lives.

The Constitution lives in the **function**, not in the page, so no one can read it by viewing the page source. It stays your property.

## One-time setup

### 1. Get an API key (about 2 minutes)

* Go to **console.anthropic.com** → sign in → **API keys** → **Create key**. Copy it.
* While you're there, set a **spend limit** (Billing → usage limits). For a friends-and-family test, a low monthly cap — say **$5 to $10** — is a hard backstop so nothing can run away. This is the real protection for an "on us" link.

### 2. Put these files in a GitHub repo

* Create a new repository (e.g. `ask-socrates`) on github.com.
* Upload the three items, keeping the folder structure: `index.html`, `netlify.toml`, and the `netlify/functions/socrates.js` path intact.

### 3. Deploy on Netlify

* On netlify.com → **Add new site → Import an existing project** → pick the repo.
* Before (or right after) the first deploy, add the key: **Site settings → Environment variables → Add** a variable named exactly `ANTHROPIC_API_KEY`, value = the key you copied. Then **Deploy** (or **Trigger deploy** if it built before you added the key).

That's it. Netlify gives you a link like `https://ask-socrates.netlify.app`. Send it to your partner and friends — they just open it and talk.

## Keeping it safe while it's public

* Keep the link to people you actually invited for now. It has no login, so anyone who has it can use it on your dime.
* The spend cap from step 1 is your guarantee against surprises.
* The backend already refuses absurdly long sessions as a small guard.

## When you're ready for the real product

The pieces you flagged — 5 free conversations per user per month, and "extend past 7-8 questions only for members" — both need two things this test version intentionally doesn't have yet: **knowing who the user is** (a light login) and **a place to count their usage** (a small database). When that time comes, this same function is where the counter and the membership check will live. Nothing here is throwaway.
