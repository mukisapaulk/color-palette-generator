# Retro Color Palette Generator

**Retro Color Palette Generator** is a free online tool for creating vibrant, nostalgic color palettes for web design, graphic design, and creative projects. The app blends a 1990s-inspired beige, pixelated interface with helpful modern functionality: generate palettes, edit colors, export/save, and toggle views — all presented with scanlines and subtle glitch animations for a playful retro vibe.

> **Note:** This project produces clearly labeled sample palettes and UI assets. It is **not** intended to replicate or impersonate any official documents.

---

## Features

* **Random Palette Generation**
  Generate five-color palettes (hex codes and color names) via TheColorAPI. Trigger generation with the **spacebar** or the floating action button (FAB).

* **Retro Aesthetic**
  Beige gradients, pixelated borders, scanline overlays, and subtle glitch animations inspired by CRT displays and early desktop UIs.

* **Edit Colors**
  Edit individual color swatches using a retro-styled modal. Enter custom hex codes (e.g., `#FF5733`) and fetch real-time color names from TheColorAPI.

* **Grid / List View Toggle**
  Mobile- and desktop-optimized display modes for palette browsing.

* **Export & Save**
  Export palettes as JSON files or save them to local storage for later retrieval.

* **SEO & Accessibility**
  SEO-optimized HTML metadata and accessible controls (ARIA labels and alt text) for better discoverability and inclusivity.

* **Monetization-Ready**
  Layout includes strategic ad placements (top banner and sidebar) that are designed not to interfere with UX.

* **Playful Retro Modals**
  Feedback modals (copy, save, export, error) styled to match the retro aesthetic with light backdrops and subtle blur.

* **Responsive Design**
  Viewport-constrained layouts tested for mobile (375px) and desktop (1024px) to avoid unnecessary scrolling.

---

## Installation

### Prerequisites

* Node.js v16 or higher
* npm v8 or higher
* (Optional) Vue CLI for local development

### Steps

```bash
# Clone the repository
git clone https://github.com/yourusername/retro-color-palette-generator.git
cd retro-color-palette-generator

# Install dependencies
npm install

# Ensure required libraries are installed (example)
npm install axios
# Tailwind CSS should be configured as part of the project setup
```

### Run Locally

```bash
npm run dev
# Then open http://localhost:5173 in your browser
```

### Build for Production

```bash
npm run build
# Deploy the generated `dist/` folder to Vercel, Netlify, or similar
```

---

## Usage

* **Generate a palette:** Press the **spacebar** or click the FAB (bottom-right) to create a new five-color palette with hex codes and names.
* **Edit a color:** Click **Edit** on a color strip, enter a hex code in the modal, and submit to update the swatch and its name.
* **Copy hex codes:** Click **Copy** on any hex code — a retro modal will confirm the action.
* **Toggle view:** Use the toolbar button to switch between grid and list displays.
* **Export / Save:** Export palettes to JSON or save them to local storage using the toolbar options.
* **Camera / Image color extraction:** A planned future feature; currently shows a placeholder modal.

---

## Project Structure

```
retro-color-palette-generator/
├── public/
│   ├── index.html          # SEO-optimized entry point
│   └── favicon.ico
├── src/
│   ├── components/
│   │   ├── Palette.vue     # Color palette display and edit modal
│   │   └── Modal.vue       # Retro feedback modal
│   ├── App.vue             # Main layout with toolbar, FAB, and ads
│   ├── main.js             # Vue app entry
│   └── assets/
├── tailwind.config.js      # Tailwind CSS configuration
├── package.json
└── README.md
```

---

## SEO & Accessibility

* **Metadata:** Add descriptive `<title>` and `<meta>` tags targeting keywords such as *color palette generator*, *retro color scheme maker*, *hex color tool*, etc.
* **Content:** Include targeted keywords in headings and instructional copy to improve indexing.
* **ARIA & Alt:** Use ARIA labels (e.g., `"Generate new color palette for design"`) and descriptive `alt` attributes for icons and images.
* **Clean URLs:** Host the app at a discoverable path like `/color-palette-generator` for better indexing.

---

## Design Notes

* Visual identity is intentionally retro: beige tones, pixelated borders, and a pixel font (e.g., *Press Start 2P*) are ideal for authenticity.
* Use scanline overlays and subtle glitch animations for nostalgia without reducing usability.
* Keep primary controls (generate, export, edit) accessible and keyboard-friendly.

---

## Contributing

Contributions are welcome!

1. Fork the repo.
2. Create a feature branch:
   `git checkout -b feature/YourFeature`
3. Commit your changes:
   `git commit -m "Add YourFeature"`
4. Push to your branch and open a pull request.

Please follow the retro aesthetic for new features and include tests where appropriate.

---

## Future Enhancements

* Add a **Lock** button to pin colors in a palette.
* Implement **Load Saved Palette** UI from local storage.
* Integrate **image-based color extraction** (camera / upload).
* Provide a downloadable layered source (Figma / PSD) and a custom pixel font option.

---

## License

MIT License — see the `LICENSE` file for details.

---

## Contact

For support or feedback, email: `mukisapaul480@gmail.com`
Or open an issue on the project's GitHub repository.

---

Built with love for retro design and modern functionality — generate your perfect color palette today!
