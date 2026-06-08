# Parcelle

Geneva cadastral parcel intelligence. React plus Vite single-page app. The map drills Canton GE into 45 communes and then into individual parcels, pulling official SITG data live (cadastre, buildings, surélévation flags, and LGZD or PLQ development rights). Two communes, Carouge and Confignon, read from a bundled snapshot so the app also works without a network. Every other commune fetches live from SITG on demand.

## Run locally

```
npm install
npm run dev
```

Then open the printed local URL.

## Build

```
npm run build
npm run preview
```

The production build lands in `dist`.

## Deploy to Vercel

Two options.

1. Git based, recommended. Push this folder to the GitHub repo Vercel watches. Vercel auto-detects Vite, runs `npm run build`, and serves `dist`. Each push redeploys.

2. CLI. From the project root, run `vercel --prod`.

If you are updating the existing parcelle-rho project rather than creating a new one, you only need to replace `src/App.jsx` in that repo with the copy here (same export, `export default function App`), commit, and push. Everything else in this package matches a standard Vite setup.

## Verify after deploy

The in-app preview environment has no network, so live behaviour can only be confirmed on the deployed URL. Open the site, choose a commune that is not Carouge or Confignon (for example Lancy, Vernier, or Plan-les-Ouates), zoom in until parcels load, and pin one. The building, dev zone, and PLQ fields should fill from live SITG, and the Surélévation and Planning upside counts in the filter panel should populate for that commune.

## Notes

- Leaflet is loaded at runtime from cdnjs by the component itself, so it is not an npm dependency and there is nothing to configure for it.
- All cadastre, building, surélévation, and development-rights data comes from SITG (Système d'Information du Territoire Genevois). The commune level investment metrics (yields and similar) are modelled and labelled as representative.
