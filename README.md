# Tor IP Addresses

The IP addresses of the Tor network: every running relay, and the exit nodes that carry Tor
traffic out to the regular internet.

## Files

| File | Contents | Raw URL |
|---|---|---|
| `tor-nodes.lst` | All running Tor relays (IPv4 and IPv6) | https://raw.githubusercontent.com/SecOps-Institute/Tor-IP-Addresses/master/tor-nodes.lst |
| `tor-exit-nodes.lst` | Exit nodes only | https://raw.githubusercontent.com/SecOps-Institute/Tor-IP-Addresses/master/tor-exit-nodes.lst |
| `Last-Checked-At` | Time of the last successful check (IST) | |

Each file has one IP address per line. Entries are normalized, deduplicated and sorted
numerically, IPv4 before IPv6, with no comments.

**Which file to use:**
- To block or flag traffic *coming from* Tor users, use `tor-exit-nodes.lst`.
- `tor-nodes.lst` is much broader. It includes relays that never send traffic to your servers.

## How it is built

- Primary source: [dan.me.uk](https://www.dan.me.uk/tornodes), `/torlist/` and `/torlist/?exit`.
- Fallback, used when the primary is unavailable or returns a bad list, from the Tor Project itself:
  - [Onionoo](https://onionoo.torproject.org/) running relays, for `tor-nodes.lst`
  - the [TorBulkExitList](https://check.torproject.org/torbulkexitlist), for `tor-exit-nodes.lst`.
    This list is IPv4 only, so IPv6 exits may be missing for that hour.

## Update schedule

**mirabot**, an automated bot, checks **every hour**:
- `Last-Checked-At` is updated on every successful check.
- Tor relays come and go constantly, so these lists change on most runs.

Before publishing, the bot checks each update for problems: minimum size, malformed data, and
any sudden drop of more than half the entries. If a check fails, the previous list stays in
place. If `Last-Checked-At` is more than a few hours old, an update is being held back or the
bot is down.

## License

MIT for this repository. Relay data comes from public Tor network information via dan.me.uk and
the Tor Project.

---
Updated hourly by **mirabot**, sponsored by [endlesstokens.ai](https://endlesstokens.ai) — *Pay for Time not Tokens*.

Maintained by [SecOps Institute](https://github.com/SecOps-Institute) ·
[LinkedIn](https://www.linkedin.com/in/aarvee11) · [Blog](https://amisafe.secops.in)
