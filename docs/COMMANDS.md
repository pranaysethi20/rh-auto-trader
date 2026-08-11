# Two-Way Phone Command Channel

The whole system is controllable from a phone with no laptop, using [ntfy](https://ntfy.sh) as the
transport. The phone **publishes** commands to a secret topic; a scheduled agent (`command-poller`)
**reads** them, validates, executes, and replies to the alerts topic.

## How it works

```
iOS Shortcut ──POST──► ntfy (secret command topic) ──poll──► command-poller ──► executes ──► reply ──► phone
```

- **Send:** an iOS Shortcut POSTs a JSON body `{"topic": "<COMMAND_TOPIC>", "message": "<PASSPHRASE> <command>"}`
  to `https://ntfy.sh`.
- **Read:** the poller runs every 10 min (7am–11pm) and reads new messages via
  `https://ntfy.sh/<COMMAND_TOPIC>/json?poll=1&since=30m`.
- **Security:** the topic name is unguessable **and** every command must begin with a passphrase.
  Messages without the exact passphrase are silently ignored (no reply — so an attacker can't even
  confirm the channel exists). A dedup guard (last-processed timestamp) prevents double-execution.

> Secrets — the real `<COMMAND_TOPIC>` and `<PASSPHRASE>` — are **not** in this repo. They live in
> private local notes only.

## Command reference

Every command is: `<PASSPHRASE> <command>`

| Command | Effect |
|---|---|
| `status` | Full account snapshot replied to the phone (value, positions + P&L, autopilot state, goal gap). |
| `cut <SYMBOL>` | Cancels the symbol's stop, sells the full position at market. |
| `levels <ENTRY> <STOP> <TARGET>` | Retunes the autopilot's fixed levels; it re-arms on those next run. |
| `buy <SYMBOL> <QTY> <LIMIT>` | Places a GTC buy-limit (used to rotate into a new stock). |
| `pause` | Halts new autonomous entries (existing position still managed). |
| `resume` | Re-enables entries. |

## iOS Shortcut setup (one time)

1. **Shortcuts app** → new shortcut → **Add Action**.
2. **Ask for Input** (Text) — prompt "Command".
3. **Get Contents of URL**:
   - URL: `https://ntfy.sh`  *(plain — no variable in the URL field)*
   - Method: **POST**
   - Request Body: **JSON**, two Text fields:
     - `topic` = `<COMMAND_TOPIC>`
     - `message` = `<PASSPHRASE> ` + the **Provided Input** variable (note the trailing space after the passphrase)
4. Name it, add to Home Screen for one-tap, or trigger with Siri.

To use: run it → type just the command part (e.g. `status`, `cut kre`, `levels 17.6 16.9 19.5`).

## Two topics, don't confuse them

- **Command topic** (secret) — the phone *publishes* here; you don't need to subscribe to it (and
  subscribing just echoes your own commands back, which is noise).
- **Alerts topic** — the phone *subscribes* here to receive all replies, fills, proposals, summaries.
