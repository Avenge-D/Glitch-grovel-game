# 🦁 Glitch Grove

> *A 2D troll platformer where the environment is a liar.*

You play as a lion charging through a neon-pastel grove full of platforms that look safe — and aren't. No complex controls. Just left, right, jump, and pure betrayal.

**[▶ Play it live on GitHub Pages](https://YOUR-USERNAME.github.io/glitch-grove/)**

---

## 🎮 Controls

| Input | Action |
|-------|--------|
| `←` / `A` | Move left |
| `→` / `D` | Move right |
| `Space` / `↑` / `W` | Jump |
| On-screen buttons | Mobile / touch support |

---

## 💀 Platform Types

Every platform has a color. Colors lie — but they're consistent lies.

| Color | Type | What it does |
|-------|------|--------------|
| 🟣 **Purple** | Safe | Normal solid platform — the rare honest one |
| 🔴 **Red** | Spikes | Instant death the moment you touch it |
| 🩵 **Cyan** | Fake | Looks solid, phases you straight through — instant death |
| 🔵 **Blue** | Ice | You land, but slide sideways uncontrollably |
| 🟠 **Orange** | Bounce | Launches you violently upward, usually into something bad |
| 🟢 **Green** | Vanish | Shows a flashing `!` warning ~0.9s before disappearing forever |
| 🟫 **Dark orange** | Hot | Survivable for ~0.6 seconds — then you're ash |

---

## 🗺️ Levels

| # | Name | What's coming for you |
|---|------|----------------------|
| 1 | *First Steps* | Intro level — one vanishing platform to ease you in |
| 2 | *Cold Blood* | Ice + spike combos. The slide will kill you. |
| 3 | *Boing Boing Bye* | Bounce pads launching you into vanishing platforms |
| 4 | *The Floor Is Lying* | Hot floors and fake platforms side by side |
| 5 | *Full Grove* | Every trap type active simultaneously. Trust nothing. |

---

## 🧠 How the Traps Work

**Vanish** platforms give you a sub-1-second visual warning (a red `!` bubble above the platform + a screen warning) before disappearing. They respawn after 3 seconds.

**Hot** platforms let you stand briefly — the burn timer starts the moment you land. Get off within 0.6 seconds or die.

**Fake** platforms render identically to safe ones except for a slightly different color shade. They have no collision — you fall through instantly.

**Bounce** platforms launch the lion at 155% jump speed. Combine with spikes above for maximum chaos.

**Ice** platforms add lateral drift on landing — your momentum keeps going even after you stop pressing the key.

---

## 📁 Project Structure

```
glitch-grove/
├── index.html              # Entry point — loads all scripts in order
├── css/
│   └── style.css           # Canvas layout, HUD, mobile buttons
├── js/
│   ├── levels.js           # All 5 level definitions (platforms, goals, messages)
│   ├── lion.js             # Lion character — full canvas drawing function
│   ├── platforms.js        # Platform rendering, legend, and AABB collision
│   ├── particles.js        # Particle system (death bursts, goal celebrations)
│   └── game.js             # Main loop, physics, input handling, trap logic
└── README.md
```

No build tools. No dependencies. No `node_modules`. Just open `index.html`.

---

## 🚀 Running Locally

```bash
git clone https://github.com/YOUR-USERNAME/glitch-grove.git
cd glitch-grove

# Option 1 — just open in browser
open index.html

# Option 2 — local dev server (avoids any file:// quirks)
npx serve .
# or
python3 -m http.server 8080
```

---

## 🌐 Deploying to GitHub Pages

1. Push this repo to GitHub
2. Go to your repo → **Settings** → **Pages**
3. Under *Source*, select **Deploy from a branch**
4. Choose `main` branch, `/ (root)` folder → **Save**
5. Wait ~60 seconds → your game is live at:

```
https://YOUR-USERNAME.github.io/glitch-grove/
```

No configuration file needed. GitHub Pages serves `index.html` automatically.

---

## 🛠️ Tech Stack

| Layer | Choice | Why |
|-------|--------|-----|
| Rendering | HTML5 Canvas 2D | Full control over every pixel, no overhead |
| Logic | Vanilla JavaScript (ES6) | Zero dependencies, runs anywhere |
| Layout | CSS3 | Flexbox for centering, pointer events for mobile |
| Hosting | GitHub Pages | Free, instant, no server required |

---

## ✏️ Adding a New Level

Open `js/levels.js` and add an object to the array inside `buildLevels()`:

```js
{
  groundY: 330,
  goal: { x: 620, y: 308 },
  msg: 'Your level intro message here.',
  platforms: [
    { x: 150, y: 260, w: 90, h: 14, type: 'normal' },
    { x: 300, y: 210, w: 80, h: 14, type: 'spike'  },
    { x: 450, y: 250, w: 80, h: 14, type: 'vanish',
      vanishDelay: 3000, warnCountdown: 0,
      warnPhase: false, gone: false, respawn: 0 },
  ],
}
```

Platform `type` options: `normal` · `spike` · `fake` · `ice` · `bounce` · `vanish` · `hot`

The `vanish` type requires the extra fields shown above. All others only need `x`, `y`, `w`, `h`, `type`.

---

## ➕ Adding a New Trap Type

1. Add a color entry to `PLATFORM_COLORS` in `js/platforms.js`
2. Add drawing logic inside `drawPlatform()` (the `if (p.type === '...')` block)
3. Add collision logic inside the `update()` function in `js/game.js`
4. Add a legend entry to the `LEGEND` array in `js/platforms.js`

---

## 📜 License

MIT — use it, remix it, make it meaner.

---

*Made with HTML5 Canvas and zero mercy.*
