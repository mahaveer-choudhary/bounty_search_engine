# Bug Bounty Search Engine

A small, client-side reconnaissance toolkit for security researchers that generates targeted search queries (Google dorks) and links to external OSINT services. It's a single-page, vanilla-HTML/JS project intended for authorized, ethical security testing and learning.

## Features

- 64+ pre-built search queries covering directory discovery, CMS enumeration, SQL, subdomains, archives, OSINT and more
- Quick-launch buttons that open queries in new tabs (Google, Shodan, Censys, Archive.org, GitHub, etc.)
- Search history (last 5 entries) and a copy-to-clipboard button for the target domain
- Responsive, single-file UI: `index.html` (logic + UI), plus theme files `style.css` and `style1.css`


## Quick Start (local)

1. Clone or copy the repository to your machine.
2. Open `index.html` in any modern browser (Chrome, Edge, Firefox, Safari).
   - No build tools or server required — project is fully client-side.
3. Enter a domain in the `Target Domain` field and click any search button.

## How the search engine works (developer notes)

- The main function is `googleSearch(type)` in `index.html`. It builds either:
  - a `searchQuery` string which is appended to `https://www.google.com/search?q=` and opened, or
  - a direct external URL (e.g., `https://crt.sh/?q=%25.` + domain) which is opened in a new tab.
- Many cases follow the pattern:
```js
searchQuery = 'site:' + targetDomain + ' <terms here>'
url = 'https://www.google.com/search?q=' + encodeURIComponent(searchQuery)
window.open(url, '_blank')
```
- To add a new query:
  1. Add a new `case N:` entry inside the `switch(type)` and append to `searchQuery` or set `url` directly.
  2. Add a button in the appropriate `.category` inside `index.html` that calls `googleSearch(N)`.
  3. Update the header stat if you want to reflect the new total.

## Security & Ethical Use (Important)

- This tool generates search queries only and does not perform automated scanning or exploitation.
- Only use this project for authorized testing, academic research, or with explicit permission from the target owner.
- The author is not responsible for misuse. Always follow applicable laws and the target site's terms of service.


## License

Include a license of your choice (e.g., MIT) before publishing if you want others to fork and reuse the code.
