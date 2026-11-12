# True North Finder

A single-page survey dashboard that works out true north and south from GPS coordinates, and measures bearings, distances and plot geometry. It is one self-contained HTML file with no build step and no dependencies, and it resizes for phone, tablet and desktop.

## Features

| View | What it does |
| --- | --- |
| **Overview** | Summary tiles for the site: true north, bearing, points inside the plot. |
| **Site and sun** | True north-south line for a coordinate, sun position, solar noon and UTM grid convergence. |
| **Two points** | Bearing, north-south angle (for example `N 45° E`) and distance between two coordinates. |
| **Plot** | Four corners drawn to scale with centre, area, perimeter, side lengths and side bearings. Warns when the sides cross or the corners lie on one line. |
| **From a centre** | A centre plus up to ten points: true bearing, compass bearing, distance and inside/outside the square. Plan view and 360° ring view, both with zoom. |

Other details:

- Inputs accept a `lat, lon` pair, degrees-minutes-seconds, or a full Google Maps link.
- Distances default to feet (square feet for area), with a switch to metres.
- Magnetic declination is set in the top bar. Compass bearing is true bearing minus declination.
- Light and dark themes follow the system setting.
- GPS buttons appear on coordinate inputs when the browser allows location (see Limitations).

## Usage

No installation is needed.

1. Open `true-north-gps.html` in a browser.
2. Use the menu (sidebar on desktop, tab bar on phones) to pick a view.
3. Paste coordinates from Google Maps (right-click a spot, click the coordinates to copy) or tap **GPS**.

### From a centre

1. Enter the four corners A to D in order around the square.
2. Leave "Measure from the centre of the square" ticked, or untick it to type your own centre.
3. Enter one point per line, up to ten.
4. In the **Plan** view, tap a point, corner, chip or table row to see its bearing line and angle from north. Tick "Show every bearing line" to draw all of them.

Bearings run clockwise from true north: 0° north, 90° east, 180° south, 270° west.

## Files

| File | Purpose |
| --- | --- |
| `true-north.html` | Page fragment for hosted artifact use. Source of truth. |
| `true-north-gps.html` | Full standalone document built from the file above. Open this one locally. |

If you edit `true-north.html`, rebuild the standalone file by wrapping it in a document shell (doctype, charset, viewport with `viewport-fit=cover`, a small body reset) and splitting at `<div class="app">` so the head parts come first and the body after.

## How it works

The page has two scripts: `calc` (pure math) and `ui` (DOM, drawing, GPS).

- **Sun and solar noon:** NOAA solar position algorithm.
- **Grid convergence:** UTM zone and convergence for the site.
- **Bearing:** great-circle initial bearing.
- **Distance:** haversine on a 6,371,008.8 m sphere.
- **Plot area and centre:** flat local grid around the plot, shoelace formula.
- **Inside or outside:** ray-casting point-in-polygon.
- **Drawings:** inline SVG, no libraries. Fonts are IBM Plex Sans and Plex Mono from Google Fonts, with system fallbacks.

## Limitations

- **GPS buttons** only work when the file is opened directly in a browser. Inside the hosted artifact frame, location is blocked and the buttons are hidden. Some browsers also refuse location for a saved local file.
- Phone GPS is typically accurate to a few metres. Treat results as a check, not a substitute for a licensed surveyor's instrument work on legal boundaries.
- Plot geometry uses a flat local approximation, which is accurate for plots of ordinary size.
- Ten points maximum in the From a centre tool.

## Browser support

Any current Chrome, Edge, Firefox or Safari. Layout is tested from 390 px (phone) to 1360 px (desktop).

## License

Add a license of your choice before publishing.
