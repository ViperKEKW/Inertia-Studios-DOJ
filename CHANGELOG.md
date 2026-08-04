# Changelog — Inertia Studios · DOJ & Court System

## [1.2.0] — 2026-08-03

**Courthouses are placed from inside the game, and saved changes take hold immediately.**

Requires `inertia_lib` **2.1.0** or newer (free, included).

### Added

- **A Courthouses tab.** Stand where the terminal should be, press *Put a courthouse here*, and name
  it. The map blip and the interaction appear straight away. Retiring one removes both and leaves every
  other courthouse exactly where it is.
- Courthouses can be **added and retired, never removed or reordered** — the same rule every positions
  list in the Inertia range follows, and it is enforced on the server rather than left to the panel.

### Fixed

- **The courthouse was always built from the config file, never from your saved settings.** The client
  waited for the config table to exist — and it exists immediately, because config files load before
  client code. Your saved settings arrive later, after a round-trip to the server, so the blip and the
  terminal were placed before they could be applied. This lost the race every time, on every restart.
- **Courthouse interaction zones are removed when the resource stops.** Blips were cleaned up; the
  target zones were not, so every restart while tuning stacked another invisible terminal on the
  courthouse steps.

### Unchanged

The DOJ tab still declares **no operations** and no data lists, and it never will. Judicial authority
is in-character: a Judge is a player's character, not a moderator. Staff configure the court from the
panel; they act inside the court through the court.

## [1.1.0] — 2026-07-30

Configure the court from inside the game. Staff open the Inertia Console, pick the **DOJ & Courts**
tab, and change fees, sentencing limits, hearing scheduling, custody and seizure without editing
files.

### ⚠ New requirement — read this before updating

**`inertia_lib` must be installed and started before `inertia_doj`.** It is free and included with
your purchase. The DOJ previously ran standalone; from this release it will not start without the
shared runtime.

```
ensure inertia_lib
ensure inertia_doj
```

### Added

- **A DOJ & Courts tab in the Inertia Console**: general settings, fees, sentencing ceilings,
  hearings and archiving, custody and bail conditions, asset seizure, and branding.
- **The arming gates are in the panel** — custody, bail, seizure and legal name changes. Each is
  marked sensitive, needs a separate staff permission, makes you type the resource name to confirm,
  and is written to the staff audit log. They are here because the direction that matters in an
  emergency is **off**, and that should never need a server restart.
- **Your config files are never rewritten.** Any setting you changed shows what your file says, with
  one click to restore it.

### Fixed

- **The four background passes now pick up a new cadence from the next pass onward.** Hearing
  reminders, case archiving, custody reconciliation and bail condition checks each read their timing
  once at startup, so changing it saved and did nothing until a restart.

### Changed

- **This tab configures the court; it never acts as the court.** There are no operations in it and
  there will not be any. A Judge is a player's character, not a moderator — a staff panel that could
  file, seal, void or sentence would create a route to judicial power the game itself does not have.

### Removed from the configurable surface

Twenty settings were declared and documented in `config/` but read by **no line of the resource** —
specified behaviour that was never wired up. They are not shown in the panel, because a setting that
saves and changes nothing is worse than no setting. They will return as each is implemented.

Most notably **`Seizure.enabled`**, which read as a master kill switch for the whole seizure system
and was consulted by nothing. Use `Seizure.armed` — that one is real, and it is in the panel.
