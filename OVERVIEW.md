Devin usage shows your Devin plan's quota consumption in Paseo's Usage surface:
daily and weekly usage percentages with reset times, plus your remaining
on-demand credit balance.

The plugin reads the quota the Devin web dashboard reports for your
organization. It authenticates with the credentials already on your machine:
the Devin CLI login store (`devin auth login`) is picked up automatically, or
you can set `DEVIN_API_KEY` (or `WINDSURF_API_KEY`) and `DEVIN_ORG_ID` in the
daemon's environment. Credentials are read on the daemon host, so agents on a
remote daemon need the login there. The token is sent only to the quota
endpoint of the deployment the login belongs to (`devin_webapp_host` in
`credentials.toml`, `DEVIN_WEBAPP_HOST` for env credentials; default
`app.devin.ai`); nothing else leaves the host.

The quota endpoint is undocumented and may change. When the stored login
expires, the card tells you to run `devin auth login` again. Requires Paseo
0.11 or later.
