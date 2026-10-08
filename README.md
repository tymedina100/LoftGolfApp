# Loft Golf Studios — Booking App

A Swift iOS booking app and Node.js calendar-sync service developed as a team senior capstone for Loft Golf Studios (August 2025–May 2026).

This repository is Tyler Medina's fork of [hoangnamapu/LoftGolfApp](https://github.com/hoangnamapu/LoftGolfApp). The upstream team and contributor history are retained. Tyler's later paid contract work (June–July 2026) focused on debugging booking, cancellation, and calendar-synchronization issues; this fork is not a claim of sole authorship.

## Project layout

- `LoftGolfApp/`: iOS application, authentication, views/view models, and uSchedule integration.
- `LoftGolfAppTests/` and `LoftGolfAppUITests/`: Swift unit and UI test targets.
- `services/calendar-sync/`: Node.js service for booking-to-calendar synchronization, bay routing, polling, and reminders.
- `docs/`: [calendar-sync architecture](docs/calendar-sync-architecture.md) and [integration test plan](docs/calendar-sync-test-plan.md).

The application uses SwiftUI, Firebase, and the uSchedule API. Calendar synchronization uses Express, Google Calendar, and Firestore. The architecture document describes intended flows; use the source and recorded validation to establish which flows work in a given deployment.

## iOS setup

1. Use macOS with Xcode and an iOS 18.2+ simulator or device, matching the project deployment target.
2. Open `LoftGolfApp.xcodeproj` and allow Xcode to resolve Swift package dependencies.
3. Use studio-authorized Firebase/uSchedule configuration and signing settings for the intended test environment. Keep private configuration out of commits.
4. Select the `LoftGolfApp` scheme and run on the chosen simulator/device.

Run the unit and UI test targets from Xcode's **Product → Test** menu. Tests that depend on studio services need an authorized test environment. Simulator success alone does not verify bookings or synchronization against live systems.

## Calendar-sync setup

```bash
cd services/calendar-sync
npm install
```

Supply configuration through the process environment or the hosting platform's secret settings. Required settings in `src/config.js` include `SYNC_API_KEY`, `BAY1_CALENDAR_ID`, `USCHEDULE_IMPERSONATE_EMAIL`, and `USCHEDULE_PASSWORD`. The service also needs authorized Google credentials for Calendar and Firestore. `BAY2_CALENDAR_ID` enables the second bay; `TIME_ZONE` defaults to `America/Phoenix`.

With approved test configuration in place, `npm start` runs the service. Startup may begin polling and reminders, so use the [integration test plan](docs/calendar-sync-test-plan.md) with the studio's test accounts before connecting to live calendars.

## Validation and repository hygiene

The Swift tests and integration plan are included for review. A fresh native build and live-service validation have not been completed as part of this repository-presentation cleanup.

Generated Xcode output and macOS metadata are excluded from the proposed source tree. Existing ignore rules prevent new build artifacts from being committed; the cleanup commit removes previously tracked artifacts without rewriting history. Original source, project configuration, and upstream attribution are preserved.

No new license is introduced by this fork; retain the upstream project's applicable terms and third-party dependency licenses.
