# claude-rc

User systemd unit that starts `claude remote-control` on login, so sessions
on this machine can be driven from claude.ai/code or the Claude mobile app.

- Working directory: `~/projects` (must be a trusted folder; run `claude`
  there once if not).
- The session is named `<hostname>-concierge` (`--name`, from `%H` in the unit).
- Persistent session: the unit runs `claude-rc-start`, which reattaches to the
  session last recorded for the working directory (`--continue`) and only
  creates a fresh one when there is nothing to continue. `--continue` only
  finds sessions recorded within roughly the last 4 hours, so after a longer
  downtime a new session is created.
- To pin one fixed session regardless of age, put its ID in
  `~/.config/claude-rc/env` as `CLAUDE_RC_SESSION_ID=<id>` (uses
  `--session-id`; remove the line to return to `--continue`).
- Installed by symlink: `~/.config/systemd/user/claude-rc.service` ->
  `~/projects/claude-rc/claude-rc.service`.

```
systemctl --user daemon-reload
systemctl --user enable --now claude-rc
journalctl --user -u claude-rc -f
```
