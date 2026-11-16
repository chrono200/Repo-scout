# Repo Scout

Repo Scout is a Termux-friendly GitHub reconnaissance and discovery CLI project. This repository also contains **OSINTFORGE**, a browser-based public-source research and link-analysis workbench.

## OSINTFORGE

OSINTFORGE is a static web application for collecting selected public technical and developer-platform records, organising entities in a graph, retaining source provenance, and exporting research cases.

- **Application:** [Open OSINTFORGE source](osintforge/index.html)
- **User guide:** [Read the user documentation](osintforge/USER_GUIDE.md)
- **Architecture:** [Technical architecture and development guide](osintforge/ARCHITECTURE.md)
- **Hosted application:** [https://chrono200.github.io/Repo-scout/](https://chrono200.github.io/Repo-scout/) (available after the GitHub Pages deployment succeeds)

### Current collectors

| Collector | Public source |
|---|---|
| Domain registration | RDAP |
| DNS records | Cloudflare DNS-over-HTTPS |
| Certificate names | crt.sh certificate transparency |
| IP network registration | RDAP |
| Public GitHub profiles and repositories | GitHub REST API |
| Existing URL scan reports | URLScan search |
| Vulnerability keyword search | NIST NVD CVE API |

The application includes an interactive SVG graph, entity inspector, source register, activity log, case notes, local browser save, JSON import/export and CSV export.

**Important:** collectors make live requests from the browser. Availability, CORS rules and upstream rate limits affect results. The tool does not bypass authentication, access private accounts, perform intrusive scanning, or claim that an association is proof. Read the [user guide](osintforge/USER_GUIDE.md) before use.

## Repo Scout CLI archive

The repository also retains the packaged Repo Scout CLI archive:

- [Repo-Scout-v1.1-fixed.zip](Repo-Scout-v1.1-fixed.zip)

The archive's runtime requirements and launch instructions should be checked against the files in that release.

## Hosting

A GitHub Actions workflow deploys the `osintforge/` directory to GitHub Pages on changes to `main`. The workflow requires GitHub Pages deployment permission for the repository.

## Maintainer

[@chrono200](https://github.com/chrono200)
