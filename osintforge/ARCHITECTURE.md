# OSINTFORGE Architecture & Development

## Architecture

OSINTFORGE is a static, client-side web application. The current implementation is contained in `index.html` and has no build step, server runtime, package installation or third-party JavaScript dependency.

- **Interface:** semantic HTML and responsive CSS.
- **Graph:** SVG nodes and edges rendered by vanilla JavaScript.
- **Collectors:** browser `fetch()` calls to public RDAP, DNS-over-HTTPS, certificate-transparency, GitHub, URLScan and NIST NVD endpoints.
- **Case model:** in-memory JavaScript state.
- **Persistence:** browser localStorage and downloadable JSON/CSV exports.
- **Hosting:** GitHub Pages via GitHub Actions.

## Data flow

1. The user chooses a collector and supplies a target.
2. The browser validates the target format.
3. The collector sends a request to its public source.
4. Returned records are converted into entities, relationships and source records.
5. The graph, findings panel, source register and activity log are updated.
6. The user can save locally or export the case.

The browser communicates directly with upstream services. There is no OSINTFORGE server receiving or storing submitted targets.

## Security model

- No login system or credential collection.
- No secret API keys embedded in the application.
- No private-account access or authentication bypass.
- Source URLs are rendered only when they use HTTP or HTTPS.
- Imported case files are untrusted input; visible text is escaped before display.
- The application is intended for public-source research, not intrusive scanning or personal targeting.

## External services

| Service | Endpoint family | Purpose |
|---|---|---|
| RDAP | `rdap.org/domain`, `rdap.org/ip` | Domain and IP registration data |
| Cloudflare DNS | `cloudflare-dns.com/dns-query` | DNS-over-HTTPS lookups |
| crt.sh | `crt.sh/?q=...&output=json` | Certificate transparency search |
| GitHub | `api.github.com/users` | Public profile and repository data |
| URLScan | `urlscan.io/api/v1/search` | Search existing public scan reports |
| NIST NVD | `services.nvd.nist.gov/rest/json/cves/2.0` | Public CVE keyword search |

External providers can change their APIs, impose limits or restrict cross-origin browser requests. Collector failures should be reported as provider/network failures, not silently interpreted as empty intelligence.

## Local development

1. Clone the repository.
2. Open `osintforge/index.html` in a modern browser, or serve the repository with any static HTTP server.
3. Use browser developer tools to inspect collector requests and errors.
4. Test each collector with a domain, IP address or public GitHub account you are authorised to research.

No build step is required.

## Extending a collector

A collector should:
1. Validate and normalise its target.
2. Use HTTPS and a public, documented endpoint.
3. Handle non-2xx responses and malformed JSON.
4. Record the source URL, provider and collection timestamp.
5. Add entities and edges without asserting unverified relationships.
6. Surface errors in the activity log.
7. Respect provider terms, rate limits and privacy constraints.

Do not add scraping of private accounts, credential collection, access-control bypass, personal-data broker lookups, covert tracking or intrusive scanning.

## Hosting

The workflow in `.github/workflows/deploy-pages.yml` publishes the `osintforge/` directory to GitHub Pages after changes reach `main`. The repository's Pages feature must be available to the GitHub Actions workflow. The resulting site URL is:

`https://chrono200.github.io/Repo-scout/`

The workflow can also be run manually from the Actions tab.
