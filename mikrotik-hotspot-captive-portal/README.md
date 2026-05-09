# Mikrotik hotspot captive portal

Branded captive portal for **MikroTik RouterOS Hotspot** — Harmony Bangkok WiFi.

## Preview

| Page | Purpose |
|---|---|
| `login.html` | WiFi sign-in form |
| `alogin.html` | Post-login spinner ("Signing you in") |
| `welcome.html` | Welcome screen with **Continue to the internet** button |
| `status.html` | "You are connected" + **Log out** button |
| `logout.html` | Confirmation after logout |
| `error.html` | Branded error page |
| `rlogin.html` | 302 redirect to login (captive portal trigger) |
| `redirect.html` | MikroTik internal redirect handler |
| `errors.txt` | Localized error messages |
| `radvert.html` | RADIUS advertisement page (optional) |
| `md5.js` | CHAP password hashing |
| `img/logo.jpg` | Brand logo |

## Flow

```
WiFi connect → rlogin.html (302) → login.html → alogin.html → welcome.html
                                                                    ↓
                                              [Continue] → original URL / google.com

Gateway IP visit → status.html → [Log out] → logout.html
```

## Deployment

1. **Winbox → Files** → delete existing `hotspot-harmony-final` folder
2. Drag the entire local `hotspot-harmony-final/` folder into Files
3. Refresh hotspot service:
   ```
   /ip hotspot disable [find]
   /ip hotspot enable [find]
   ```
4. Confirm the profile points at this folder:
   ```
   /ip hotspot profile print
   ```
   Look for `html-directory=hotspot-harmony-final`.
5. Test: forget WiFi → reconnect → open `http://neverssl.com` → walk the flow.

## Customization

- **Logo:** replace `img/logo.jpg` (recommended ≤ 240 px wide)
- **Brand colors:** primary `#d9462a`, accent `#2dab4f` — search & replace in CSS
- **Error messages:** edit `errors.txt` (supports any language)
- **Default destination** when no original URL: edit `welcome.html` button `href`

## Compatibility

Tested on RouterOS 6.49 and 7.x. Standard MikroTik hotspot template tags `$(...)` are used throughout — see [MikroTik Hotspot HTML wiki](https://wiki.mikrotik.com/wiki/Manual:Customizing_Hotspot) for reference.

---

Built for MikroTik captive portal · generated with Claude Opus 4.7
