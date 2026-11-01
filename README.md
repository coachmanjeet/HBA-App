# Kitna Jaane Ho Haryana Ne? — HBA Quiz Game

A lightweight, mobile-friendly quiz game for the Haryanvi Bay Area Association.
One HTML file + logo. No server, no signup, no cost.

## How it works

- **Host** opens this page on a laptop / big screen and taps "I'm the Host".
  A QR code appears. Players scan it, enter their name, and tap Join.
- **Players** answer on their own phones. 15 seconds per question.
- **Scoring:** correct answer = 100 points + speed bonus up to 50
  (faster = more points). Wrong answer = 0.
- **Finale:** Top 3 podium + full ranking.
- **Capacity:** no hard cap — built for 50–70 players, extra joiners welcome.
  Late joiners catch up at the current question.

## Live sync — read this

Phones sync through a free public relay (HiveMQ / Mosquitto over secure
WebSockets). Nothing to install, no account. Requirements:

- Venue WiFi must allow internet + WebSockets (most do).
- Host and players all open the same deployed URL (see below).

If the relay is unreachable, the app says so on screen. Fallback that
always works: **Practice Alone** mode — the full game on one phone,
no internet needed. Use it to rehearse, or as a backup on the night.

## Put it on GitHub Pages (2 minutes)

```bash
cd hba-quiz-game
git init
git add index.html logo.png README.md
git commit -m "HBA Haryana quiz game"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo>.git
git push -u origin main
```

Then in the repo on github.com: **Settings → Pages → Source: Deploy from
a branch → main → /(root) → Save**. Your game is live at
`https://<your-username>.github.io/<repo>/`.

The host screen's QR code is generated from the live page URL
automatically, so it always points at the right place.

## Run of show (tonight, ~7-minute slot)

1. Host opens the live URL on the big screen, taps "I'm the Host".
2. Show the QR code. Players scan, enter names, join (lobby counts them).
3. Host taps Start Game. Questions auto-advance: 15s to answer, 5s reveal.
4. After the last question, the Top 3 podium appears on every phone
   and on the host screen.

Current timing: 6 questions = 6 × 20s ≈ 2 minutes of play + lobby.
Adding 4 more questions brings it to ≈ 3.5 minutes + lobby ≈ 5–7 minutes.

## Add or change questions

Edit the `QUESTIONS` array at the top of the `<script>` in `index.html`.
Each entry:

```js
{ q: "Question text?",
  o: ["Option A", "Option B", "Option C", "Option D"], a: 1,
  fact: "One-line fact shown on the reveal screen." },
```

`a` is the index of the correct option (0–3). That is the only place
questions live — no database, no rebuild step.

## Live app

https://coachmanjeet.github.io/HBA-App/

## Second game: Haryanvi Translation Challenge

https://coachmanjeet.github.io/HBA-App/quiz2.html

5 Haryanvi-to-English translation questions, same engine, separate room code
(HBA2026Q2) so it never collides with the main quiz.
