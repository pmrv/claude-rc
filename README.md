# claude-rc

User systemd unit that starts `claude remote-control` on login, so sessions
on this machine can be driven from claude.ai/code or the Claude mobile app.

- Working directory: `~/projects` (must be a trusted folder; run `claude`
  there once if not).
- Installed by symlink: `~/.config/systemd/user/claude-rc.service` ->
  `contraptions/claude-rc/claude-rc.service`.

```
systemctl --user daemon-reload
systemctl --user enable --now claude-rc
journalctl --user -u claude-rc -f
```
