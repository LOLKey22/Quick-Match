# Quick Match – QA Testing

Group 11 · Thura Min Tun · Myint Myat Pyae Sone

Quick Match is checked in two ways:

1. **Automated tests:** code that checks the game rules every time we run `npm test`.
2. **Manual tests:** a checklist we play through by hand on a phone-sized screen.

---

## 1. Automated tests

### Where they are

| File | What it checks |
|---|---|
| [`src/game/test/logic.test.ts`](src/game/test/logic.test.ts) | The game rules in [`src/game/logic.ts`](src/game/logic.ts): scoring, hearts, streaks, speeds, shuffling and stars |
| [`src/test/app-routing.test.tsx`](src/test/app-routing.test.tsx) | The home page (`/`) opens the game rather than a "not found" page |

### How to run them

```sh
npm install
npm test
```

### Test cases and results

| ID | Requirement (from our proposal) | Test | Result |
|---|---|---|---|
| A1 | Right answer: +10 and the streak grows | correct answer gives +10 and increases combo | ✅ Pass |
| A2 | Wrong answer: −1 heart, streak resets | wrong answer removes one heart and resets combo | ✅ Pass |
| A3 | Time-out takes exactly one heart (never two) | timeout removes exactly one heart | ✅ Pass |
| A4 | Easy 5 s, Medium 4 s, Hard 3 s | easy is 5s, medium is 4s, and hard is 3s | ✅ Pass |
| A5 | Every question shows all six fruits | each question shows all six fruits | ✅ Pass |
| A6 | Next target never repeats the last one | a new target never repeats the previous fruit | ✅ Pass |
| A7 | +5 quick bonus with half the time or more left | awards a quick-answer bonus at exactly half the time remaining | ✅ Pass |
| A8 | +10 bonus on every 5th answer in a streak | adds a 10-point bonus on every fifth correct answer in a streak | ✅ Pass |
| A9 | 3 / 2 / 1 stars from hearts kept | assigns 3, 2, or 1 stars based on hearts remaining | ✅ Pass |
| A10 | Reward text such as "+10 Correct · +5 Quick" | spells out each part of the reward without double counting | ✅ Pass |
| A11 | The game page loads | matches a page for / instead of falling back to not found | ✅ Pass |

**Last run:** 20 November 2026, 11 of 11 passed.

```
 Test Files  2 passed (2)
      Tests  11 passed (11)
```

---

## 2. Manual tests

Run the game (`npm run dev`, then open http://localhost:5173/) on a phone or in the browser's phone view. Write Pass or Fail in the Result column.

| ID | Steps | Expected result | Result |
|---|---|---|---|
| M1 | Open the game | Logo, bouncing fruits, Easy / Medium / Hard, Start Game, How to Play, Settings | |
| M2 | Press How to Play, then Back | The rules are shown, and Back returns to the menu | |
| M3 | Open Settings, turn sound off, reload the page | Sound is still off after the reload | |
| M4 | Press Start Game | "3 – 2 – 1 – Go!" plays before the first question | |
| M5 | Look at the cards | Six large fruits in two rows of three, easy to tap | |
| M6 | Tap the right fruit straight away | "+10 Correct · +5 Quick", score +15, card bounces green | |
| M7 | Tap the right fruit near the end of the countdown | "+10 Correct", score +10 | |
| M8 | Get 5 right in a row | "+10 Streak" appears on the 5th answer | |
| M9 | Tap a wrong fruit | Red outline, −1 heart, streak back to 0, the right fruit glows green | |
| M10 | Let the timer run out | Card wobbles, exactly 1 heart lost, the right fruit glows green | |
| M11 | Watch the last 1.5 seconds | The bar turns red and the number pulses | |
| M12 | Play 10 questions | The same fruit is never asked twice in a row | |
| M13 | Press Pause, wait 5 seconds, press Resume | The clock stops and the cards are hidden, then the clock continues from where it stopped | |
| M14 | Try tapping two cards quickly | Only the first tap counts | |
| M15 | Reach 100 points without losing a heart | "Level Complete!" with 3 stars and the personal best | |
| M16 | Lose all 3 hearts | "Game Over" with score and best combo | |
| M17 | Return to the menu after a game | The best score and stars are shown under that level | |
| M18 | Check the browser tab | Apple icon and the title "Quick Match – Find It Fast!" | |

**Tested by:** ____________ **Date:** ____________ **Device:** ____________

---

## 3. Bugs found and fixed during QA

| Bug | Fix |
|---|---|
| Fruit pictures were tiny (16 px) on the game cards | Let the fruit drawings fill each card |
| Reward text counted the quick bonus twice ("+15 Correct · +5 Quick") | Text now shows "+10 Correct · +5 Quick" |
| The correct card faded with the others when the answer was revealed | The correct card stays bright and glows green; the others fade |
| Countdown sometimes stalled, or one miss cost two hearts (first build) | One timer per question, plus a guard so each question resolves once |
