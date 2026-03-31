# 🕌 Isnad Chain Analyzer — تحليل سلسلة الإسناد

> An interactive Graph Theory application for the analysis of Hadith transmission chains (Isnad), built with D3.js and pure HTML/CSS/JavaScript.

[![Graph Theory](https://img.shields.io/badge/Graph%20Theory-DAG%20Analysis-c8952a?style=flat-square)](https://github.com/zuhaibbutt786)
[![Language](https://img.shields.io/badge/Language-JavaScript%20%2F%20D3.js-60a5fa?style=flat-square)](https://github.com/zuhaibbutt786)
[![Status](https://img.shields.io/badge/Status-Active-10b981?style=flat-square)](https://github.com/zuhaibbutt786)
[![License](https://img.shields.io/badge/License-MIT-94a3b8?style=flat-square)](LICENSE)

---

## 📖 Overview

The **Isnad Chain Analyzer** applies formal **Graph Theory** to the Islamic science of Hadith transmission (*ʿIlm al-Isnād*). Every Hadith is backed by a chain of narrators stretching from the Prophet Muhammad ﷺ through generations of Companions, Tabi'un, and scholars to the great compilers of the 3rd century AH.

This tool models that chain as a **Directed Acyclic Graph (DAG)** — where each narrator is a **node** and each transmission is a **directed edge** — enabling rigorous computational analysis of authenticity, centrality, and structural integrity.

The application comes pre-loaded with **26 historical narrators** and **46 verified transmission links**, spanning the complete canonical chain from the Prophet ﷺ to Imam Bukhari and Imam Muslim.

---

## ✨ Features

### Graph Theory Algorithms

| Feature | Algorithm | Description |
|---|---|---|
| **Force-Directed Layout** | Spring-embedder (D3 Force) | Nodes positioned by generation layer and repulsion/attraction forces |
| **Shortest Path** | BFS (Breadth-First Search) | Finds the minimum-link chain between any two narrators |
| **All Chains Enumeration** | DFS with backtracking | Traces every valid Isnad path between two narrators (up to 60 chains) |
| **Betweenness Centrality** | Brandes' Algorithm | Identifies single-points-of-failure in the transmission network |
| **Degree Centrality** | In/Out degree calculation | Ranks narrators by total transmission connections |
| **Cycle Detection** | DFS coloring (White/Grey/Black) | Verifies the Isnad is a true DAG — no narrator appears in their own chain |
| **Connected Components** | BFS on undirected projection | Discovers isolated narrator clusters within the graph |

### Hadith Science Visualizations

- **Node color** encodes narrator reliability: `Thiqah` (green) · `Sadooq` (blue) · `Daʿīf` (orange) · `Majhūl` (gray)
- **Ring color** encodes generation: Prophet ﷺ → Ṣaḥāba → Tābiʿūn → Atbāʿ → Imāms → Compilers
- **Node size** encodes degree centrality — more connected narrators appear larger
- **Edge style**: solid gold lines = `سماع` (direct hearing); dashed lines = `إجازة` (written permission)
- **Automatic grading**: each discovered chain is graded as Ṣaḥīḥ / Ḥasan / Ḍaʿīf based on the weakest-link narrator's reliability

### Interactive Controls

- Click any narrator node to view bio, generation, death date, teachers, students, and centrality scores
- Filter the graph by **generation** (Ṣaḥāba only, Tābiʿūn only, etc.) or by **reliability class**
- Run shortest-path and all-chains analysis between any two selected narrators
- **Add custom narrators** with name, Arabic name, generation, reliability, death date, and location
- **Add transmission links** between any two narrators with a selectable transmission method
- Zoom, pan, drag nodes, and reset the view at any time

---

## 🚀 Getting Started

### Option 1 — Open Directly (No Setup Required)

This is a fully self-contained single-file application. Simply download `isnad_graph_analyzer.html` and open it in any modern browser.

```bash
# Clone the repo
git clone https://github.com/zuhaibbutt786/isnad-chain-analyzer.git

# Open the app
open isnad_graph_analyzer.html
# or on Windows:
start isnad_graph_analyzer.html
```

### Option 2 — Serve Locally

```bash
# Using Python
python -m http.server 8000

# Using Node.js
npx serve .
```

Then visit `http://localhost:8000/isnad_graph_analyzer.html`

### Requirements

- Any modern browser (Chrome, Firefox, Safari, Edge)
- No server, no build step, no dependencies to install
- D3.js v7 is loaded via CDN (`cdnjs.cloudflare.com`)

---

## 📐 Graph Theory Background

### Why a DAG?

An Isnad is valid only if it is **acyclic** — no narrator can have received a narration from someone who in turn received it from them, since transmission flows strictly forward in historical time. The cycle detection algorithm verifies this property formally.

### Betweenness Centrality

Given a graph *G = (V, E)*, the betweenness centrality of a node *v* is:

$$C_B(v) = \sum_{s \neq v \neq t} \frac{\sigma_{st}(v)}{\sigma_{st}}$$

Where $\sigma_{st}$ is the total number of shortest paths from *s* to *t*, and $\sigma_{st}(v)$ is the number of those paths passing through *v*. A narrator with high betweenness is a **critical transmission bottleneck** — if their narrations are rejected, many chains collapse.

### Chain Grading (Weakest Link Model)

Each chain is graded by the **minimum reliability score** of all narrators in the path:

| Score | Grade | Label |
|---|---|---|
| 5 | All narrators Thiqah | Ṣaḥīḥ |
| 4 | At least one Sadooq | Ṣaḥīḥ li Ghayrihī |
| 3 | Hasan-level narrator present | Ḥasan |
| 2 | Daʿīf narrator present | Ḍaʿīf |
| ≤1 | Severely weak narrator | Mawḍūʿ |

---

## 🗂️ Pre-loaded Dataset

The application ships with the following historical narrators across 6 generations:

| Generation | Narrators |
|---|---|
| 0 — Prophet ﷺ | Prophet Muhammad ﷺ |
| 1 — Ṣaḥāba | Umar ibn al-Khattab · Abu Huraira · Aisha · Ibn Umar |
| 2 — Tābiʿūn | Alqama · Urwa ibn al-Zubayr · Qatada · Ibn Shihab al-Zuhri · Muhammad ibn Ibrahim · Yahya al-Ansari |
| 3 — Atbāʿ al-Tābiʿīn | Hisham ibn Urwa · Abu al-Zinnad · Amr ibn Dinar · Ayyub al-Sakhtiyani |
| 4 — Imāms | Sufyan ibn Uyayna · Imam Malik · Al-Layth ibn Sad · Abu Muawiya · Ibn al-Mubarak · Imam Shafi'i · Imam Ahmad |
| 5 — Compilers | Yahya ibn Main · Ali ibn al-Madini · Imam Bukhari · Imam Muslim |

All narrator biographies, death dates, locations, and reliability grades are sourced from classical *rijāl* literature including *Tahdhīb al-Kamāl* and *Mīzān al-Iʿtidāl*.

---

## 🖼️ Screenshots

```
[Graph View]              [Narrator Detail]         [Chain Analysis]
Force-directed DAG   →    Bio + centrality stats →  Ṣaḥīḥ / Daʿīf grading
with generation layers    teachers & students       all paths enumerated
```

> Screenshots coming soon. Run the app locally to explore the full interface.

---

## 🛠️ Tech Stack

| Technology | Role |
|---|---|
| **D3.js v7** | Force simulation, graph rendering, zoom/pan |
| **HTML5 / CSS3** | Layout, theming, dark UI |
| **Vanilla JavaScript** | All graph algorithms (BFS, DFS, Brandes, etc.) |
| **SVG** | Graph canvas rendering |

No frameworks. No build tools. No backend. A single `.html` file.

---

## 📁 Project Structure

```
isnad-chain-analyzer/
│
├── isnad_graph_analyzer.html   # Complete self-contained application
├── README.md                   # This file
└── LICENSE                     # MIT License
```

---

## 🔮 Roadmap

- [ ] Export graph as SVG / PNG image
- [ ] Import custom narrator datasets via JSON
- [ ] Pagerank centrality in addition to betweenness
- [ ] Timeline view showing narrators by death year (AH)
- [ ] Support for multiple simultaneous Hadith chains comparison
- [ ] Arabic-language UI toggle
- [ ] Narrator search / filter by name

---

## 🤝 Contributing

Contributions are welcome — especially additions to the narrator dataset, corrections to biographical data, or new graph analysis features.

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m 'Add some feature'`
4. Push to the branch: `git push origin feature/your-feature`
5. Open a Pull Request

---

## 📜 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgements

- Classical *rijāl* scholars whose centuries of narrator criticism made this data possible
- D3.js team for the force simulation library
- The field of computational Islamic studies for inspiring this application

---

<div align="center">

**Built with dedication to the science of Hadith**

*"إِنَّمَا الْأَعْمَالُ بِالنِّيَّاتِ"*

*"Actions are but by intentions"* — Ṣaḥīḥ al-Bukhārī, Hadith 1

---

Made by **[Zuhaib Butt](https://github.com/zuhaibbutt786)**

[![GitHub](https://img.shields.io/badge/GitHub-zuhaibbutt786-181717?style=flat-square&logo=github)](https://github.com/zuhaibbutt786)

</div>
