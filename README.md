# SCUM Map Coordinate Mapper

A precise coordinate mapping system for SCUM game that converts in-game coordinates to pixel positions on a 1080x1080 map image.

## Features

- **High-Precision Calibration**: Uses linear regression (least squares method) with 16 intersection points for maximum accuracy
- **Real-Time Mapping**: Instantly converts SCUM game coordinates to pixel positions on the map
- **Quadrant Detection**: Automatically calculates the 5x5 quadrant (Z0-D4) based on marker position
- **Calibration Mode**: Visual calibration tool with draggable markers at all quadrant intersections
- **X-Axis Inversion**: Automatically handles SCUM's inverted X-axis coordinate system
- **Responsive Design**: Works on desktop and mobile devices
- **No Dependencies**: Pure HTML, CSS, and JavaScript - no external libraries required

## How to Use

1. Open `index.html` in a web browser
2. Paste SCUM coordinates in the format: `{X=-142798.922 Y=-142780.359 Z=39619.605|P=0.000000 Y=0.000000 R=0.000000}`
3. Press Enter or click "Buscar Posição"
4. The red marker will appear at the exact position on the map
5. View the quadrant, pixel coordinates, and game coordinates in the info panel

## Calibration

The system is pre-calibrated using 16 known intersection points:
- Map center: `X=-142798.922, Y=-142780.359` → Pixel (540, 540)
- All 16 quadrant intersections with their precise game coordinates and pixel positions

### Calibration Mode

1. Click "Modo Calibração" to enter calibration mode
2. Drag the markers at quadrant intersections to fine-tune positions
3. Use "Gravar Calibração" to save adjustments to localStorage
4. Use "Gerar Arquivo" to export calibration data as JSON

## Coordinate System

- **Map Size**: 1080x1080 pixels (144 km² in-game)
- **Center Point**: (540, 540) pixels = `X=-142798.922, Y=-142780.359` in-game
- **Quadrants**: 5x5 grid (Z0-Z4, A0-A4, B0-B4, C0-C4, D0-D4)
- **X-Axis**: Inverted (negative X goes right on map)
- **Y-Axis**: Standard (positive Y goes up/north on map)

## Technical Details

### Calibration Method

The system uses **linear regression (least squares)** to calculate scale factors:

```
SCALE_X = Σ(deltaX * deltaPixelX) / Σ(deltaX²)
SCALE_Y = Σ(deltaY * deltaPixelY) / Σ(deltaY²)
```

This method uses all 16 intersection points for maximum precision across the entire map.

### Coordinate Conversion

1. Calculate delta from center: `deltaX = gameX - CENTER_X`, `deltaY = gameY - CENTER_Y`
2. Apply scale: `calculatedX = CENTER_PIXEL_X + (deltaX * SCALE_X)`
3. Apply X-axis inversion: `pixelX = MAP_WIDTH - calculatedX`
4. Clamp to map bounds: `[0, 1080]` for both X and Y

## Files

- `index.html` - Complete application (HTML, CSS, JavaScript)
- `1080x1080.png` - SCUM map image (144 km²)
- `scum-calibration-2025-11-06.json` - Calibration data with all 16 intersection points

## Browser Compatibility

Works on all modern browsers:
- Chrome/Edge (recommended)
- Firefox
- Safari
- Mobile browsers

## License

MIT License - See LICENSE file for details

## Author

PauloPedreiro

## Repository

https://github.com/PauloPedreiro/Scum-maps-Index

