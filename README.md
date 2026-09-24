# 🧠 3D Developer Portfolio — ALIAT Atef

<div align="center">

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Three.js](https://img.shields.io/badge/Three.js-r128-000000?style=for-the-badge&logo=threedotjs&logoColor=white)](https://threejs.org/)
[![Dark/Light](https://img.shields.io/badge/Theme-Dark%20%26%20Light-8B5CF6?style=for-the-badge)](#-dark--light-mode)

A **single-file, zero-build 3D portfolio** for an AI / Computer Vision engineer — a floating developer workspace (code editors, a browser, a live detection view) rendered in WebGL behind a clean, responsive layout.

[Features](#-features) • [Quick Start](#-quick-start) • [Architecture](#-architecture) • [Customization](#-customization) • [Deployment](#-deployment) • [Troubleshooting](#-troubleshooting)

</div>

---

## 📌 What's Included?

This portfolio provides:

- 🌌 **3D Background** - Floating code, web and computer-vision windows drawn with Three.js
- 🧑‍💻 **Hero, About, Projects, Stack, Contact** - Five sections in one scrolling page
- 🃏 **3D-Tilt Project Cards** - Mouse-reactive cards linking to each GitHub repository
- 🌗 **Dark / Light Mode** - Follows the system setting, with a manual toggle
- 📱 **Responsive Layout** - Works on desktop, tablet and phone
- 📦 **One File** - Everything lives in `index.html`, no bundler or npm install
- ⚡ **CDN Only** - Three.js from cdnjs, fonts from Google Fonts

---

## 🚀 Features

| Feature | Status | Description |
|---|---|---|
| 🖥️ Floating Dev Workspace | ✅ | 7 window types (Python, Java, SQL, HTML, terminal, browser, detection view) placed across 11 depth layers |
| 👁️ Computer Vision Window | ✅ | Face landmarks, `face 0.98` / `person 0.94` bounding boxes and a scan line |
| 🖱️ Mouse Parallax | ✅ | Camera follows the pointer for a sense of depth |
| 📜 Scroll Motion | ✅ | Windows drift upward as the visitor scrolls |
| 🌗 Theme Toggle | ✅ | Wireframe grid, window textures and UI colors all redraw on switch |
| 💾 Theme Memory | ✅ | Choice saved in `localStorage` (wrapped in try/catch, so it degrades safely) |
| 🃏 Tilting Project Cards | ✅ | CSS 3D perspective tilt on hover |
| 📱 Mobile Friendly | ✅ | Windows pull closer to the center on narrow screens, nav links collapse |
| 🔒 Safe-Area Aware | ✅ | Respects notches and system bars on phones |

---

## 📐 Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      index.html                             │
│                                                             │
│  ┌──────────────────┐        ┌───────────────────────────┐  │
│  │  HTML sections   │        │   <canvas id="bg">        │  │
│  │  hero · about    │        │   Three.js scene          │  │
│  │  work · stack    │        │                           │  │
│  │  contact         │        │   • 7 canvas textures     │  │
│  └────────┬─────────┘        │   • 11 floating planes    │  │
│           │                  │   • blueprint grid        │  │
│           ▼                  └─────────────▲─────────────┘  │
│  ┌──────────────────┐                      │                │
│  │  P[] projects    │                      │ redraw on      │
│  │  → tilt cards    │        ┌─────────────┴─────────────┐  │
│  └──────────────────┘        │   Theme engine            │  │
│                              │   CSS variables ◄─ toggle │  │
│                              │   prefers-color-scheme    │  │
│                              │   localStorage            │  │
│                              └───────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

**How the 3D background works**

1. Each window (`recognize.py`, `Main.java`, `stock.sql`, `index.html`, `bash`, browser, detection view) is drawn onto a `512×340` 2D canvas by a small draw function.
2. Each canvas becomes a `THREE.CanvasTexture` applied to a plane.
3. Planes are positioned in a layout table, then animated every frame (bobbing, parallax, scroll drift).
4. When the theme changes, the textures are redrawn with the new palette read from the CSS variables.

---

## ⚡ Quick Start

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/N1N0u/portfolio.git
cd portfolio
```

> Replace the URL with your own repository name.

### 2️⃣ Open It

The simplest way: double-click `index.html`.

For a local server (recommended, avoids any browser file restrictions):

```bash
# Python
python -m http.server 8000

# or Node
npx serve .
```

### 3️⃣ Visit

| Method | URL |
|---|---|
| **Local server** | http://localhost:8000 |
| **Direct file** | `file:///path/to/index.html` |

> An internet connection is needed the first time, to load Three.js and Google Fonts from their CDNs.

---

## 🌗 Dark / Light Mode

| Behavior | Details |
|---|---|
| **Default** | Follows `prefers-color-scheme` |
| **Manual** | Click the ☾ / ☀ button in the top bar |
| **Saved** | Stored in `localStorage` under the key `theme` |
| **3D scene** | Grid color and every window texture are redrawn to match |

Colors are defined as CSS variables on `:root`:

| Variable | Role |
|---|---|
| `--bg` / `--fg` | Page background / text |
| `--mute` | Secondary text |
| `--acc` | Primary accent (cyan in dark, deep blue in light) |
| `--acc2` | Secondary accent (violet) |
| `--card` / `--line` | Glass card fill / borders |

---

## 🛠️ Customization

### Edit the Projects

Projects live in the `P` array inside the `<script>`:

```js
const P = [
  [
    "USB Face-Recognition Locker",              // title
    "Locks any inserted USB drive...",          // description
    ["<100ms", "99.2% LFW", "76MB .exe"],       // metric chips
    "Python · ONNX · CustomTkinter · psutil",   // tech line
    "usb-face-recognition-locker"               // GitHub repo name
  ],
  // ...
];
```

Each card links to `https://github.com/N1N0u/<repo name>`. Change that base URL in the card-building loop if your username differs.

### Edit the Text Sections

Hero, About, Stack and Contact are plain HTML inside `<section>` tags. Edit them directly.

### Edit the 3D Windows

The `D` array holds one draw function per window type:

| Index | Window |
|---|---|
| `0` | `recognize.py` (Python) |
| `1` | Browser (`emitcompany.dz`) |
| `2` | Computer-vision detection view |
| `3` | `Main.java` |
| `4` | `stock.sql` |
| `5` | `bash` terminal |
| `6` | `index.html` |

Code windows use a simple format: alternating **color key** and **text** pairs.

```js
['k','import ','f','cv2, onnxruntime']   // k = keyword, f = plain text
```

| Key | Color |
|---|---|
| `k` | Keyword (secondary accent) |
| `a` | Function / accent |
| `s` | String / success (green) |
| `n` | Number / warning (amber) |
| `f` | Plain text |
| `c` | Comment |

### Move or Add Windows

Placement is controlled by the `lay` array:

```js
// [windowType, x, y, z, rotationY, scale]
[2, 4.6, 0.8, -3, -0.35, 1]
```

Add a row to add a window; change `z` to push it further back.

---

## 🌍 Deployment

The site is fully static, so any static host works.

### GitHub Pages

1. Push `index.html` (and this README) to your repository
2. Go to **Settings → Pages**
3. Choose the `main` branch and `/ (root)`
4. Your site appears at `https://<username>.github.io/<repo>/`

### Other Options

| Host | Notes |
|---|---|
| **Netlify / Vercel** | Drag-and-drop the folder, no build command |
| **cPanel / shared hosting** | Upload `index.html` via FTP |
| **Any web server** | Serve `index.html` as-is |

---

## 🔍 Troubleshooting

### Black or Empty Background?

1. Check that your browser supports **WebGL** (visit `about:gpu` in Chrome)
2. Make sure hardware acceleration is enabled
3. Open the console and check that `three.min.js` loaded from cdnjs

### Windows Look Blurry or Text Is Missing?

The window textures are redrawn once the JetBrains Mono font finishes loading. If you are offline, the page falls back to the system monospace font, which is expected.

### Theme Does Not Persist?

Some private-browsing modes block `localStorage`. The toggle still works for the current session.

### Page Feels Slow on an Old Machine?

Open `index.html` and edit the `lay` array to remove some windows, and lower the pixel ratio:

```js
R.setPixelRatio(Math.min(devicePixelRatio, 1));
```

### Text Hard to Read Over the Windows?

Lower the window opacity in the mesh material (`opacity: .78`) to a smaller value such as `.5`.

---

## 📁 Project Structure

```
portfolio/
├── index.html      # Entire site: markup, styles, 3D scene, logic
└── README.md       # This file
```

---

## 🧰 Tech Stack

| Layer | Tools |
|---|---|
| **Markup / Styling** | HTML5, CSS3 (custom properties, grid, backdrop-filter) |
| **3D** | Three.js r128, `CanvasTexture`, `GridHelper` |
| **Logic** | Vanilla JavaScript |
| **Fonts** | Space Grotesk, JetBrains Mono (Google Fonts) |
| **Hosting** | Any static host |

---

## 🌐 Browser Support

| Browser | Support |
|---|---|
| Chrome / Edge | ✅ Latest |
| Firefox | ✅ Latest |
| Safari (macOS / iOS) | ✅ Latest |
| Older browsers without WebGL | ⚠️ Page content works, 3D background does not render |

---

## 🤝 Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 👤 Author

**ALIAT Atef** — AI Engineer | Computer Vision Engineer | Real-Time Systems Builder

- 🐙 [GitHub](https://github.com/N1N0u)
- 💼 [LinkedIn](https://www.linkedin.com/in/atef-aliat/)
- 📊 [Kaggle](https://www.kaggle.com/atefaliat)
- 📧 aliat.atef@gmail.com

---

## ⭐ Skills Demonstrated

This project showcases:

- ✅ WebGL / Three.js scene design without a build step
- ✅ Procedural canvas textures for 3D content
- ✅ Theme-aware rendering (CSS variables driving 3D colors)
- ✅ Responsive, mobile-safe UI design
- ✅ Performance-conscious single-file architecture
- ✅ Accessible controls (labelled theme toggle, system theme support)

---

## 📞 Support & Issues

Found a bug?

- 🐛 [Open an Issue](https://github.com/N1N0u/portfolio/issues)
- ⭐ If helpful, please star the repository!

---

<div align="center">

**Made with ❤️ for the AI & Computer Vision community**

[⬆ back to top](#-3d-developer-portfolio--aliat-atef)

</div>
