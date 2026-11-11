# Changelog

## 1.11.0 - 2026-11-11

### Added
- Update page: see what's new in each release, update with one click, and optionally check and install updates automatically. Releases come from GitHub, and each installer is checked against its SHA256 before it runs.

### Fixed
- Server-side requests from a Next.js dev server to `https://<name>.localhost` sites no longer fail with a certificate error.
- Firefox accepts the local certificate for `https://localhost`, used by Next.js and Nuxt dev servers.
- Installed apps list: Loala shows as 64-bit, its size counts only Loala itself (not your projects and databases), and the website and description are filled in.
- Uninstalling also removes Loala's browser cache.

## 1.10.14 - 2026-11-10

### Added
- Node.js projects run from the Sites list: Dev, Build, and Start for Next.js, Nuxt, Vite, and Express, each in the background with its own terminal, restart, port, and stop controls.
- Next.js and Nuxt dev servers use HTTPS with the local certificate.
- Site domains behave like hosting: a static build is served directly, a started Node server is proxied, and an info page explains what to do otherwise.
- Quick app templates for Next.js, Vite, Nuxt, and Express.
- Global npm packages and Go installs are kept inside the Loala folder, so they move with it.

### Changed
- Stop All is about five times faster and also stops running Node.js dev servers, starts, and builds.
- Focus outlines use the accent color instead of black.

### Fixed
- Sharing a site on your own domain works again after logging out of Cloudflare and back in.
- The site list stays responsive while a share is starting.
- Entries written to the hosts file by other programs are no longer removed, and a read-only hosts file is handled.
- Custom document roots follow the Loala folder when it is moved.
- Start All starts every other service even when one fails, and reports all errors at once.
- Quick add extracts archives reliably, downloads one package at a time, and fetches ffmpeg from a faster source.
- Submenus line up with their parent item when the main menu is scrolled.

## 1.5.2 - 2026-11-07

First public release.

- Apache and Nginx with automatic HTTPS for every site at `https://<name>.localhost`.
- MySQL, PostgreSQL, MongoDB, Redis, and Memcached, with one-click backups and scheduled automatic backups.
- PHP, Node.js, Python, and Go, with several versions side by side.
- Quick app: create WordPress, Laravel, and other projects, or clone from a Git URL.
- Quick add: install more versions and tools from the menu.
- Share any site on a public URL through Cloudflare Tunnel.
- Built-in terminal, editor, cron jobs, Procfile runner, and Mailpit for testing email.
