<p align="center">
  <img src="docs/banner.png" alt="Miraxos — case study" width="100%">
</p>

# Miraxos

**Miraxos** is a SaaS for elevator cabin manufacturers. Enter the cabin and car-frame dimensions — Miraxos generates the
laser-ready DXF part drawings and the work order together, in a single package.
It is live at **[miraxos.com](https://miraxos.com)** and used in production by manufacturers in Türkiye.

> Miraxos is a commercial, closed-source product. This repository contains no source code — only this overview.

---

## 👤 My role

**Founder & product builder.**

- Product vision, roadmap and priorities
- Domain model of cabin and car-frame parts, built together with a mechanical-engineering partner
- Architecture and quality decisions — what "done" means, how every change is verified before release
- Customer onboarding: preparing each manufacturer's templates and validating the first outputs with them
- Release management: staging → production

---

## 🎬 See it in action

<table>
  <tr>
    <td width="50%" valign="top">
      <a href="docs/miraxos-demo.mp4"><img src="docs/launch.png" alt="Miraxos product demo"></a>
      <p><b>Product demo</b> (64 s, Turkish) — module → set → dimensions → preview → work order → download</p>
    </td>
    <td width="50%" valign="top">
      <a href="docs/miraxos-1100x1400.mp4"><img src="docs/dimensions.png" alt="One set of dimensions"></a>
      <p><b>1100 × 1400</b> (22 s, Turkish) — one set of dimensions, a full set of parts</p>
    </td>
  </tr>
</table>

---

## ⚙️ How it works

1. **Choose a module** — car frames and cabins from a single catalog (e.g. 1-1 suspension, 2-1 side/rear counterweight, electric cabin)
2. **Choose the production set** — the manufacturer's own parts, approved by their engineer
3. **Enter the dimensions** — cabin width/depth, rail distances, door and panel options
4. **Preview** — the drawing is generated live; if a dimension can't be produced, Miraxos tells you the valid range instead of failing
5. **Download** — one ZIP with laser-ready DXF files and a work-order PDF: parts grouped by thickness, matched to balloon numbers on the drawing

<p align="center"><img src="docs/preview.png" alt="Live preview" width="80%"></p>

---

## ✨ Product highlights

| | |
|---|---|
| **Company-specific catalogs** | Parts and ceiling patterns belong to one manufacturer; a catalog is never visible to another company |
| **Engineer approval** | Every uploaded DXF part is reviewed; an unapproved part can't appear in any set |
| **Publishing gate** | A set is actually produced with trial dimensions before it can go live — a set that can't be produced isn't published |
| **Range suggestions** | When dimensions don't fit, the user gets the valid ranges, not just an error |
| **No installation** | Runs in the browser — desktop, tablet and phone; no CAD license or powerful computer needed |
| **12+ drawing modules** | 5 active today, 7 more opened on customer request |

**Results reported on miraxos.com:** ~95 % less drawing time · under 2 minutes average output time.

<p align="center"><img src="docs/devices.png" alt="Desktop, tablet and phone" width="80%"></p>

---

## 🏗️ Engineering

```mermaid
flowchart LR
    U[Browser · desktop / tablet / phone] --> W[Web app · Next.js + TypeScript]
    W --> DB[(PostgreSQL · Supabase)]
    W -- preview --> E[Drawing engine · Python]
    W -- production job --> Q[Job queue]
    Q --> K[Worker · Node.js]
    K --> E
    E --> F[DXF drawings + work-order PDF]
    F --> S[(File storage)]
```

**Numbers (measured October 2026)**

- **19,000+ automated tests** — including golden-file regression tests that compare generated drawings against approved reference outputs
- **338 database migrations**, each verified on a local copy before it reaches staging and production
- **1,600+ commits** since July 2026

**Practices**

- Multi-tenant by design — each manufacturer's data, parts and catalog are kept separate
- Safeguards are verified by *deliberately breaking them*: a protection only counts once the test that guards it is seen failing
- Staging → production release pipeline, error tracking and uptime monitoring
- Screens checked on 6 screen sizes × light and dark themes; customer-facing UI in Turkish and English

![Next.js](https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?style=for-the-badge&logo=supabase&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)

---

### 📫 Contact

Interested in Miraxos for your production? **[miraxos.com](https://miraxos.com)** · [omerarkbua01@gmail.com](mailto:omerarkbua01@gmail.com)
