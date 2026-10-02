# H2S Guard

H2S Guard is a prototype industrial safety monitoring application for passive colorimetric H2S dosimeter wristbands. It provides worker scanning, exposure analysis, reading history, alerts, supervisor monitoring, administration screens, reports, and local demo data persistence.

The product name is **H2S Guard**. The GitHub repository uses the name `H2S-Guard` or `H2S-Guard-1` when a second repository is required because GitHub repository names cannot contain spaces.

## Product Flow

```text
Worker
  -> Dosimeter scan
  -> Color or demo analysis
  -> Exposure status
  -> Save reading
  -> History and alerts
  -> Supervisor monitoring
  -> Admin readings, workers, batches, reports, and settings
```

## Features

- Worker home, exposure history, alerts, and profile views.
- Deterministic demo scan presets: Normal, Attention, High Exposure, and Invalid Reading.
- Explicit Demo and Live scanner modes.
- Live camera capture and image upload analysis.
- QR-based employee lookup and profile viewing.
- Exposure result cards with dose, confidence, duration, timestamp, color shift, and calibration details.
- Local reading persistence using browser storage.
- Automatic alert creation for high exposure and attention readings.
- Supervisor monitoring dashboard and escalation views.
- Admin overview, workers, dosimeters, readings, incidents, analytics, reports, batches, calibration, audit logs, alert engine, and settings sections.
- Light and dark themes with persisted theme preference.
- Responsive web layout with mobile navigation.
- Lucide React icons throughout the web interface.

## Technology

- React 19 and TypeScript
- Vite and Tailwind CSS v4
- Lucide React
- Expo Router and React Native screens
- jsPDF and AutoTable for prototype report generation
- Browser localStorage for prototype persistence

## Requirements

- Node.js 20 or newer recommended.
- npm.
- A modern browser for the web application.
- Camera access and HTTPS for live camera capture in deployed environments. Demo mode works without a camera.

## Install

```bash
npm install
```

## Run the Web App

```bash
npm run dev
```

Open the local URL printed by Vite, normally `http://localhost:5173`.

## Build and Lint

```bash
npm run build
npm run lint
```

The lint configuration reports existing unused-import and React refresh warnings. The production TypeScript and Vite build must complete successfully.

## Demo Validation Flow

1. Open the app in Worker view.
2. Select **Scan Dosimeter**.
3. Keep **Demo** mode selected.
4. Select **High Exposure**.
5. Press the capture button.
6. Confirm the result is **HIGH EXPOSURE** with the selected preset dose.
7. Save the reading.
8. Open Alerts and confirm the matching critical alert.
9. Open History and confirm the new reading.
10. Switch to Supervisor and confirm the live reading in monitoring.
11. Switch to Admin and inspect Overview and Readings.
12. Toggle dark mode and verify headings and controls remain readable.

### Demo and Live Modes

Demo mode always uses the selected deterministic preset. A webcam frame cannot overwrite a demo result.

Live mode uses the camera or uploaded image for color analysis. If a usable image cannot be analyzed, the result is explicitly `INVALID` rather than silently becoming `NORMAL`.

## Prototype Calibration Logic

The colorimetric calculation is prototype/mock calibration logic. It must not be interpreted as laboratory certification, occupational exposure certification, or regulatory compliance certification.

The current prototype uses:

```text
dose = 0.85 * deltaE^1.15
NORMAL: dose < 25
ATTENTION: dose <= 40
HIGH_EXPOSURE: dose > 40
```

Invalid optical readings are represented separately and do not produce a quantitative dose.

## Project Structure

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

## Data and Reset

The prototype stores readings, alerts, workers, notifications, role, theme, and audit data in browser localStorage. Use **Reset Demo Environment** in the demo controls to restore the initial prototype state.

This project does not include a production backend, multi-user synchronization, or a regulatory compliance certification service.

## Repository

The existing repository is:

```text
https://github.com/Kart01-dev/H2S-Guard
```

The Expo application metadata is defined in `app.json` with display name `H2S Guard`, slug `h2s-guard`, and package identifier `com.h2sguard.app`.
