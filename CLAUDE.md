# pace-birdsfoot

Single-file pace-of-play app (`index.html`) for Birdsfoot golf course staff,
used on a phone.

## Structure

- Everything is in `index.html`: inline CSS and JS, no build step, no
  dependencies.
- Hosted on GitHub Pages from `main` at https://vpciii.github.io/pace-birdsfoot/.
  Pushing to `main` deploys, and every file in the repo is publicly served.
- `robots` is set to noindex, nofollow. Keep it that way.

## How pace is computed

- `CHECKPOINTS`: `[holesPlayed, expectedMinutesFromTee]` pairs (for example,
  9 holes in 130 minutes).
- `PARS` holds the par of holes 1–18. Between checkpoints, the expected time is
  split by `PAR_WEIGHT` (par 3/4/5 = 10/14/17).
- Groups can start on any hole (`startHole`). `playOrder` and `holeOfPlayed`
  convert between a hole's number and its place in the group's round.
- Group "B" runs `settings.bGap` minutes behind group A. A delta of
  `settings.lateMin` or more is "late", and anything above 0 is "behind".

## State (localStorage)

- `pace-settings`: user settings, checked against `LIMITS`.
- `pace-state`: the current check. `pace-carts`: saved carts with notes. Since
  v1.5 these persist until cleared by hand (New, ×, Clear all).
- When you change a stored shape, keep loading data saved by older versions
  (see the v1.2 `selectedHole` migration in `loadState`).
- Wrap every localStorage access in try/catch.

## UI conventions

- Mobile-first: 480px max width, safe-area insets, large tap targets, dark
  green theme set by `:root` variables.
- Check changes at phone width (375px) before pushing.

## Releasing a change

Every change that someone using the app would notice gets a new version and a
"What's new" entry:

- Add an entry at the top of the `CHANGES` list in `index.html`: the new version
  and one or two short, plain-language lines written for whoever is using the
  phone, not developers. The version label at the bottom of the page is read
  from that first entry, so don't edit the label itself.
- Use the same version in the commit subject: `vX.Y: <summary>`.
- If the version has been pushed already, the next change goes in a new version.
