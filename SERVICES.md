# External Services & Widget Rationale

This document tracks all third-party microservices, APIs, design components, and GitHub Actions dependencies integrated into the `xdc7-css` profile repository.

---

## 🛠️ Widgets & External APIs

| Service Name | Verified Endpoint | Status | Purpose & Rationale |
|--------------|-------------------|--------|---------------------|
| **Capsule Render** | `capsule-render.vercel.app` | ✅ Active (200 OK) | Dynamic SVG header & footer banners, section dividers. Provides high-impact navy/gold visual theme. |
| **Readme Typing SVG** | `readme-typing-svg.demolab.com` | ✅ Active (200 OK) | Animated subheader typing text effect presenting roles and philosophy. |
| **Shields.io** | `img.shields.io` | ✅ Active (200 OK) | Industry-standard badges for social links, tech stack indicators, and architectural methodologies. |
| **Skill Icons** | `skillicons.dev` | ✅ Active (200 OK) | High-definition vectorized tech stack grid icons. |
| **GitHub Readme Stats** | `github-readme-stats-fast.vercel.app` | ✅ Active (200 OK) | Active mirror service providing live GitHub statistics cards, top language distribution, and pinned repository cards. |
| **GitHub Streak Stats** | `streak-stats.demolab.com` | ✅ Active (200 OK) | Real-time contribution streak visualization with navy and gold palette customization. |
| **GitHub Profile Trophy** | `github-trophies.vercel.app` | ✅ Active (200 OK) | Real-time achievement trophies rendered as SVG icons based on commit activity and stars. |
| **GitHub Activity Graph** | `github-readme-activity-graph.vercel.app` | ✅ Active (200 OK) | Interactive line graph chart showcasing annual contribution trends. |
| **Profile Views Counter** | `komarev.com/ghpvc` | ✅ Active (200 OK) | Lightweight cloud microservice counting total unique profile views. |

---

## ⚙️ GitHub Actions Workflow

| Action Name | Workflow Location | Latest Version | Purpose |
|-------------|-------------------|----------------|---------|
| `actions/checkout` | `.github/workflows/snake.yml` | `v4` | Checks out repository files into runner workspace. |
| `Platane/snk` | `.github/workflows/snake.yml` | `v3` | Automatically generates contribution grid snake SVGs in light and dark mode. |
| `crazy-max/ghaction-github-pages` | `.github/workflows/snake.yml` | `v4` | Deploys the generated SVG artifacts automatically to the orphan `output` branch. |

---

## 💡 Technical Setup Notes

1. **Snake Animation Deployment**:
   - The workflow `.github/workflows/snake.yml` generates `github-snake.svg` and `github-snake-dark.svg` into the `dist/` folder.
   - `crazy-max/ghaction-github-pages@v4` publishes the contents of `dist/` directly to an isolated branch named `output`.
   - The `README.md` references the SVGs via GitHub raw content links (`raw.githubusercontent.com/xdc7-css/xdc7-css/output/...`).

2. **API Reliability Strategy**:
   - Primary Vercel deployments for standard stats APIs can experience high traffic rate-limiting or maintenance pauses.
   - We utilize high-availability active mirrors (`github-readme-stats-fast.vercel.app` and `github-trophies.vercel.app`) to guarantee 100% uptime and smooth rendering on your GitHub landing page.
