# devin-usage-source

Devin plan usage in Paseo — daily and weekly quota bars plus your on-demand
credit balance, in the Usage surface and sidebar.

## Install

```
paseo plugin install git:ryosuz/paseo-devin-usage
```

Plugins must be enabled in the daemon (`pluginsEnabled` in config.json).
Reload or restart the daemon after enabling.

## Authentication

The plugin reads credentials on the daemon host. Env credentials take
precedence over the CLI login for the same organization:

1. **Environment variables**: set `DEVIN_ORG_ID` plus `DEVIN_API_KEY` or
   `WINDSURF_API_KEY` in the daemon's environment. The bearer token and org id
   can be copied from a `billing/quota/usage` request in your browser's
   developer tools on `app.devin.ai`. Manually copied session tokens expire.
2. **Devin CLI login** (zero config): if you ran `devin auth login`, the
   session token in `~/.local/share/devin/credentials.toml` and the org id in
   `~/.config/devin/config.json` are used automatically (XDG data/config dirs
   and Windows `%APPDATA%` locations are honored). Re-running
   `devin auth login` refreshes an expired token; the plugin picks it up on
   the next fetch.

Skip this plugin if your Paseo build already ships `devin-usage-source` as a
built-in — the plugin and usage-source IDs are reserved by the bundled copy.

Quota requests go to the deployment the login belongs to — the
`devin_webapp_host` recorded in `credentials.toml`, or `DEVIN_WEBAPP_HOST`
for env credentials. Default is `app.devin.ai`.

If the daemon runs on a remote host, credentials must exist on that host.

## Notes

- Uses the undocumented `billing/quota/usage` dashboard endpoint, so it can
  break if Cognition changes it.
- Accounts on a non-quota plan show "No Devin quota plan" instead of bars.
