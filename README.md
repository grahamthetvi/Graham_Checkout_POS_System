# Graham Checkout

A browser-based Point of Sale system built as a single HTML file. Designed for iPadOS Safari with VoiceOver screen reader support, USB barcode/RFID scanner input, and camera-based scanning.

## Features

- **Barcode scanning** via USB scanner (keyboard emulator) or device camera
- **Automatic product lookup** against OpenFoodFacts, OpenBeautyFacts, and OpenProductsFacts APIs
- **Deterministic pricing algorithm** generates consistent prices from product category, brand, and barcode seed
- **Manual product entry** fallback when a barcode isn't found in any API
- **Gift card payments** via USB RFID reader, or QR code scanned with the device camera
- **QR code generation** for gift cards in the admin panel
- **localStorage persistence** for inventory and gift card balances
- **Screen reader optimized** with semantic HTML, ARIA live regions, and native `<dialog>` focus trapping

## Deployment

This is a single `index.html` file with no build step. Serve it from any static host.

**GitHub Pages:**

1. Push this repo to GitHub
2. Go to Settings > Pages
3. Set Source to your main branch, root `/`
4. Access at `https://<username>.github.io/Graham_Checkout/`

## Usage

### Getting Started

1. Open the app in a browser (Safari on iPad recommended)
2. Tap **Admin** in the top-right corner
3. Tap **Seed Test Data** to load sample gift cards ($50 each) and inventory items

### Scanning Products

- **USB scanner:** Scan any barcode. The app detects rapid keystroke input automatically.
- **Camera:** Tap **Scan with Camera** to open the viewfinder. Point at a barcode.
- If the product is in local inventory, it's added to the cart immediately.
- If not, the app queries three product APIs. Found products get a generated price and are saved locally.
- If nothing is found, a manual entry form appears.

### Checkout

1. Tap **Charge $X.XX** when the cart has items
2. The payment dialog offers two options:
   - **Tap RFID Card** — scan a gift card with the USB RFID reader
   - **Scan QR Code** — use the camera to scan a gift card QR code
3. On successful payment, the balance is deducted and the cart clears

### Admin Panel

- **Seed Test Data** creates three gift cards (IDs: `A1B2C3D4`, `E5F6G7H8`, `I9J0K1L2`) with $50 balances and three sample inventory items
- **Generate QR** creates a scannable QR code for any gift card, encoding its hex ID

## Tech Stack

- Vanilla HTML, CSS, JavaScript (no framework)
- [html5-qrcode](https://github.com/mebjas/html5-qrcode) (CDN) — camera barcode/QR scanning
- [qrcode.js](https://github.com/davidshimjs/qrcodejs) (CDN) — QR code image generation
- [Open Food Facts API](https://world.openfoodfacts.org/) — product data

## Hardware

Designed for an iPad with:
- USB barcode scanner (keyboard emulator mode)
- USB RFID reader (keyboard emulator mode)
- Built-in camera (for barcode/QR scanning)

The scanner interceptor detects rapid sequential keystrokes (6+ characters within 80ms per keystroke) followed by Enter, distinguishing hardware input from normal typing.
