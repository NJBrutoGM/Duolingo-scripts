<div align="center">

<img src="https://assets.duohacker.io.vn/images/DuoHacker_Logo_NoBG_PNG.png" alt="DuoHacker" width="180">

# Duolingo DuoHacker

**Farm XP, Gems and Streaks. Unlock Duolingo Max. Solve lessons automatically.**

![Version](https://img.shields.io/badge/version-2026.08.28-0A84FF?style=flat-square)
![License](https://img.shields.io/badge/license-BY--NC--ND%204.0-34C759?style=flat-square)
![Platform](https://img.shields.io/badge/platform-Chrome%20%7C%20Firefox%20%7C%20Edge%20%7C%20Safari%20%7C%20Opera%20%7C%20Brave-FF9500?style=flat-square)

[Website](https://duohacker.io.vn) · [Discord](https://duohacker.io.vn/discord) · [GitHub](https://duohacker.io.vn/github) · [Donate](https://duohacker.io.vn/donation#choose)

</div>

---

## Overview

DuoHacker is a single-file userscript that adds a floating control panel to [duolingo.com](https://www.duolingo.com). It talks directly to Duolingo's own web endpoints using the session token already present in your browser — no password, no separate server, no install outside your userscript manager.

Everything runs locally in the page: network calls go to `duolingo.com`, `stories.duolingo.com`, `goals-api.duolingo.com` and the leaderboard API, and all settings live in your browser's `localStorage`.

**Default panel language:** Tiếng Việt. English, Español and Français can be selected from the language menu at the top center of the page.

---

## Features

### Farm

| Feature | Modes | Notes |
| --- | --- | --- |
| **XP Farm** | `#` amount · 🕐 minutes · `∞` infinite | Farms in chunks of up to 499 XP and reconciles the final total against the server |
| **Gem Farm** | `∞` until stopped | Claims pending `SKILL_COMPLETION` rewards in parallel and verifies the gem delta through the API |
| **Streak Farm** | `#` days · 🕐 minutes · `∞` infinite | Backfills daily sessions with timezone-correct start/end timestamps |
| **Practice Farm** | `#` lessons · `0` = unlimited | Navigates to `/practice`, solves each lesson, resumes automatically after reloads |
| **Auto League** | target rank | Joins a league if needed, then farms XP until it overtakes the rank above your target |
| **Auto Daily Quest** | one click | Completes every unearned daily goal in a single batched update |
| **Monthly Quest** | one click / per-quest | Lists quests by month with progress bars and injects the missing progress |

### Extras

- **Shop Items** — browse the shop by category and claim items (streak freezes, XP boosts, hearts, outfits, Super 3 Days).
- **Free Duolingo Max** — client-side flag that makes the web app report an active subscription. Reload to apply.
- **Hide Profile** — toggles Duolingo's `disable_social` privacy setting directly.
- **Account Manager** — save the current account and switch between saved accounts from the panel.
- **Leaderboard** — read-only view of your cohort with medals, promotion zone and XP.
- **Reactions** — equip any league or course reaction on your leaderboard entry.

### Lesson tools

- **Auto Solver** — injects `SOLVE` / `SOLVE ALL` buttons into lessons and practices. Handles choice, translate, word bank, pairs, cloze, table, syllable, listen, speak, story and character-writing challenges.
- **Lesson Shortener** — replaces a lesson with a single instant challenge.
- **Stories Shortener** — strips challenges from stories so they can be clicked through.
- **Hide Animation** — hides Duolingo images, videos, canvases and Lottie animations.
- **Safe Mode** — multiplies click delays (2.5× + jitter) and types text word-by-word to look more human.
- **Loop delay** — global pacing between farm iterations (default `500 ms`).

### Panel

- Connection state is mirrored in three states: connecting, connected, and **outdated** (click it to open GreasyFork).
- Profile row with live XP / gems / streak counters, updated as each farm runs.
- Animated page transitions, collapsible panel (`Hide` / `Show`), stacked toast notifications.
- Full keyboard support on inputs — `Enter` starts a farm.

---

## Requirements

- A desktop browser: **Chrome 120+**, **Firefox 120+**, **Edge**, **Opera**, **Brave**, or **Safari** via the Userscripts app.
- A userscript manager (see below).
- An account logged in at `duolingo.com` or `duolingo.cn`.
- The script needs two grants: `GM_xmlhttpRequest` (cross-origin API calls) and `GM_addStyle` (panel styling). If `GM_xmlhttpRequest` is unavailable, it falls back to same-origin `fetch`.

Mobile browsers are supported on a best-effort basis: same-origin requests move to `fetch`, but most mobile userscript managers do not implement the required grants.

---

## Installation

### Option 1 — Tampermonkey (recommended)

1. Install the Tampermonkey extension for your browser:
   - [Chrome / Brave / Edge / Opera](https://chromewebstore.google.com/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo)
   - [Firefox](https://addons.mozilla.org/firefox/addon/tampermonkey/)
2. Open the script page on GreasyFork: **<https://greasyfork.org/en/scripts/561041-duolingo-duohacker>**
3. Click the green **Install this script** button.
4. Tampermonkey shows a confirmation page — review the permissions and click **Install**.
5. Open or reload <https://www.duolingo.com>.
6. The blue **Hide** button appears in the bottom-right corner. Click the gear icon to open settings.

### Option 2 — Violentmonkey

1. Install [Violentmonkey](https://violentmonkey.github.io/get-it/) for Chrome, Firefox or Edge.
2. Open the GreasyFork page linked above and press **Install this script**.
3. Approve the install prompt.
4. Reload Duolingo.

### Option 3 — Greasemonkey (Firefox)

1. Install [Greasemonkey 4+](https://addons.mozilla.org/firefox/addon/greasemonkey/).
2. Greasemonkey 4 sandboxes scripts by default, so enable `GM_xmlhttpRequest`-capable mode: in `about:addons` → Greasemonkey → **Preferences**, make sure scripts are allowed to run on `duolingo.com`.
3. Install from GreasyFork, then reload Duolingo.

> If API calls fail under Greasemonkey, switch to Tampermonkey or Violentmonkey — Greasemonkey's cross-origin implementation is more restrictive.

### Option 4 — Safari (Userscripts app)

1. Install the [Userscripts](https://apps.apple.com/app/userscripts/id1463298887) app from the Mac App Store (or iOS App Store).
2. Enable it in **Safari → Settings → Extensions** and grant it access to `duolingo.com`.
3. Open the GreasyFork page in Safari and press **Install this script**.
4. Reload Duolingo. Because Safari has no `GM_xmlhttpRequest`, the script automatically uses `fetch` with `credentials: 'include'`.

### Option 5 — ScriptCat / other managers

Any manager that supports `GM_xmlhttpRequest` + `GM_addStyle` and exposes `unsafeWindow` will work. Import the `.user.js` file directly from GreasyFork or the GitHub raw URL.

### Manual installation (from this file)

1. Open your manager's dashboard → **Utilities** (Tampermonkey) or **+** (Violentmonkey).
2. Choose **Import from file** and select `DuoHacker.js`.
3. Save, then reload Duolingo.

---

## First run

1. **Connect.** The top row of the panel shows `Connecting` → `Connected`. It reads the `jwt_token` cookie already set by Duolingo and fetches your profile.
   - `Not logged in` means the cookie is missing: log in on duolingo.com and reload the page.
   - `Outdated` in orange means a newer version exists on GreasyFork — click it to open the install page.
2. **Pick a language** with the flag button at the top center (`VI` / `EN` / `ES` / `FR`). The choice is remembered.
3. **Set your pacing.** Open the gear icon → **Loop delay (ms)**. `500` is the default. Slower values (e.g. `800`–`1500`) reduce the chance of rate limiting.
4. **Enter a value and press the blue button.** The button turns red and reads `STOP` while running; press it again to stop and keep what was already earned.
5. **Watch the notification stack** at the bottom of the page for per-farm results.

### Mode button

Each farm input has a square button on its left that cycles the input's meaning:

| Icon | Mode | Input |
| --- | --- | --- |
| `#` | Target amount | XP (min 30, max 500,000) or streak days (1–3,650) |
| 🕐 | Time | Minutes to run, with a live progress bar |
| `∞` | Infinite | Runs until you press `STOP` |

---

## Settings reference

| Setting | Default | What it does |
| --- | --- | --- |
| Loop delay (ms) | `500` | Pause between farm iterations. Saved in `localStorage` as `dh2_delay` |
| Free Duolingo Max | off | Makes the web app report `hasPlus: true` and injects a permanent `gold_subscription` shop item. Client-side only — reload to apply |
| Hide Profile | off | Writes the `disable_social` privacy setting on your account |
| Auto Solver | off | Shows `SOLVE` / `SOLVE ALL` during lessons and practices |
| Hide Animation | off | Hides Duolingo images, videos, canvases and Lottie players via injected CSS |
| Lesson Shortener | off | Replaces newly created sessions with one instant challenge |
| Stories Shortener | off | Removes challenges from story payloads |
| Safe Mode | off | 2.5× + random click delays, word-by-word typing |

### Auto Solver shortcuts

| Shortcut | Action |
| --- | --- |
| `Ctrl/Cmd + Enter` | Solve the current challenge once |
| `Ctrl/Cmd + Shift + Enter` | Toggle continuous solving (`SOLVE ALL` / `PAUSE`) |

Continuous solving stops automatically if the URL changes.

---

## How it works

The script installs two independent fetch layers:

1. **Page context** — an injected `<script>` wraps `window.fetch` and `XMLHttpRequest` to serve the client-side features that React itself requests: the free-Max profile patch, story shortening, and lesson shortening. It only activates while the matching toggle is on in `localStorage`.
2. **Sandbox** — a wrapper around `unsafeWindow.fetch` handles `POST /2023-05-23/sessions` for lesson creation and re-installs itself if Duolingo replaces `fetch` (checked every 2 s and on navigation).

Farm calls go through `GM_xmlhttpRequest` with an explicit `Authorization: Bearer <jwt>` header; on mobile or managers without that grant they fall back to credentialed `fetch`.

State is local only:

```
dh2_lang  dh2_delay  dh2_super  dh2_shop  dh2_accounts
dh2_lessonShortener  dh2_storiesShortener
duohacker_safe_mode  duohacker_inject_solver  duohacker_hide_animation
sessionStorage: dh2_practice
```

`dh2_accounts` stores saved accounts **including their JWT** in plaintext in `localStorage`. Only save accounts on a browser profile you control.

---

## Troubleshooting

| Symptom | Fix |
| --- | --- |
| Panel does not appear | Confirm the script is enabled for `duolingo.com` in your manager, then hard-reload (`Ctrl+Shift+R`). The panel is fixed to the bottom-right; on narrow screens it sits 80 px above the bottom edge |
| `Not logged in` | The `jwt_token` cookie is missing or expired. Log in on duolingo.com and reload |
| `Outdated` | A newer build is on GreasyFork. Click the orange connection button |
| Farm stops with `Rate-limited. Stopping.` | Five consecutive failed requests triggered the back-off. Raise **Loop delay**, enable **Safe Mode**, and wait before retrying |
| Gems do not increase | Gem farming only claims rewards that already exist. Finish a lesson or skill first so a `SKILL_COMPLETION` reward is pending |
| Streak days rejected | Streak backfill depends on your account's timezone and current streak start date. Let the profile reconnect before retrying |
| XP total lower than requested | The script re-verifies against `totalXp` and tops up the gap. Large targets take several passes |
| Free Max not applied | Toggle it off/on, then reload the page. It is a client-side display flag only |
| Lesson Shortener has no effect | Toggle it on **before** starting the lesson, then reload so the session is created with the hook active |
| Duolingo images disappeared | Turn off **Hide Animation** |
| Avatars are broken | The panel falls back to a default avatar; a stale leaderboard cache clears itself on the next reconnect |

---

## Credits

| Project | Author | Contribution |
| --- | --- | --- |
| **DuoHacker V1** | [DuoHacker](https://github.com/DuoHacker/DuoHacker/tree/main/v1) | Original script — its core mechanics are reused in V2 |
| **Duolingo PRO** | [anonymoushackerIV](https://github.com/anonymoushackerIV/Duolingo-PRO) | The V2 interface was inspired by this script |

Built and maintained by **DuoHacker**.

- Website: <https://duohacker.io.vn>
- Discord: <https://duohacker.io.vn/discord>
- GitHub: <https://github.com/DuoHacker>
- YouTube: <https://duohacker.io.vn/youtube>

UI font: SF Pro Rounded, served from `font.duohacker.io.vn`. Icons are Duolingo's own CDN assets and SF Symbols glyphs.

---

## License

**BY-NC-ND 4.0** — Attribution, NonCommercial, NoDerivatives.

You may share the script unmodified with attribution. You may not sell it or distribute modified versions. Full text loads inside the panel under **Settings → DuoHacker V2**, or read it [here](https://github.com/DuoHacker/DuoHacker/blob/main/LICENSE).

---

## Notes

This is an unofficial third-party tool, not affiliated with or endorsed by Duolingo. It modifies requests in your own browser session, which Duolingo's Terms of Service prohibit — use it on an account you are willing to lose. For personal, educational use.

---

<div align="center">

### Tiếng Việt — Bắt đầu nhanh

1. Cài **Tampermonkey** cho trình duyệt.
2. Mở <https://greasyfork.org/en/scripts/561041-duolingo-duohacker> → bấm **Install this script** → **Install**.
3. Tải lại <https://www.duolingo.com>. Bảng điều khiển xuất hiện ở góc dưới bên phải.
4. Đợi trạng thái chuyển sang **Đã kết nối**, chọn ngôn ngữ bằng nút cờ ở giữa phía trên.
5. Nhập số XP / Gem / Streak rồi bấm **CHẠY**. Bấm **DỪNG** để dừng và giữ phần đã nhận.
6. Vào **Cài đặt** để chỉnh **Độ trễ vòng** (khuyến nghị 800–1500 ms nếu bị giới hạn) và bật **Chế độ an toàn**.

</div>
