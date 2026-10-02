# H2S Guard 🛡️

Prototype industrial safety monitoring for passive colorimetric H2S dosimeter wristbands.

H2S Guard connects a worker scan to exposure analysis, saved readings, alerts, supervisor monitoring, and admin telemetry. It is designed for demonstration and workflow validation; it is not a certified laboratory or occupational exposure instrument.

## What It Includes ✨

- Worker home, exposure history, alerts, and profile views.
- Deterministic demo scanning for Normal, Attention, High Exposure, and Invalid Reading scenarios.
- Separate Demo and Live scanner modes.
- Live camera capture and image upload analysis.
- Employee QR lookup and profile inspection.
- Exposure results with dose, confidence, duration, timestamp, optical color data, and calibration metadata.
- Local browser persistence for readings, alerts, workers, notifications, role, theme, and audit records.
- Supervisor monitoring and escalation workflows.
- Admin sections for overview, workers, dosimeters, readings, incidents, analytics, reports, batches, calibration, audit logs, alert rules, and settings.
- Responsive navigation and persisted light/dark theme support.
- Lucide React icons for the web interface.

## Demo Workflow 🔄

```text
Worker
  -> Select Scan Dosimeter
  -> Choose Demo or Live mode
  -> Analyze the dosimeter
  -> Review exposure result
  -> Save reading
  -> Review History and Alerts
  -> Switch to Supervisor monitoring
  -> Inspect Admin readings and reports
```

### Deterministic Demo Scan 🎯

1. 🚀 Start the web app and open **Scan Dosimeter**.
2. 🎛️ Keep the scanner in **Demo** mode.
3. 🔴 Select **High Exposure**.
4. 📷 Press the capture button.
5. ✅ Confirm the result is **HIGH EXPOSURE** and `42.8 ppm·h`.
6. 💾 Save the reading.
7. 🚨 Open Alerts and confirm the matching critical alert.
8. 📋 Open History and confirm the new reading.
9. 👷 Switch to Supervisor and Admin views to inspect the same reading.

Demo mode uses the selected preset even when a webcam is available. A camera frame cannot overwrite a selected demo result.

### Live Camera Mode 📸

Live mode analyzes a camera frame or uploaded image. Camera access generally requires HTTPS and browser permission. If the image cannot be analyzed reliably, the application returns `INVALID` instead of silently falling back to `NORMAL`.

## Technology 🧰

- React 19
- TypeScript
- Vite
- Tailwind CSS v4
- Lucide React
- Expo Router and React Native
- jsPDF and AutoTable
- Browser localStorage for prototype persistence

## Requirements 📦

- Node.js 20 or newer recommended
- npm
- Modern web browser
- HTTPS and camera permission for live camera scanning in deployed environments

## Install and Run ▶️

Install dependencies:

```bash
npm install
```

Start the web application:

```bash
npm run dev
```

Open the local URL printed by Vite. The default URL is usually `http://localhost:5173`.

## Validation Commands ✅

Production build:

```bash
npm run build
```

Lint:

```bash
npm run lint
```

Preview the production build:

```bash
npm run preview
```

The project currently reports existing lint warnings for unused imports and React refresh guidance. The TypeScript and Vite production build should complete successfully.

## Prototype Calibration 🧪

The colorimetric calculation is prototype/mock logic. It must not be treated as a regulatory limit, laboratory result, certification, or accuracy claim.

The current implementation uses:

```text
dose = 0.85 * deltaE^1.15
NORMAL: dose < 25
ATTENTION: dose <= 40
HIGH_EXPOSURE: dose > 40
```

Invalid optical readings are stored separately and do not produce a quantitative dose.

## Data and Reset ♻️

The web prototype persists data in browser localStorage. The stored data includes readings, alerts, workers, notifications, selected role, theme preference, and audit records.

Use **Reset Demo Environment** in the demo controls to restore the initial prototype data.

This repository does not include a production backend, multi-user synchronization, hosted authentication, or regulatory compliance certification service.

## Project Structure 🗂️

```text
app/                         Expo Router mobile screens
public/                      Static assets
src/components/common/      Shared buttons, cards, modals, badges, and states
src/components/layout/      Header, sidebar, navigation, footer, and FAB
src/components/scanner/     Camera and dosimeter scanner
src/components/views/       Worker, history, alerts, profile, and dashboard views
src/components/admin/       Supervisor and admin sections
src/context/                Shared application state and actions
src/data/                   Prototype workers, readings, alerts, and admin data
src/services/               Browser persistence service
src/types/                  Shared TypeScript models
src/utils/                  Color analysis, PDF, and cryptographic helpers
```

## Application Identity 🏷️

- Product name: **H2S Guard**
- Expo display name: `H2S Guard`
- Expo slug: `h2s-guard`
- Android and iOS bundle identifier: `com.h2sguard.app`
- GitHub repository: https://github.com/byteStealthX/H2S-Guard
