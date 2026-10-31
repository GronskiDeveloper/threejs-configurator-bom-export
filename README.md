# Cabinet configurator with a bill of materials you can export

A small Three.js starter. Configure a cabinet, and the parts list builds itself from the same numbers: boards with cut sizes in millimetres, shelf pins, screws, running metres of edge banding. One button exports it as CSV.

The point is the handoff. A lot of configurators look great and then stop at the 3D view, so someone in the office retypes the dimensions into a cutlist by hand. That is where the errors come from. If the config already knows the geometry, it already knows the parts. The factory should get them straight.

## How it works

- `build()` draws the cabinet from width, height, depth and shelf count.
- `bom()` reads the same four numbers and returns the cut list: panel sizes, hardware counts, edge banding in metres. Nothing is typed in by hand, it all derives from the structure.
- `exportCsv()` turns that into a CSV a workshop can open.

Read [`index.html`](index.html), the geometry and the BOM come from one source of truth.

## Run it

```bash
npx serve .
# or
python -m http.server 8000
```

## What this is

An educational starter: generic cabinet, chipboard assumptions, clean code, MIT. The numbers are plausible, not a real cutting program.

A production system carries your real board library, kerf and trim allowances, grain direction, nesting and offcut optimisation, and your own hardware catalogue. That is custom work, and it is usually where the money is, because it removes a manual step that was costing the manufacturer orders.

## About

I build custom 3D product configurators for manufacturers, including the unglamorous part: turning a configuration into something the factory floor can actually build from.

- https://grodev.pl/konfigurator-produktowy-3d
- https://grodev.pl/en/custom-3d-configurator

Dominik Groński, GroDev, Poznań.

## License

MIT, see [LICENSE](LICENSE).
