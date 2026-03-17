# NULL//TRACE

> *A browser-based hacking roguelike. Terminals, networks, social engineering, and a handler who knows more than they're telling you.*

---

NULL//TRACE is a single-file browser game — no server, no install, no dependencies. Open the HTML file in Chrome or Edge and you're in a simulated OS shell. You play as a freelance network operator taking contracts to breach corporate networks, exfiltrate data, and disappear without a trace.

Every run is different. The target company, its employees, its network topology, and the files inside it are all procedurally generated. The tools are real. The attack chains mirror actual penetration testing methodology. Getting caught means starting over.

---

## Getting Started

**Requirements:** Chrome or Edge (file:// protocol supported). No installation needed.

1. Download `NULL_TRACE_V1.html`
2. Open it in Chrome or Edge
3. Log in as `ghost_0x1` / `null1234` to play
4. Log in as `trainee` / `learn` for a guided walkthrough

That's it.

---

## The Core Loop

Each run follows the real-world penetration testing kill chain:

```
Recon → Scan → Exploit → Exfil → Cover tracks → Disconnect
```

You start with a fresh alias, a small credit balance, and a contract board. You pick a target, equip your tools, connect to the network, find credentials, escalate access, steal files, delete your logs, and get out. The trace meter climbs while you're connected — if it hits 100% before you disconnect, the session burns and you die.

Between runs your reputation and tool unlocks persist. Each run gets harder as your difficulty tier increases.

---

## Two Accounts

### `ghost_0x1` / `null1234` — Operator
The main game. Procedurally generated targets, a full contract board, SPECTR narrative, achievements, career progression. No hand-holding.

### `trainee` / `learn` — Training Mode
A guided tutorial set in a locked-down two-node sandbox. SPECTR acts as your trainer, reacting to each step and telling you exactly what to type next. The tutorial network, mail, and contract board are isolated from the operator game. Complete it and log back in as the operator.

---

## Gameplay Systems

### Terminal
A fully functional simulated OS shell. Command history, tab completion (context-aware — completes node names, file paths, employee emails, and tool flags), and 56 commands including real Unix filesystem operations, network tools, hacking tools, and social engineering commands.

### Network Map
An SVG node graph showing the active network. Zone borders (PUBLIC / INTERNAL / EXEC) group nodes by security tier. Click any node to see its state. Pan with mouse or touch drag. Nodes show real-time security state, firewall status, and connection indicators.

### Contracts and Missions
A contract board refreshes each run with procedurally generated operations. Seven contract types:

| Type | Tools Required | Objective |
|------|---------------|-----------|
| DATA_EXTRACT | scan, connect, exfil | Steal sensitive files from a target org |
| CREDENTIAL_HARVEST | phish, login | Harvest credentials via social engineering |
| SABOTAGE | connect, escalate trace | Trigger INCIDENT state and vanish |
| GHOST_OP | everything, quietly | Complete objectives without raising alarms |
| SOCIAL_ONLY | phish, impersonate, login | Social engineering only — no technical exploits |
| WEB_EXPLOIT | gobuster, nikto, sqlmap | Web attack chain against vulnerable HTTP stack |
| CREDENTIAL_ATTACK | enum4linux, hydra | Enumerate and brute-force network credentials |

Each contract generates objectives with inline hints, an intel panel with tool recommendations, and a payout scaled to difficulty tier.

### Security FSM
Every node has a security state machine: `NOMINAL → SUSPICIOUS → INCIDENT → LOCKDOWN`. Noisy actions (fast scans, brute-force, nikto) raise the trace meter and can trigger security escalations. Escalation speeds up the trace timer, rotates passwords, and eventually locks down the entire org.

### Tools and Loadout
Four tiers of tools across five categories (Scanner, Cracker, Exfil, Stealth, OSINT). Equip up to four in your loadout slots. Tools modify passive stats — trace rate, scan speed, exfil value, stealth multiplier. Tool synergy combos unlock additional bonuses. Tier 4 tools (8,000 cr) require multiple successful runs to afford.

### Procedural Org Generator
Every proc-gen target is built from scratch: a company name (from 14 industries × 20 adjectives × 20 nouns), 5–10 employees with names, roles, hobbies, pets, email patterns, and security awareness levels, a realistic filesystem with role-specific files and lore dead drops, and a network topology (FLAT, SEGMENTED, HUB_SPOKE, or MESH) scaled to difficulty.

### Difficulty Scaling
Four tiers based on career run count: ROOKIE → OPERATOR → VETERAN → GHOST. Each tier tightens trace rates, raises security awareness, adds IDS response speed, and increases contract difficulty. Objective rewards scale up with difficulty to compensate.

---

## Hacking Commands

### Core Operations
```
scan [node]                  probe a node for open services and OS
connect [node]               establish a session on a node
disconnect                   cleanly exit the current session
fw-unlock [node] [user] [pass]  bypass a firewalled node
crack [file]                 run password cracker against a hash file
exfil [file]                 exfiltrate a file to your local vault
scp [remotefile] [localdest] quietly copy a file (low noise, no vault)
rm-logs                      delete session logs on current node
```

### M11 Hacking Tools
```
gobuster dir -u http://[node] -w [wordlist]   web directory enumeration
nikto -h [node]                               web vulnerability scan (loud)
sqlmap -u "http://[node]/path?q=1" --dbs      SQL injection and data dump
hydra -l [user] -P rockyou ssh://[node]       credential brute-force
nc -lvnp [port]                               open reverse shell listener
enum4linux -a [node]                          SMB/Windows enumeration
```

Each tool has a full `man [tool]` documentation page and `--help` flag.

### Filesystem
```
ls [path]        cd [path]      cat [file]     mkdir [dir]
touch [file]     rm [file]      rm *           rm -rf [dir]
mv [src] [dest]  cp [src] [dest]  nano [file]  grep [pattern] [file]
grep -r [pattern] [dir]          ps             kill [pid]    chmod
```

### Social Engineering
```
phish list-targets               show all employees and awareness levels
phish [email]                    send a phishing email
phish [email] --template [id] --from [email]   targeted spear-phish
phish list-templates             8 available templates (IT reset, CEO wire, etc.)
impersonate [email]              set FROM identity for phish campaigns
login [user] [pass]              authenticate as a stolen identity
```

### System
```
nodes            list all network nodes and firewall states
secstate         security state of all nodes
status           connection, trace, and proxy status
proxy status     show proxy chain and trace protection
difficulty       current difficulty tier and stats
sound            toggle sound effects
music            toggle ambient music
man [tool]       full documentation for any tool
help             all commands
```

---

## Apps (Windows)

| App | Key | Description |
|-----|-----|-------------|
| NET//MAP | map | Visual network graph, zone regions, live node states |
| MAIL// | mail | In-game email — SPECTR messages, admin alerts, social engineering results |
| BOARD// | board | Contract board with objectives, intel, and payout |
| MISSION// | mission | Active contract objectives with inline hints |
| FORGE// | forge | Tool market and loadout management |
| PHISH// | phish | Phishing campaign builder with template preview |
| INTEL// | intel | Accumulated OSINT — credentials, user data, vulnerabilities |
| FEED// | feed | Procedural news feed — your past operations appear as headlines |
| META// | meta | Career overview and achievement tracker |
| SEC//MON | secmon | Real-time security event monitor |
| SYS// | sysmon | System status, difficulty profile, run stats |

Open any app: `open [appname]` or via the taskbar APPS button.

---

## Narrative — SPECTR

SPECTR is your handler. Not an employer — something between a mentor and a watcher. They communicate exclusively through encrypted mail, leaving brief, precise messages that reveal more about the world of NULL//TRACE than any contract briefing does.

The narrative unfolds across 17 triggers that fire based on your career milestones — first breach, first death, run count thresholds, achievement unlocks, and tier transitions. Ghost presence lines occasionally inject into your active terminal mid-session.

Starting around run 12, a second faction makes contact. Their mail looks different — darker, no signature, origin unknown. SPECTR goes quiet. Then comes back. The story is in the gaps.

---

## Achievements

15 career achievements tracked in META//:

| Achievement | How to unlock |
|-------------|---------------|
| Ghost Operator | Complete a full run without triggering SUSPICIOUS on any node |
| Speed Runner | Complete a run in under 3 minutes |
| Archivist | Read every file in a proc org |
| Social Butterfly | Phish 5 or more employees in a single run |
| Bulldozer | Trigger INCIDENT on a FLAT topology network |
| Surgeon | Exfil a HIGH value file without ever connecting to more than 2 nodes |
| ... and 9 more | Tracked across career, never reset |

Achievements trigger unique SPECTR reactions when SPECTR notices you've unlocked them.

---

## Save System

Progress saves at three points:
- **On disconnect** — mid-run state saves automatically each time you exit a node
- **On shutdown/logout** — full state saves before returning to the login screen
- **On tab close** — `beforeunload` handler saves and disconnects cleanly if you close the browser

Logging back in restores your run exactly where you left it — alias, credits, objectives, tools, exfil vault, intel, and network state. Career META (reputation, achievements, story flags) persists permanently in `localStorage`.

To reset everything: type `resetmeta` in the terminal.

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Tab` | Context-aware autocomplete (commands, paths, node names, emails, flags) |
| `↑ / ↓` | Command history |
| `Ctrl+Space` | Command palette |
| `Alt+T` | New terminal window |
| `⏻` (taskbar) | Save and return to login screen |

---

## Sound and Music

**Sound effects** (`sound` to toggle): connect/disconnect tones, exfil blip, objective fanfare, trace warning pulses, SPECTR mail chime, achievement arpeggio, firewall unlock sequence, and death rumble. All generated via Web Audio API — no files.

**Ambient music** (`music` to toggle): a procedural dark synth layer — 42Hz sub-bass drone, filtered sawtooth pad with slow LFO sweep, sparse glitch pings, and a slow bass pulse. Fades in on boot, varies slightly each session. Both settings persist across sessions.

---

## Technical

- Single HTML file (~426KB) — no server, no dependencies, no install
- Runs on `file://` protocol in Chrome and Edge
- Web Audio API for all sound generation
- SVG for the network map
- `localStorage` for all persistence
- Vanilla JavaScript throughout

---

## Roadmap

The game is at **V1.0** — a complete playable roguelike with multiple runs of content. Planned expansions:

- **M12** — Metasploit workflow, privilege escalation chains, Meterpreter post-exploitation
- **M13** — New target biomes: home/IoT networks, CTF challenge nodes, SCADA/industrial targets
- **M14** — Active Directory attack chain: Responder → Hashcat → BloodHound → DCSync
- **M15** — Honeypot and deception networks: Cowrie, Endlessh, canary tokens
- **M16** — Home base and C2 infrastructure: proxy chains, beacon management, OpSec heat
- **M17** — OSINT depth and social engineering expansion: Shodan queries, vishing, USB drops
- **Godot port** — Native desktop build preserving the full terminal aesthetic

---

## Credits

Built as a solo browser project. The attack chains, tool syntax, and security concepts draw from the real-world methodology of educators including John Hammond, IppSec, Heath Adams (TCM Security), LiveOverflow, and NetworkChuck — all of whom teach ethical hacking and penetration testing publicly.

No real systems were harmed. All networks, companies, employees, and credentials are procedurally generated fiction.

---

*Don't get traced.*
