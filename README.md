# Meds Tracker - A Medication Management and Caregiver Monitoring App

A mobile application designed to help users organize their medications, manage medication schedules, receive reminders, track doses, and share medication adherence information with approved caregivers or trusted contacts.

The application extends a traditional medication tracker by introducing an invitation-based caregiver monitoring system and emergency contact functionality.

**Important:** This application does not collect, store, or manage hospital records, hospital medical histories, or information from hospital databases. Medication information is entered and managed by the user.

---

## 1. Key Features

### 📋 Medication Management

- Add, edit, and archive medications with name, dosage, form, and custom icons.
- Track current medication supply with visual progress bars and low-supply alerts.
- Support common medication forms, including tablets, capsules, liquids, and injections.
- Support PRN (as-needed) medications without a fixed schedule.

### 💊 Drug Database and Interactions

- Search the RxNorm drug database with autocomplete.
- Automatically fill medication names and generic names from search results.
- Provide warnings about potential interactions between medications.

### ⏰ Smart Scheduling

- Flexible scheduling options: daily, specific days, or custom intervals.
- Multiple medication times per day.
- Start and end dates for medications with limited durations.
- Configurable snooze durations.
- Add a medication and schedule it in one flow or schedule it later.

### 🔔 Push Notifications and Reminders

- Configurable notifications for each medication schedule.
- Snooze actions directly from notifications.
- Medication reminder notifications.
- Missed-dose catch-up reminders.
- Low-supply reminders.
- Restore scheduled reminders when the application launches.

### ✅ Dose Tracking

- One-tap dose logging.
- Mark medications as taken or skipped.
- Undo accidental dose entries.
- Calendar view showing daily medication adherence.
- Track medication history and adherence.

Dose statuses:

- **Taken:** The user has recorded the medication as taken.
- **Skipped:** The user has recorded the medication as skipped.
- **Unconfirmed:** No dose record has been submitted for the scheduled medication.

An unconfirmed dose should not automatically be treated as a skipped dose.

### 📊 Reports and Analytics

- Weekly and monthly medication adherence charts.
- Consecutive-day adherence streaks.
- Per-medication missed-dose breakdowns.
- Visual reports showing medication adherence levels.

### 🩺 Symptom and Side Effect Tracking

- Record symptoms and side effects.
- Assign severity levels: mild, moderate, or severe.
- Add optional notes.
- Link symptoms to specific medications or record them independently.
- Browse symptom history by date.

### 👤 User Profile and Account

- Secure authentication through Supabase.
- Email/password registration and login.
- Optional Google Sign-In.
- Profile management.
- Medication statistics and adherence summaries.
- Password management.
- Privacy and security settings.
- Data export and account deletion.

### 👨‍👩‍👧 Trusted Contacts and Caregiver Monitoring

This feature extends the existing caregiver-sharing functionality.

Instead of only generating a medication summary for manual sharing, users can establish a connection with a trusted contact who can monitor their medication adherence.

**Trusted contact management**
- Users can add trusted contacts.
- Users can send invitations to contacts.
- Contacts must accept invitations before a monitoring connection is established.
- Users can view invitation and connection statuses.
- Users can remove contacts or revoke their access.

**Caregiver invitation and permissions**
- Invited contacts must accept the invitation.
- The user must grant the required permission before medication information becomes accessible.
- Emergency contact status does not automatically grant access to medication information.
- Users can change or revoke caregiver permissions at any time.

**Caregiver dashboard**
- Approved caregivers can view the medication information shared with them.
- View medication names and schedules, subject to granted permissions.
- View dose statuses: taken, skipped, and unconfirmed.
- View relevant medication adherence updates.
- View adherence summaries where permission is granted.

Caregivers should not be able to edit medication schedules, modify medication records, or make changes to the user's account unless such functionality is explicitly authorized.

### 🚨 Emergency Contact and Assistance

- Users can designate a trusted contact for emergencies.
- Store the contact's name and phone number.
- Provide a quick-call option.
- Provide a quick-message option.
- Open the device's existing phone or messaging application when the user selects an emergency contact action.

Emergency contact functionality is separate from caregiver monitoring permissions.

