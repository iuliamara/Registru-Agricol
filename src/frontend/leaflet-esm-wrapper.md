# Leaflet ESM Wrapper

> **Current implementation note (25 November 2026):** the wrapper and typing/alias files are present, but active `ParcelaMapComponent` and `OsmMapComponent` still import directly from `leaflet`. `angular.json` permits Leaflet CommonJS output. The conversion guidance below records the original rationale and intended usage; it is not evidence that every map import was converted. Current maps use Leaflet/OpenStreetMap and JSONB GeoJSON persistence. See [GIS implementation](../../Docs/Applications/Public-Institutions-Portal.md#gis-and-maps). The complete pre-expansion version is preserved in the historical collection.

## Ce am adăugat

1. Un wrapper ESM pentru Leaflet:
   - `src/app/shared/utils/leaflet-esm.ts`
   - Acest fișier re-exportă tot din `leaflet/dist/leaflet-src.esm.js` și oferă un export default.

2. Configurație TypeScript:
   - `tsconfig.app.json`
   - Am adăugat `baseUrl` și `paths` pentru aliasul `@utils/leaflet-esm`.

3. Configurație Angular build:
   - `angular.json`
   - Am permis `leaflet` ca dependență CommonJS prin `allowedCommonJsDependencies`.

## De ce s-a făcut această schimbare

Leaflet este un pachet care poate produce un bailout de optimizare în build-ul Angular atunci când este importat direct ca CommonJS.

Folosind `leaflet/dist/leaflet-src.esm.js` printr-un wrapper ESM, compilatorul poate folosi o versiune modernă de modul și reduce avertismentele de optimizare.

## Cum se folosește

În loc de:

```ts
import * as L from 'leaflet';
```

sau:

```ts
import { map, tileLayer } from 'leaflet';
```

folosește:

```ts
import * as L from '@utils/leaflet-esm';
```

sau:

```ts
import { map, tileLayer, marker } from '@utils/leaflet-esm';
```

sau:

```ts
import Leaflet from '@utils/leaflet-esm';
```

## Observații

- Dacă un fișier Angular importă `leaflet` direct, trebuie modificat să importe din `@utils/leaflet-esm`.
- Wrapperul se bazează pe `leaflet/dist/leaflet-src.esm.js`, care este versiunea ESM oferită de pachet.
- `allowedCommonJsDependencies` rămâne util pentru a evita blocarea build-ului în cazul în care alte părți ale proiectului folosesc încă `leaflet` din CommonJS.
