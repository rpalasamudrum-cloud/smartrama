# smartRama

A daily five-question quiz with two packs, **Ramayana** and **Bollywood** — four choices per question.

| File | What it is |
| --- | --- |
| `index.html` | Landing page |
| `ramayana.html` | The Ramayana pack |
| `bollywood.html` | The Bollywood pack |

Every file is fully self-contained: no build step, no dependencies, no server code. Open one in a browser and it works, online or off. The only network request is a Google Fonts stylesheet, which falls back to Georgia if it can't be reached.

Both packs are published. The Bollywood bank's dates, award years and superlative claims were checked against sources on 9 August 2026; the notes are in `held-back-bollywood/README.md` in the working directory.

## How the game works

- **Today's five** — the daily set, chosen deterministically from the date. Everyone playing on the same day gets the same five questions, in the same order, with the same answer positions. Resets at local midnight.
- **Unlimited** — endless rounds. A question won't repeat until the bank is used up.
- **Scoring** — easy 10, medium 15, hard 25. Each round is 2 easy + 2 medium + 1 hard, so 75 points are available.
- Streaks and all-time points are saved in the browser and count daily rounds only.
- Keyboard: `1`–`4` to answer, `Enter` to advance.

---

## Published site

Served by GitHub Pages from the `main` branch, `/ (root)`:

- <https://rpalasamudrum-cloud.github.io/smartrama/> — landing page
- <https://rpalasamudrum-cloud.github.io/smartrama/ramayana.html> — the pack directly

To publish changes, commit and push to `main`; Pages redeploys on its own.

```
git add -A && git commit -m "..." && git push
```

### Troubleshooting

**404 after enabling Pages** — `index.html` must sit at the top level of the repo, not inside a subfolder.

**Changes don't show up** — hard-refresh (`Ctrl/Cmd + Shift + R`), or wait a couple of minutes. The **Actions** tab shows deploy status.

**Streak reset itself** — streaks live in browser local storage, so they are per-device and per-browser. Incognito windows won't keep them.

---

## Editing the questions

Each HTML file has its bank near the top of the `<script>` block as a `const BANKS = {...}` object:

```js
{
  "q": "Who composed the original Sanskrit Ramayana?",
  "a": "Valmiki",                                  // correct answer
  "w": ["Vyasa", "Tulsidas", "Kalidasa"],          // three wrong options
  "d": "e",                                        // difficulty: e | m | h
  "e": "Sage Valmiki wrote the Adi Kavya ..."      // shown after answering
}
```

The correct answer is always stored as `a` and shuffled into position at runtime, so there is no answer key to keep in step.

Keep at least 2 easy, 2 medium and 1 hard. A bigger bank means more days before questions come around again, but adding or removing any question reshuffles which ones land on which date — that is expected, not a fault.

After editing, run the verifier from the parent working directory. It checks structure, determinism, the tier mix and the option shuffling directly against the shipped files:

```
/System/Library/Frameworks/JavaScriptCore.framework/Versions/A/Helpers/jsc verify5.js
```

---

## Design

The look is deliberate and should be kept: no emoji, no gradients, no drop shadows. Flat warm paper, hairline rules, real typography (Cormorant Garamond and Spectral, falling back to Georgia), answer options set as a printed list with roman numerals rather than boxed buttons. The verifier fails the build if an emoji, gradient or box-shadow reappears.

## Related

**Hindu Mythology** is a separate repository: <https://github.com/rpalasamudrum-cloud/mythology-quiz>. A **Bible** pack was prototyped and set aside; its bank is preserved in the working directory as `bible-pack.js`. Neither is referenced anywhere in these files.
