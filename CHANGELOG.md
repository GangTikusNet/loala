# Changelog

## 1.14.2 - 2026-11-27

### Added
- Each site in the Sites list has a Delete button, which opens the same confirmation as Tools > Delete project.

### Changed
- Deleting a project can also drop its databases in MySQL, PostgreSQL, and MongoDB: those set in `.env` or `wp-config.php`, and those named after the project. They are selected by default and backed up to `backup/<engine>/` before they are dropped.
- If a database server is stopped, the delete dialog says which databases can't be checked, instead of leaving them behind without notice.
- Quick app lets you choose the database engine (MySQL, PostgreSQL, or MongoDB, among those running) and name the database. Laravel and Symfony projects can use MySQL or PostgreSQL, and WordPress uses MySQL.
- Symfony projects created with a database get a `DATABASE_URL` in `.env`, so Doctrine uses it once installed.
- Clone copies the source project's database in MySQL, PostgreSQL, or MongoDB, found from its `.env`, and the new database name can be changed.

### Fixed
- Laravel projects created with a database no longer fail with "Table 'sessions' doesn't exist": the tables are created in the new database.
- The WordPress Quick app no longer fails with "The download is not a valid archive": it downloads the official `.zip` archive. Existing configurations using the old `.tar.gz` link are updated.
- The Nuxt Quick app creates the project without stopping to ask questions (minimal template, npm, no Git repository), like Next.js.

## 1.12.7 - 2026-11-19

### Added
- Python projects run from the Sites list: FastAPI, Flask, and Django are detected automatically, with Install (creates the project's `.venv` and installs its packages), Dev, and Start, each in the background with its own terminal, restart, port, and stop controls.
- While a Python app is running, its site domain (`https://<name>.localhost`) shows the app.
- Python apps trust the local certificate, so `requests` and `httpx` can call `https://<name>.localhost` sites.
- Quick app templates for FastAPI, Flask, and Django.

### Changed
- Updating shows a progress window until Loala opens again.
- A new release is announced once with a small card, in addition to the dot on the Update icon.
- Node.js and Python apps listen only on this computer (127.0.0.1): they are not reachable from the network, and Windows Firewall no longer asks about them.
- Custom hostname formats such as `{name}.dev` get trusted certificates. When a new suffix is used, the local certificate authority is recreated and trusted again.

### Fixed
- Apps served at `https://<name>.localhost` now know they are behind HTTPS, so redirects, absolute URLs, and secure cookies are correct. Django forms and the admin login no longer fail the CSRF check, and the Flask template handles the proxy.
- Stop, Restart, Stop All, and Exit stop the whole app, including processes started by npm or the uvicorn reloader, so its port is freed.
- Dev and Start say which program is using the port instead of failing silently, and Restart waits for the port to be free.
- Node.js and Python apps left running after Loala closed unexpectedly are stopped the next time Loala opens.
- A site's domain switches to the app once the app is listening, instead of showing an error while it starts.
- Python Install: projects with only `pyproject.toml` install their dependencies, an interrupted Install is no longer treated as installed, and more app layouts are found (`src/` packages, `__init__.py` factories, `fastapi.FastAPI()`).
- Starting a service while others are running uses its latest port, version, and password.
- Settings are saved safely: an interrupted save no longer empties `loala.ini`, changes made at the same time are kept, unknown entries are preserved, and a file saved with a BOM is read correctly.
- MySQL stops cleanly even when its root password was changed outside Loala. Data from an older layout is only moved to the MySQL version that created it, and an interrupted first setup no longer leaves a broken data folder.
- Automatic backups only back up the database server Loala runs, and failed empty backups no longer push out good ones.
- Reloading reports a port that is already in use. Apache and Nginx reload independently, and a PHP problem in Nginx is reported.
- Long requests to Node.js and Python apps no longer time out after 60 seconds, and uploads through Apache are allowed up to 2 GB, as in Nginx.
- In Nginx, `.php` files inside Node.js and Python projects are no longer run by PHP, and WildcardDNS names are matched regardless of letter case.
- A hosts file saved in another encoding is updated without changing other entries, and it is written in one step.
- Updating replaces the Loala you update from, waits longer for it to close and asks instead of stopping silently, stops leftover servers before replacing files, and explains what to do when antivirus briefly locks a file.
- The settings backup made when updating is no longer overwritten by a reinstall and no longer includes the npm and Go package folders.
- Update checks report when GitHub limits requests, keep a known update after a failed check, and remove an interrupted download.
- Uninstalling stops servers still running from the Loala folder.
- Updating Node.js with Quick add keeps the current version if the new one can't be put in place.
- Quick app keeps one cached download per address, refreshes the latest WordPress after seven days, and keeps the cached copy when a download fails.
- Reloading Apache no longer refuses requests to other sites: Apache re-reads its configuration without stopping, so a request arriving at that moment waits about a second instead of failing. A configuration error is reported and the running Apache keeps serving.
- Mongo Express is no longer reported as failed when it takes longer to start the first time.
- Loala removes a leftover browser data folder (about 80 MB) left behind by older versions.
- The downloaded installer no longer stays in the `tmp` folder after updating.
- Missing Indonesian translations.

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
