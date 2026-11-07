# DeckForge

An Android deck builder and collection tracker for Magic: The Gathering, built around ManaBox CSV
exports and Scryfall data. Offline first: the card index, rulings, set symbols and art cache all
live on the device.

## Shared deck links

Deck links are served from this repository by GitHub Pages:

```
https://soharuda.github.io/DeckForge/?d=<payload>
```

`docs/index.html` is the viewer, and it does one thing: show a deck. It is a single static page
with no dependencies (no CDN, no framework): the deck rides in the `d` query string as base64url of
gzipped JSON, the page unpacks it with the browser's own gzip support, then looks the printings up
on Scryfall for names, art, mana costs and prices. Cards are grouped by type and sorted by mana
value, each row shows the art, and tapping a row opens the card full size: swipe (or arrow keys) to
walk the whole deck in the same order the list is drawn. Nothing is stored server side, and no collection data is embedded in the page. The same file
is bundled in the app as `assets/vault-viewer.html`, so a shared page file opens on the same view. The payload looks like this:

```json
{"v":1,"kind":"deck","name":"Leech","format":"commander","formatLabel":"Commander",
 "commander":"Clavileño, First of the Blessed","commander2":null,"count":100,
 "lines":[[1,"LCC","302",0,"Sol Ring","main","<scryfall printing id>"]]}
```

`lines` entries are `[quantity, set, collector number, foil quantity, name, board, printing id]`.
`board` is `main`, `commander`, `companion` or `side`.

## Pages

- Source: `main`, folder `/docs`
- Enforced HTTPS, built automatically on push to `main`
- `.nojekyll` is present so the folder is served exactly as committed