### ❓ Help and Support

- In-app FAQ.
- Direct email support link.
- Privacy policy information.

### 🧩 Android Home Screen Widget

- Display the next scheduled medication.
- Open the application directly from the widget.
- Automatically update widget information.

### 🔄 Over-the-Air Updates

- Support application updates through Expo Updates.
- Error boundary and crash recovery.

### 📡 Offline Support

- Monitor network connectivity.
- Display an offline indicator.
- Handle temporary loss of internet connectivity.
- Synchronize supported data when connectivity is restored.

### 🌙 Dark Mode

- Light and dark themes.
- Automatic system theme detection.
- Manual theme selection.

---

## 2. Architecture

The application will maintain its existing architecture while introducing additional caregiver-related functionality.

```text
                    Expo Router (Screens)
                            |
       ---------------------------------------------
       |             |             |               |
   User Screens  Medication    Caregiver       Profile &
                 Screens        Screens        Settings
       |             |             |               |
       ---------------------------------------------
                            |
                    TanStack Query
                     (Server State)
                            |
       ---------------------------------------------
       |             |             |               |
  Medications    Schedules     Dose Logs    Caregiver Data
       |             |             |               |
       ---------------------------------------------
                            |
                  Supabase (Postgres)
                     + Row Level
                      Security
                            |
       ---------------------------------------------
       |             |             |               |
    Zustand      AuthContext   ThemeContext   Notifications
```

### Main Architecture Components

- **Expo Router:** Application navigation and screen management.
- **TanStack Query:** Fetching, caching, and updating server data.
- **Supabase:** Authentication, PostgreSQL database, and Row-Level Security.
- **Zustand:** Local form drafts and temporary client state.
- **React Context:** Authentication and theme management.
- **Expo Notifications:** Medication reminders and supported caregiver notifications.

Screens should access server data through reusable TanStack Query hooks rather than calling Supabase directly.

---

## 3. Technology Stack

| Layer | Technology | Purpose |
|---|---|---|
| Framework | Expo SDK | Cross-platform mobile development |
| UI | React Native | Mobile user interface |
| Routing | Expo Router | File-based navigation |
| Language | TypeScript | Type safety |
| Server State | TanStack Query v5 | Data fetching and caching |
| Client State | Zustand v5 | Form and temporary state |
| Authentication | Supabase Auth | User authentication |
| Database | PostgreSQL | Application data storage |
| Database Security | Supabase RLS | Access control |
| Notifications | Expo Notifications | Medication and caregiver notifications |
| Networking | NetInfo | Network monitoring |
| OTA Updates | Expo Updates | Application updates |
| Widgets | react-native-android-widget | Android home screen widget |
| UI Components | React Native custom components | Reusable interface components |

---

## 4. User Experiences

The application will support two main experiences.

### A. Medication User

The medication user can:

- Register and log in.
- Manage their profile.
- Add, edit, and delete medications.
- Create medication schedules.
- Receive medication reminders.
- Record doses as taken or skipped.
- View medication adherence reports.
- Add trusted contacts.
- Send caregiver invitations.
- Grant or revoke caregiver permissions.
- Designate an emergency contact.
- Call or message their emergency contact.

### B. Approved Caregiver

An approved caregiver can:

- Register and log in.
- Receive and respond to caregiver invitations.
- View the medication information shared with them.
- Monitor medication adherence.
- View taken, skipped, and unconfirmed dose statuses.
- View available adherence summaries.
- Receive relevant notifications if enabled and permitted.

Caregivers cannot automatically access a user's information simply because they are listed as an emergency contact.

---

## 5. Proposed Project Structure

The existing Expo Router structure will be extended with additional caregiver-related screens.

