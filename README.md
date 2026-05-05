# 🎂 Birthday Card Generator

A personalized, shareable birthday card — beautiful dark glassmorphism UI, live age ticker, confetti, coin chime, and a fake ₹500 Amazon gift card prank. Hosted on GitHub Pages. No backend, no build step, just one HTML file.

**Live →** [shawkeen.github.io/birthday](https://shawkeen.github.io/birthday/)

---

## How to Use

### Share a card with someone

Just craft a URL in this format and send it:

```
https://shawkeen.github.io/birthday/{Name}/{DDMMYYYY}/
```

| Part | Description | Example |
|------|-------------|---------|
| `Name` | The birthday person's name | `Neha` |
| `DDMMYYYY` | Date of birth — Day, Month, Year | `06051997` for 6 May 1997 |

**Examples:**

```
https://shawkeen.github.io/birthday/Neha/06051997/
https://shawkeen.github.io/birthday/Hrithik/23072000/
https://shawkeen.github.io/birthday/Priya/14021999/
```

You can also use the built-in **link generator** at the base URL — fill in a name and date of birth, get a ready-to-copy link.

---

## Features

- **Personalized from URL** — name and age are pulled directly from the link, no editing needed
- **Live age ticker** — shows exact age down to 6 decimal places, updating in real-time
- **100+ birthday jokes** — all name-personalized, with smooth fade transitions
- **Fake ₹500 gift card** — a harmless prank button with 30+ funny responses
- **Coin popup + chime** — every click spawns a floating `+₹1` coin and plays a gold coin sound via Web Audio API (no external audio files)
- **Confetti** — hearts, stars, circles and rectangles in rose gold and champagne tones
- **Link generator** — built-in UI at the base URL to create and copy personalized links
- **Zero dependencies** — pure HTML + CSS + vanilla JS, Google Fonts only

---

## File Structure

```
birthday/
├── index.html   ← main card + generator (handles URL routing)
├── 404.html     ← GitHub Pages SPA redirect trick
└── README.md
```

The `404.html` is what makes dynamic URLs work on GitHub Pages. When someone opens `/birthday/Neha/06051997/`, GitHub Pages would normally 404 because that folder doesn't exist. The `404.html` intercepts this, stores the intended path in `sessionStorage`, and redirects to `index.html` — which then reads the path and renders the correct card.

---

## How to Deploy Your Own

1. **Fork this repo** or create a new one named `birthday`
2. Drop in `index.html` and `404.html`
3. Go to **Settings → Pages → Source** → set to `main` branch, `/ (root)`
4. Your generator will be live at `https://{your-username}.github.io/birthday/`
5. Update the `BASE_URL` constant in `index.html` to match your username:

```js
var BASE_URL = 'https://{your-username}.github.io/birthday/';
```

---

## Customization

Everything lives in `index.html`. Key spots to edit:

| What | Where in the file |
|------|-------------------|
| Add / remove jokes | `buildJokes(n)` function |
| Change prank messages | `buildPranks()` function |
| Change the coin chime notes | `playCoinChime()` — edit the `freq` values |
| Change colors | CSS `:root` variables at the top |
| Change the confetti shapes/colors | `SHAPES` and `COLORS` arrays |
| Change the gift card button text | Search `Claim ₹500 Amazon Gift Card` |

---

## Tech Notes

- **URL parsing** — `window.location.pathname` split on `/`, segments 1 and 2 are name and DOB
- **DOB format** — `DDMMYYYY` (e.g. `06051997` → 6 May 1997). Parsed as `new Date(yyyy, mm-1, dd)`
- **Coin sound** — generated entirely with the Web Audio API. Three sine wave oscillators (C6 → E6 → G6) with exponential gain decay
- **Confetti** — canvas-based, `requestAnimationFrame` loop with gravity simulation
- **GitHub Pages routing** — standard `404.html → sessionStorage → index.html` trick

---

## License

MIT — fork it, remix it, send it to everyone you know on their birthday.

---

*Built by [shawkeen](https://github.com/shawkeen) · [iamhrithikshaw](https://www.linkedin.com/in/iamhrithikshaw) on LinkedIn*
