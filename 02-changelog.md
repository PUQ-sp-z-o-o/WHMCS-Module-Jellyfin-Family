# Changelog

### Jellyfin Family module **[WHMCS](https://puqcloud.com/link.php?id=77)**
#####  [Order now](https://puqcloud.com/whmcs-module-jellyfin-family.php) | [Download](https://download.puqcloud.com/WHMCS/servers/PUQ_WHMCS-Jellyfin-Family/) | [Community](https://community.puqcloud.com/)

---

## v3.0 (01-07-2026)

Full rewrite onto the PUQ module skeleton (shared with the other PUQ WHMCS modules).

**Added**
- AJAX, card-based client area with a gradient status hero, a two-column account/usage layout, usage progress bars (sessions, failed logins), library chips, an active-devices table and a **media-accounts** card — plus toast notifications and confirm dialogs.
- **AJAX media accounts (Family).** Clients add, edit and delete media accounts in a modal, pick their libraries with checkboxes, toggle each on/off and drop its devices — all without a page reload. The old `?action_m=` sub-pages are replaced. The number of media accounts is set per product (*Media Accounts Configuration → Count of media accounts*).
- Suspend / Unsuspend / Change package / Terminate now **cascade to every media account** (disable, re-enable to the stored state, re-apply policy, or delete).
- Admin service tab shows a **Media Accounts** table (enabled state, username, enabled libraries).
- Self-service **Drop all devices** and **Unblock** actions in the client area (no page reload).
- **Dynamic library picker** in the product configuration form: the library list is loaded live from the assigned Jellyfin server as checkboxes, with a *Select all* toggle and a *Reload* button (with a manual text-box fallback when the server is unreachable). The separate *Use all libraries* switch is kept.
- Product configuration form injected on the WHMCS product page via `AdminAreaFooterOutput`.
- Admin homepage license alert listing products with invalid or missing licenses.
- Automatic schema setup — the module self-creates its `puq_license` and `puqJellyfinFamily_media_account` tables on load (no SQL to run).
- **Diagnostic logging throughout.** Every lifecycle action, hook and AJAX call records its result and any exception to the WHMCS Module Log; all Jellyfin API calls log their request/response on error (and every write call on success), with the HTTP status code and the real Jellyfin message. Passwords are redacted in the log.

**Changed**
- **Jellyfin 10.11.10+ compatibility.** Switched to the modern `Authorization: MediaBrowser` header (with `Version`) as the primary scheme and dropped the deprecated `X-Emby-Token` / `X-MediaBrowser-Token` headers that Jellyfin removes in 10.12/10.13. The password endpoint now uses the current route `Users/Password?userId=` instead of the deprecated `Users/{id}/Password`.
- `CreateAccount` now reads the new user's `Id` directly from the `Users/New` response instead of re-listing all users and matching by name (faster and robust against special characters).
- API error handling now inspects the HTTP status code and extracts the real Jellyfin error message (ProblemDetails / validation errors) instead of occasionally treating a 4xx as success.
- All product settings are now stored as a single JSON document in `configoption24`. Existing v2 installs are read transparently from the legacy `configoption2`–`configoption8` slots (including *Media Accounts Configuration* in `configoption2`), so **no reconfiguration is required** after upgrading.
- License verification moved to a block-based hash with online/offline caching.
- Jellyfin admin API token is cached per instance instead of re-authenticating on every call.
- PHP **7.4 / 8.1 / 8.2+** compatible source; hardened with null-safe reads, `try/catch` around all external calls, and `htmlspecialchars` on every API-sourced string.

**Fixed**
- Web-interface URL no longer mishandled the plain-HTTP/port-80 case (operator-precedence bug in the default-port check).
- Empty text fields (e.g. an intentionally blank username suffix) are now preserved instead of reverting to their default on save.

**Removed**
- Legacy `lib/functions.php`, `lib/puqJellyfinFamilyLicense.php`, `lib/puqJellyfinFamilyPackageOption.php` and the old `templates/include/header.tpl` (folded into the new skeleton).

## v2.1

- Previous public release.
