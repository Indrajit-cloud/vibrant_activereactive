# AmbuQuick

Repository: `vibrant_activereactive`

AmbuQuick is a lightweight front-end demo for ambulance booking and location simulation using Leaflet and the browser Geolocation API.

## What this repo contains

- `index.html` — single-page UI with a Leaflet map, booking UI, SOS flows, a simple chatbot mock, and utilities for geolocation and simulation.
- Styles and scripts are embedded in `index.html` and use CDN-hosted Leaflet and Font Awesome.

## New features (added)

- Real geolocation tracking using the browser Geolocation API (watchPosition).
- Simulation mode that plays a small sample route and updates the user marker.
- Manual mode to set coordinates by hand.
- Dynamic hospital list: a local `hospitals` dataset is used to populate the booking modal; distances to each hospital are calculated with the Haversine formula and shown in the select options.
- Nearest hospital is auto-selected and hospital markers (with popups showing distance) are added to the map.
- Booking confirmation includes the selected hospital name and straight-line distance from the current location.

## How to run (recommended)

Some browsers restrict geolocation on `file://` pages. Use a simple local static server (Python is handy). From the repository root run:

```powershell
# serve current directory on port 8000
python -m http.server 8000

# then open in your browser:
# http://localhost:8000
```

Notes:
- Geolocation (real mode) requires HTTPS or `localhost` in most browsers. Running the server above and opening `http://localhost:8000` is sufficient for testing geolocation locally.
- Simulation mode does not require geolocation permission.

## How to test the features

1. Open `http://localhost:8000` in your browser.
2. Allow location access when prompted to test Real mode (the map will center on your location and hospital distances will update live).
3. Use Location Mode controls (Real / Simulate / Manual):
	- Real: starts live tracking (watchPosition). Hospitals update as the location changes.
	- Simulate: shows a sample route and moves the user marker; hospital distances refresh during simulation.
	- Manual: enter Latitude / Longitude and click Set to place the user marker manually; hospital distances update.
4. Open the Book Ambulance modal: the hospital dropdown shows names and distances; the nearest hospital is auto-selected. Selecting a different hospital updates the displayed distance.

## Implementation notes & limitations

- Distances are straight-line (great-circle) distances computed with the Haversine formula. They are not driving distances or travel times.
- For production-grade shortest-route and ETA calculations consider integrating a routing API (OSRM, Mapbox Directions, Google Directions). That would replace straight-line distance with route distance/time.
- Hospital data is currently an in-file array inside `index.html`. You can replace it with a server-served JSON endpoint and fetch it to populate the list dynamically.

## Next suggestions (optional)

- Integrate a routing API for driving distance / ETA and pick the true shortest route.
- Allow upload/draw of custom simulation routes or fetch real ambulance locations from a backend.
- Persist user mode (real/sim/manual) to localStorage.

## License

This project uses the repository's LICENSE (see `LICENSE`).