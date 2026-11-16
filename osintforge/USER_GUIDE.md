# OSINTFORGE User Guide

OSINTFORGE is a browser-based workbench for collecting and organising information from selected public internet sources. It uses a graph view to connect entities and keeps source links and collection timestamps alongside findings.

## Start

1. Open the hosted application (once GitHub Pages deployment has completed) or open `osintforge/index.html` locally in a modern browser.
2. Give the case a name.
3. Enter a target and choose its type, or leave the type on Auto-detect.
4. Select a collector in the left panel.
5. Select **Run live collection**.
6. Review the Findings, Sources & provenance, and Activity log tabs.

No collection is performed until you start a collector.

## Available collectors

| Collector | Input | Data source | What it retrieves |
|---|---|---|---|
| Domain intelligence | Domain | RDAP, Cloudflare DNS-over-HTTPS, crt.sh | Registration events/status, nameservers, DNS answers, and certificate names |
| DNS records | Domain | Cloudflare DNS-over-HTTPS | A, AAAA, MX, NS, TXT and CAA answers |
| Certificate transparency | Domain | crt.sh | Publicly logged certificate names (up to 100 records processed) |
| IP / network RDAP | IPv4 or IPv6 | rdap.org | Public registration range, network name, handle and country |
| GitHub public profile | GitHub username or organisation | GitHub REST API | Public profile metadata and up to 30 recently updated public repositories |
| URLScan public reports | Domain | URLScan public search | Existing publicly indexed scan reports; it does not submit a new scan |
| CVE product search | Search phrase or product | NIST NVD CVE API | Public CVE records matching the keyword |

Each collector makes live requests when invoked. Results depend on the upstream service, availability, rate limits, CORS policy and the target. An empty result is not proof that no records exist.

## Graph workspace

- Select an entity to view its type, detail, source and source link.
- Drag nodes to rearrange the graph.
- Use the entity search field to find a node.
- **Fit graph** arranges nodes in a radial layout.
- **Toggle labels** hides or shows node labels.
- **Clear graph** removes graph entities and relationships from the current workspace.
- **＋ Note** adds a manual observation to the graph.
- Removing a node also removes its connected edges.

The graph is an analyst's working view, not an assertion that every association is a verified real-world relationship. The current version draws simple association edges from the first entity to newly discovered entities. Validate relationships against the cited source.

## Cases, notes and exports

- **Save case locally** stores the current case in this browser's local storage.
- **Export JSON** downloads a complete case file, including entities, edges, sources, timestamps and notes.
- **Export CSV** downloads the entity list for spreadsheet analysis.
- **Import JSON** loads a previously exported OSINTFORGE case file.
- Research notes are saved with the local case.

Local storage is specific to the browser profile and device. Clearing browser data can delete saved cases. Export important work regularly. This version does not provide accounts, cloud storage, shared cases or server-side backups.

## Understanding findings

Every source entry includes a provider name, query URL, description and collection time. Open the source to inspect the original result. A provider may update or remove data after collection, so preserve the exported case when a time-stamped record is important.

RDAP and DNS results describe public technical infrastructure. Certificate transparency entries show names present in public certificate records; they do not prove that a host is live or controlled by a particular person. GitHub fields are public profile data and may be incomplete. CVE keyword matches require manual product/version validation.

## Troubleshooting

### A collector reports a network or fetch error
Check connectivity and try again. The source may be temporarily unavailable, may rate-limit requests, or may not permit browser-origin requests. The app runs as a static site and cannot bypass a provider's CORS restrictions. The error is shown in the Activity log.

### No results are returned
Check spelling and target type. Try the source directly using the link in Sources & provenance. No result does not establish that a domain, record, vulnerability or relationship does not exist.

### Imported case rejected
Import only a JSON file exported by OSINTFORGE with schema `osintforge.case.v1`. Treat files received from other people as untrusted data.

### Case disappeared
Cases are stored locally in the browser. Import a prior JSON export if available.

## Privacy and responsible use

- Use the tool for legitimate research into public infrastructure, public repositories and published records.
- Do not use it to harass, stalk, dox, threaten or target private individuals.
- Do not attempt to access private accounts, bypass authentication, evade access controls or conduct intrusive scans.
- Do not enter passwords, API keys, private records or confidential case material.
- Respect provider terms, rate limits, privacy law and applicable organisational policies.
- Do not treat automated findings as proof. Corroborate important claims with primary sources.

## Current limitations

This is a client-side research workbench, not a commercial intelligence platform. It does not run continuous monitoring, active port scans, exploit checks, breach-database searches, private-account lookups, identity resolution, automated attribution, or AI-generated conclusions. It does not guarantee provider uptime or completeness. Browser CORS and public API limits may prevent an individual collector from returning data in some environments.

## For contributors

See [Architecture and development](ARCHITECTURE.md) for the implementation model and extension guidance.