```text
medication-tracker/
├── app/
│   ├── _layout.tsx
│   ├── index.tsx
│   │
│   ├── (tabs)/
│   │   ├── index.tsx
│   │   ├── medications.tsx
│   │   ├── reports.tsx
│   │   └── profile.tsx
│   │
│   ├── auth/
│   │   ├── login.tsx
│   │   ├── signup.tsx
│   │   └── profile-setup.tsx
│   │
│   ├── medication/
│   │   ├── add.tsx
│   │   ├── [id].tsx
│   │   ├── edit.tsx
│   │   ├── schedule.tsx
│   │   ├── reminders.tsx
│   │   └── log-prn.tsx
│   │
│   ├── caregiver/
│   │   ├── dashboard.tsx
│   │   ├── invitations.tsx
│   │   ├── invitation-details.tsx
│   │   ├── monitored-user.tsx
│   │   └── permissions.tsx
│   │
│   ├── contacts/
│   │   ├── index.tsx
│   │   ├── add.tsx
│   │   └── emergency.tsx
│   │
│   ├── profile/
│   │   └── edit.tsx
│   │
│   ├── caregiver-sharing.tsx
│   ├── notifications.tsx
│   ├── notification-settings.tsx
│   ├── symptoms.tsx
│   ├── log-symptom.tsx
│   ├── privacy-security.tsx
│   └── help-support.tsx
│
├── components/
│   └── ui/
│
├── hooks/
│   ├── useQueryHooks.ts
│   ├── useCaregiverHooks.ts
│   ├── useContactHooks.ts
│   └── useNetworkStatus.ts
│
├── lib/
│   ├── supabase.ts
│   ├── queryClient.ts
│   ├── queryKeys.ts
│   └── notifications.ts
│
├── stores/
│   └── draftStores.ts
│
├── contexts/
│   ├── AuthContext.tsx
│   └── ThemeContext.tsx
│
├── types/
│   └── database.ts
│
├── utils/
│
├── widgets/
│
└── supabase/
    └── migrations/
```

The structure is a proposed extension. Existing files should be retained where possible rather than duplicated.

---

## 6. Database Design

The existing database uses Supabase PostgreSQL with Row-Level Security.

The current core tables include:

### Existing Tables

| Table | Purpose |
|---|---|
| `profiles` | Stores user profile information. |
| `medications` | Stores medication details. |
| `schedules` | Stores medication schedules. |
| `dose_logs` | Stores recorded medication doses. |
| `symptoms` | Stores user-recorded symptoms and side effects. |

### Proposed New Tables

| Table | Purpose |
|---|---|
| `trusted_contacts` | Stores trusted contact relationships and contact details. |
| `caregiver_invitations` | Tracks invitations, acceptance, and rejection. |
| `caregiver_permissions` | Stores the monitoring permissions granted by users. |
| `caregiver_notifications` | Stores caregiver-related notification records, if notification history is required. |

### Proposed Relationships

- One user can have multiple medications.
- One medication can have multiple schedules.
- One schedule can have multiple dose logs.
- One user can have multiple trusted contacts.
- One user can invite multiple caregivers.
- One caregiver can monitor multiple users if each user independently grants permission.
- Each caregiver connection can have its own permission settings.

### Database Security

- Users can access and manage their own medication information.
- Caregivers can only access information explicitly shared with them.
- Invitations must be accepted before a caregiver connection is activated.
- Monitoring permissions must be granted separately.
- Users can revoke permissions.
- Database Row-Level Security must enforce these restrictions.

No hospital records, hospital patient histories, or hospital database integrations will be included.

---

## 7. Caregiver Monitoring Workflow

1. A user creates an account and logs in.
2. The user adds their medications and schedules.
3. The user opens the trusted contacts section.
4. The user adds a contact and sends an invitation.
5. The invited contact receives the invitation.
6. The contact accepts or declines.
7. The user grants the appropriate medication monitoring permissions.
8. The caregiver can now access the information shared with them.
9. When the user records a dose, the caregiver dashboard can reflect the updated status.
10. The user can revoke access whenever necessary.

### Dose Monitoring

| Dose status | Meaning |
|---|---|
| Taken | User recorded the dose as taken. |
| Skipped | User recorded the dose as skipped. |
| Unconfirmed | No dose record exists for the scheduled dose. |

---

## 8. Emergency Contact Workflow

1. The user opens the emergency contact section.
2. The user adds or selects a trusted contact.
3. The contact's name and phone number are saved.
4. The user can select the call or message option.
5. The device opens its phone or messaging application.

