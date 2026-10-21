# small reviewer notes

## Architecture

This is a minimal Vite + React single-page starter application. `src/main.jsx` bootstraps `App` under `StrictMode` and imports the global stylesheet; `App.jsx` composes the page from focused components and data-driven feature cards. Static content is separated into `src/data/features.js`, while visual sections live under `src/components/`.

## Conventions

- Use function components with default exports, as in `src/components/Brand.jsx`, `FeatureCard.jsx`, and `HeroArt.jsx`.
- Keep component files focused on one visual responsibility; `App.jsx` composes `Brand`, `HeroArt`, and `FeatureCard` rather than embedding their markup.
- Store repeatable/static collections in `src/data`; `App.jsx` renders `features` from `src/data/features.js` with a stable `key={feature.number}`.
- Pass feature fields through explicit component props and object spread: `FeatureCard` accepts `{ number, title, description }`, and callers use `<FeatureCard key={feature.number} {...feature} />`.
- Use `.jsx` for React components and `.js` for plain data modules. Relative imports include the file extension, e.g. `./components/Brand.jsx` and `./data/features.js`.
- Keep transient UI state local. The button state in `src/App.jsx` uses `useState(false)` and updates only the button label after activation.
- Preserve semantic HTML and accessibility attributes: `main`, `nav`, `section`, `article`, `footer`, `aria-label`, and `aria-hidden` are used throughout `src/App.jsx` and `src/components/HeroArt.jsx`.
- External links opened in a new tab must include `rel="noreferrer"`; see the React documentation link in `src/App.jsx`.
- The app is mounted through `createRoot` and wrapped in `StrictMode` in `src/main.jsx`; retain this entry-point pattern.
- Vite configuration stays minimal and uses `defineConfig` with the React plugin in `vite.config.js`.

## Watch out for

- Do not replace stable list keys with array indexes; feature cards currently use the data-level `number` field.
- Avoid moving static feature content into JSX when it can remain in `src/data/features.js`.
- Preserve the `aria-hidden="true"` attributes on decorative arrow, dot, and checkmark spans so they are not redundantly announced.
- Be careful when changing the button behavior in `src/App.jsx`: it is intentionally a local, one-way “started” state rather than navigation or form submission.
- Do not remove `rel="noreferrer"` when modifying the external `target="_blank"` link.