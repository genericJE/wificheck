# wificheck

A tool to notify you when an unstable Wi-Fi connection comes back online.
Inspired by flakey cafe internet connections <3

```
  \   /
   \ /
   (•)>
  ● Wi-Fi down — waiting on carrier pigeon… (7s)
```

## Install

### Homebrew

```sh
brew install genericJE/tools/wificheck
```

### Manual

```sh
curl -o /usr/local/bin/wificheck https://raw.githubusercontent.com/genericJE/wificheck/main/wificheck
chmod +x /usr/local/bin/wificheck
```

## Usage

```sh
wificheck                    # ping until the connection is up
wificheck -r                 # watch a live connection; notify if it drops
wificheck -q                 # quiet (no `say`)
wificheck -s                 # static; skip the animation, plain status line
wificheck -d 8.8.8.8         # ping a different host
wificheck -t 5               # give up after 5 minutes
wificheck -i 5               # ping every 5 seconds (default: 1)
```

### Options

| Flag | Description |
|---|---|
| `-r`, `--reverse` | Watch a live connection; notify after 3 consecutive failures |
| `-s`, `--static` | Skip the ASCII animation; show a plain status line |
| `-q`, `--quiet` | Suppress the spoken notification (`say`) |
| `-d`, `--dns <host>` | DNS/host to ping (default: `1.1.1.1`) |
| `-t`, `--timeout <mins>` | Give up after this many minutes (forward mode) |
| `-i`, `--interval <secs>` | Seconds between ping attempts (default: `1`) |
| `-h`, `--help` | Show help |

### Environment

| Variable | Description |
|---|---|
| `WIFICHECK_DNS` | Default ping target. Overridden by `-d`/`--dns`. |

## Behaviour

**Forward mode** (default) — pings until the connection is up:
- First ping succeeds → "Internet is working"
- Later ping succeeds → "Internet is working again"
- Timeout reached → "Internet is not working. Tried for N minutes to reach `<host>` without success."

**Reverse mode** (`-r`) — pings while the connection is up:
- After 3 consecutive failures → "Internet is not working"

## Requirements

- macOS (uses `say` for the spoken notification)
- `bash` and `ping` (both stock)

## License

MIT

If anything here ends up being useful to you and you feel like saying thanks, my PayPal is https://paypal.me/genericJE. Truly no expectation either way, just leaving the option here in case.
