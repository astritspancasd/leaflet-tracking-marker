# react-leaflet-tracking-marker [![MIT License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=plastic)](http://opensource.org/licenses/MIT) [![npm version](https://img.shields.io/npm/v/react-leaflet-tracking-marker.svg?style=plastic)](https://www.npmjs.com/package/react-leaflet-tracking-marker) [![npm version](https://img.shields.io/npm/dw/react-leaflet-tracking-marker.svg?style=plastic&color=important)](https://www.npmjs.com/package/react-leaflet-tracking-marker)

> ✈ A React Leaflet library that allows developers to create custom markers that drifts to a certain point, computes their bearing angle using given coordinates and rotates accordingly.

##### Supports `react-leaflet` v3.x

!["IMG"](./src/demo/planeDemo.gif 'example')

> This library was inspired from [leaflet-drift-marker](https://github.com/hugobarragon/leaflet-drift-marker#drift_marker-with-leaflet) and [react-leaflet-rotatedmarker](https://github.com/verdie-g/react-leaflet-rotatedmarker).

## Installation

```bash
npm install --save react-leaflet-tracking-marker
```

`react-leaflet-tracking-marker` requires `leaflet` and `react-leaflet` as [`peerDependency`](https://docs.npmjs.com/files/package.json#peerdependencies)

```bash
npm install --save leaflet react-leaflet
```

## Usage

Inherits props from `leaflet-drift-marker` and still supports all existing props from [react-leaflet marker](https://react-leaflet.js.org/docs/api-components/#marker)

| Props              | Type               | Default    | Description                                                                                                                 |
| ------------------ | ------------------ | ---------- | --------------------------------------------------------------------------------------------------------------------------- |
| `position`         | `LatLngExpression` |            | The current coordinates. This is mandatory.|
| `previousPosition` | `LatLngExpression` |            | The previous point coordinates, **Allows the marker to automatically computes its rotation angle.** This is mandatory.|
| `rotationOrigin`   | `String`           | `'center'` | The rotation center, as a [`transform-origin`](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-origin) CSS rule. |
| `duration`         | `number`           |            | Required, duration in milliseconds marker will take to destination point                                                    |
| `keepAtCenter`     | `boolean`          | `false`    | Makes map view follow marker                                                                                                |

#### Example

```js
import LeafletTrackingMarker from 'react-leaflet-tracking-marker'

function AirplaneMarker({ data }) {
  const { latitude, longitude } = data
  const [prevPos, setPrevPos] = useState([latitude, longitude])

  useEffect(() => {
    if (prevPos[1] !== longitude && prevPos[0] !== latitude) setPrevPos([latitude, longitude])
  }, [latitude, longitude, prevPos])

  return <LeafletTrackingMarker icon={icon} position={[latitude, longitude]} previousPosition={prevPos} duration={1000} />
}
```

# License

MIT License
