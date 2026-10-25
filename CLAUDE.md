# pace-birdsfoot

Single-file pace-of-play app (`index.html`).

## Releasing a change

Every change that someone using the app would notice gets a new version and a
"What's new" entry:

- Add an entry at the top of the `CHANGES` list in `index.html`: the new version
  and one or two short, plain-language lines written for whoever is using the
  phone, not developers. The version label at the bottom of the page is read
  from that first entry, so don't edit the label itself.
- Use the same version in the commit subject: `vX.Y: <summary>`.
- If the version has been pushed already, the next change goes in a new version.
