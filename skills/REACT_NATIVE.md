# React Native

## Purpose

Mobile client framework for the Driver Booking Android app.

## Scope

App structure, navigation, state, environment config, and UI patterns.

## Version

React Native **0.86.0** — Android only in Phase 1.

**Application ID:** `com.driverbookingmobile` (`android/app/build.gradle`).

## Key packages

| Package | Version | Use |
| --- | --- | --- |
| `react-native-paper` | 5.15.3 | UI components |
| `@react-navigation/native` + `native-stack` | 7.x | Navigation |
| `@reduxjs/toolkit` + `react-redux` | 2.12 / 9.3 | Client state |
| `@tanstack/react-query` | 5.101 | Server state |
| `axios` | 1.18.1 | HTTP |
| `@react-native-google-signin/google-signin` | 14.x | Google OAuth idToken |
| `@react-native-firebase/app` + `messaging` | 25.1.0 | FCM push — [FIREBASE.md](./FIREBASE.md) |
| `react-native-vector-icons` | 10.3.0 | Icons (`fonts.gradle` in `android/app/build.gradle`) |
| `react-native-dotenv` | 4.x (dev) | `.env` → `@env` imports |

## Structure

```
src/
├── auth/              # RoleSelection, AuthScreen, OtpAuthScreen, googleSignIn.ts
├── customer/          # Customer onboarding, vehicles, booking flows
├── driver/            # Driver onboarding, booking request, trip flows
├── notifications/     # pushRegistration.ts, inbox UI
├── config/env.ts      # API_BASE_URL, GOOGLE_WEB_CLIENT_ID, FCM_SENDER_ID
├── state/
│   ├── flow.tsx       # Auth, booking, notification orchestration
│   └── bookingStatus.ts
├── services/          # api.ts, session.ts
├── hooks/             # e.g. useBookingMessagePolling
├── components/        # ScreenFrame, FormField, buttons, etc.
├── theme/             # Design tokens — UI_GUIDELINES.md
└── types/env.d.ts     # @env module typings
```

Booking UI lives under `customer/` and `driver/` flow screen files — there is no top-level `booking/` folder.

## Environment

Copy `.env.example` → `.env` (gitignored). Loaded via `react-native-dotenv` in `babel.config.js` (disabled in Jest; use `__mocks__/env.js`).

| Variable | Purpose |
| --- | --- |
| `API_BASE_URL` | Backend base URL — physical device: laptop LAN IP; emulator: `http://10.0.2.2:8080` |
| `GOOGLE_WEB_CLIENT_ID` | Web OAuth client ID for native Google Sign-In |
| `FCM_SENDER_ID` | Firebase project sender ID — `replace-me` uses push stub mode |

Read values through `src/config/env.ts` — do not import `@env` outside config/types.

## Navigation

- Auth stack vs main app controlled by auth state ([ADR-0006](../decisions/ADR-0006-mobile-auth-flow-and-phase-1b-identity.md))
- React Navigation native stack
- Flow: Role selection → Auth screen → password / OTP / Google → role home
- Do not `replace` to home from inside auth stack — parent switches on auth state

## Auth (Phase 1 + 1b)

| Method | Mobile entry | Backend |
| --- | --- | --- |
| Password | `AuthScreen.tsx` | `POST /api/v1/auth/login`, `/register` |
| OTP | `OtpAuthScreen.tsx` | `POST /api/v1/auth/otp/request`, `/verify` |
| Google | `googleSignIn.ts` → `AuthScreen` | `POST /api/v1/auth/oauth/google` |

- `configureGoogleSignIn()` runs on app start (`App.tsx`)
- Google requires **Web client ID** in `.env` plus **Android OAuth client** (package + SHA-1) in Google Cloud Console
- OAuth without mobile → `PENDING_VERIFICATION` → mobile OTP (`VERIFY_MOBILE`) before onboarding writes

Detail: [AUTH_FLOW.md](../docs/architecture/AUTH_FLOW.md), [ADR-0007](../decisions/ADR-0007-phase-1b-otp-and-google-oauth.md).

## State

- Redux Toolkit + React Query for server state
- Booking display states mapped from backend — [BOOKING_STATUS_MAPPING.md](../docs/architecture/BOOKING_STATUS_MAPPING.md)
- Business logic in `flow.tsx` / services — screens stay thin
- Push registration runs after successful auth via `registerPushAfterAuth()` in `flow.tsx`

## Commands

```bash
npm start              # Metro
npm run android        # Debug build to emulator/device
npm test               # Jest
npm run lint
```

After `.env` changes: restart Metro with `--reset-cache`.

## Related

- [UI_GUIDELINES.md](../docs/design/UI_GUIDELINES.md)
- [TYPESCRIPT.md](./TYPESCRIPT.md)
- [FIREBASE.md](./FIREBASE.md)
- [JWT.md](./JWT.md)
