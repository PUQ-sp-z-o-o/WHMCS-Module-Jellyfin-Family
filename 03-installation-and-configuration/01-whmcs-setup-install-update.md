# WHMCS setup (install/update)

### Jellyfin Family module **[WHMCS](https://puqcloud.com/link.php?id=77)**
#####  [Order now](https://puqcloud.com/whmcs-module-jellyfin-family.php) | [Download](https://download.puqcloud.com/WHMCS/servers/PUQ_WHMCS-Jellyfin-Family/) | [Community](https://community.puqcloud.com/)

## Technical requirements

The **PUQ Jellyfin Family** module is encoded with **ionCube Loader v13** (or newer) and is published as a separate build for each supported PHP major version. Installation and updates follow the same procedure.

| PHP version | WHMCS version   | Module build |
|-------------|-----------------|--------------|
| PHP 7.4 | 8.11.0 -        | `php74` |
| PHP 8.1 | 8.11.0 +        | `php81` |
| PHP 8.2 (or newer) | 8.11.0 + and 9+ | `php82` |

> Pick the build that matches the **PHP runtime of your WHMCS server**, not the WHMCS version — PHP 8.2 and any newer PHP always use `php82`. Not sure which PHP version your WHMCS runs on? Check **Utilities → System → PHP Info** in the WHMCS admin area.

A reachable **Jellyfin server, version 10.11.10 or newer**, with an administrator account and an API key, is also required.

---

## Download

A separate build is published for each PHP major version. All versions and historical builds are available in the index:

- [https://download.puqcloud.com/WHMCS/servers/PUQ_WHMCS-Jellyfin-Family/](https://download.puqcloud.com/WHMCS/servers/PUQ_WHMCS-Jellyfin-Family/)

### Direct "latest" downloads

#### PHP 8.2

```bash
wget https://download.puqcloud.com/WHMCS/servers/PUQ_WHMCS-Jellyfin-Family/php82/PUQ_WHMCS-Jellyfin-Family-latest.zip
```

#### PHP 8.1

```bash
wget https://download.puqcloud.com/WHMCS/servers/PUQ_WHMCS-Jellyfin-Family/php81/PUQ_WHMCS-Jellyfin-Family-latest.zip
```

#### PHP 7.4

```bash
wget https://download.puqcloud.com/WHMCS/servers/PUQ_WHMCS-Jellyfin-Family/php74/PUQ_WHMCS-Jellyfin-Family-latest.zip
```

---

## Installation

### Step 1: Extract the archive

On your WHMCS server (or locally, before uploading):

```bash
unzip PUQ_WHMCS-Jellyfin-Family-latest.zip
```

### Step 2: Deploy the module

Copy and replace the `puqJellyfinFamily` folder into the WHMCS servers module directory, so the module lives at `WHMCS_WEB_DIR/modules/servers/puqJellyfinFamily/`:

```
puqJellyfinFamily  →  WHMCS_WEB_DIR/modules/servers/puqJellyfinFamily/
```

Example:

```bash
cp -r puqJellyfinFamily /var/www/html/whmcs/modules/servers/
```

Make sure **ionCube Loader v13+** is enabled for the PHP version WHMCS runs on. On first load the module self-creates its database tables (`puq_license` and `puqJellyfinFamily_media_account`) — there is no SQL to run manually.

### Step 3: Next steps

1. [Add a Jellyfin server in WHMCS](02-create-new-server.md) — connect WHMCS to your Jellyfin server.
2. [Product configuration](03-product-configuration.md) — create the **PUQ Jellyfin Family** product, enter the license key and configure the access policy.

---

## Update

Installation and updates follow the same procedure. To update an existing installation:

1. Back up the WHMCS database and the `modules/servers/puqJellyfinFamily/` directory.
2. Download the new build that matches the current PHP version and overwrite all files in `modules/servers/puqJellyfinFamily/`.
3. Open any WHMCS admin page once — the module verifies and creates any missing database tables automatically.

> Upgrading from **v2.x**: no reconfiguration is required. The module reads existing product settings from the legacy `configoption2`–`configoption8` slots (including *Media Accounts Configuration* in `configoption2`) until you save the product once through the new form, at which point they are consolidated into `configoption24`.

> **Tip:** always back up your WHMCS installation before performing an update.