Emergency contact access does not automatically provide caregiver monitoring permissions.

---

## 9. Notifications

The existing notification system will be extended where necessary.

### Medication User Notifications

- Scheduled medication reminders.
- Snoozed medication reminders.
- Low medication supply alerts.
- Invitation acceptance notifications.
- Caregiver permission or access updates.

### Caregiver Notifications

Subject to the user's notification preferences:

- New caregiver invitation.
- Medication marked as skipped.
- Scheduled dose remains unconfirmed after an agreed period.
- Relevant medication adherence updates.

Notifications should not imply that a medication was physically taken or missed when the system only knows whether the user recorded a dose.

---

## 10. Security and Privacy

Security is important because the application handles personal medication information.

The application should:

- Use Supabase authentication.
- Protect user information through Row-Level Security.
- Restrict caregiver access to explicitly shared information.
- Require invitation acceptance.
- Require separate monitoring permission.
- Allow users to revoke access.
- Avoid exposing medication information to unauthorized users.
- Store only information necessary for the application's functionality.

Emergency contact details and caregiver monitoring permissions should be managed separately.

---

## 11. Getting Started

### Prerequisites

- Node.js 18 or later.
- Bun package manager.
- Expo CLI.
- Visual Studio Code.
- Expo Go or an Expo development build.
- Supabase project.
- Android device or emulator.

### Installation

Clone the repository:

```bash
git clone <repository-url>
cd medication-tracker
```

Install dependencies:

```bash
bun install
```

Create a `.env` file:

```env
EXPO_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
EXPO_PUBLIC_SUPABASE_KEY=your-anon-public-key
```

Configure Supabase and run the required database migrations.

Start the application:

```bash
bun run start
```

For a development build:

```bash
bun run prebuild
bun run android
```

---

## 12. Development Priorities

The development work can be organized into the following stages:

| Stage | Tasks |
|---|---|
| 1. Existing application | Review and understand the existing medication tracker. |
| 2. Authentication | Confirm registration, login, and profile functionality. |
| 3. Medication management | Confirm medication CRUD, scheduling, reminders, and dose tracking. |
| 4. Trusted contacts | Implement contact management and invitations. |
| 5. Caregiver permissions | Implement invitation acceptance, authorization, and access revocation. |
| 6. Caregiver dashboard | Implement shared medication and adherence monitoring. |
| 7. Emergency contact | Implement calling and messaging options. |
| 8. Notifications | Extend notifications for caregiver-related events. |
| 9. Testing | Test functionality, permissions, security, and usability. |

---

## 13. Project Scope

### In Scope

- User authentication and profile management.
- Medication management.
- Medication scheduling.
- Medication reminders.
- Dose tracking.
- Medication adherence reports.
- Trusted contact management.
- Caregiver invitations.
- Caregiver permission management.
- Caregiver medication monitoring.
- Emergency calling and messaging.

### Out of Scope

- Hospital record management.
- Hospital database integration.
- Patient medical history management.
- Doctor appointment booking.
- Medical diagnosis.
- Prescription issuance.
- Automated treatment recommendations.
- Direct communication with hospital information systems.

---

## 14. Important Design Considerations

1. A caregiver must accept an invitation before a monitoring connection is established.
2. A user must grant monitoring permission before medication information is shared.
3. Emergency contact status must remain separate from caregiver monitoring access.
4. Users must be able to revoke caregiver access.
5. An unconfirmed dose must not automatically be classified as skipped.
6. Caregivers should have read-only access to shared medication information unless additional permissions are deliberately introduced.
7. The application must not present itself as a hospital records system or a replacement for professional medical care.

---

## Built With

- [Expo](https://expo.dev/)
- [React Native](https://reactnative.dev/)
- [Expo Router](https://docs.expo.dev/router/introduction/)
- [Supabase](https://supabase.com/)
- [TanStack Query](https://tanstack.com/query)
- [Zustand](https://zustand-demo.pmnd.rs/)
- [Expo Notifications](https://docs.expo.dev/versions/latest/sdk/notifications/)
- [TypeScript](https://www.typescriptlang.org/)

