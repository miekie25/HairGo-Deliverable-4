# HairGo — Deliverable 4

HairGo is a native Android application for booking hair salon and barbershop appointments. Clients can discover salons, browse services, book appointments, and communicate with salon owners. Salon owners can manage their salon profiles, services, and bookings, while administrators can moderate users, salons, and reports.

HairGo is developed as a final-year group project using Android and Firebase technologies.

## Features

### Client Features

- Register using phone OTP and log in using email and password.
- Reset passwords through email.
- Search salons by name or location.
- View salon profiles, photos, services, prices, and ratings.
- Book one or more services using available appointment slots.
- View upcoming and past bookings, reschedule appointments, and cancel bookings.
- Complete the mock payment workflow for a booking.
- View booking details and payment-related information.
- Message salon owners through booking-linked conversations.
- Leave reviews for completed bookings.
- Report salon-related issues or application problems.
- Track or edit reports while they are pending.
- View notification history and scheduled appointment reminders.
- Edit their profile, enable dark mode, and delete their account.

### Salon Owner Features

- Register and create one or more salon profiles.
- View incoming bookings and confirm, decline, or mark bookings as completed.
- View booking details, including the client's phone number and appointment notes.
- View dashboard summaries for pending, confirmed, completed, and today's bookings.
- Manage salon services, prices, operating hours, and salon photos.
- Switch between salons associated with their account.
- Message clients through booking-linked conversations.
- View booking and payment-related information where implemented.

### Administrator Features

- Access dashboard tabs for Overview, Users, Salons, and Reports.
- Open reports and update their status.
- Message users through the administrative messaging feature.

**Current limitation:** The administrator interface is still being connected to Firebase. Some dashboard lists use sample data, while the report detail screen reads and writes real data.

## Technology Stack

- Native Android development using Java and Kotlin.
- XML layouts, ViewBinding, and Material 3.
- Firebase Authentication, including email/password and phone OTP.
- Cloud Firestore for application data.
- Firebase Cloud Messaging infrastructure.
- WorkManager for appointment reminders.
- Minimum Android SDK: 26.
- Compile and target SDK: 36.
- Android Gradle Plugin: 8.12.3.
- Kotlin: 2.4.0.
- Project Java target: JDK 11; use JDK 17 or newer for the development environment.

## Mock Payment System

HairGo includes a mock payment system to demonstrate the booking payment workflow.

- Allows users to interact with the simulated payment process.
- Supports payment-related information and statuses as implemented in the application.
- Demonstrates how payment fits into the appointment booking experience.

**Important:** The payment system is for demonstration purposes. It does not process real financial transactions through a live payment gateway.

## Source Code

The compressed source-code package is available in this repository:

`HairGo-Deliverable4-source.zip`

The ZIP contains the committed project source at the time it was packaged.

## Demonstration Video

The demonstration video shows HairGo in action and presents the implemented client and salon-owner workflows.

**Video link:** [Insert the direct link to the completed demonstration video]

## Screenshots and User Stories

Screenshots of the running application and brief user stories will accompany the Deliverable 4 submission PDF. They will demonstrate key features and explain how clients, salon owners, and administrators interact with HairGo.

## Getting Started

1. Install a recent version of Android Studio.
2. Download and extract the source-code ZIP.
3. Open the extracted project folder in Android Studio.
4. Allow Gradle to synchronise the project.
5. Configure Firebase as described below, if required.
6. Connect an Android device or configure an emulator running Android 8.0 (API 26) or later.
7. Run the application from Android Studio.

## Firebase Configuration

HairGo uses Firebase Authentication and Cloud Firestore. The Android Firebase configuration file is located at `app/google-services.json`.

To use a different Firebase project, configure Firebase for the package name `com.hairgo.app` and provide the corresponding configuration file.

### Firestore Collections

The application's main collections include:

- `users` — user profiles, roles, contact details, account status, and device tokens.
- `salons` — salon profiles, owner IDs, services, ratings, operating hours, and deletion status.
- `bookings` — appointment details, clients, salons, selected services, appointment times, booking statuses, notes, and payment-related fields.
- `reviews` — ratings and comments associated with completed bookings.
- `reports` — application or salon reports and their status.
- `messages` — administrative messages sent to users.
- `conversations` — booking-linked client and owner conversations, including participant information, last-message previews, and unread indicators. Individual chat messages are stored in a subcollection.
- `salonPhotos` — salon photos stored as encoded JPEG images.
- `slotLocks` — records used to claim appointment slots and help prevent conflicting bookings.

The project uses soft deletion for applicable records, marking them as deleted rather than permanently removing them. Firestore security rules restrict hard deletion.

### Security Rules and Indexes

Firestore security rules are maintained in `firestore.rules`. They must be published to the appropriate Firebase project.

A composite index is required for a booking query using `salonID`, `isDeleted`, and `dateTime` in ascending order.

Phone OTP testing uses South African `+27` phone-number formatting. Firebase test phone numbers can be configured in the Authentication console.

### Test Accounts

Demo credentials are not included in the repository. Client and salon-owner accounts can be registered through the application.

There is no administrator registration screen. Administrator access is configured through the Firebase user record for the relevant test account.

## System Design

HairGo uses a layered structure:

1. **Presentation layer:** Android activities and fragments display screens and handle user interactions.
2. **Application and Firebase manager layer:** Manager classes coordinate operations and return results through callbacks.
3. **Backend layer:** Firebase Authentication and Cloud Firestore provide authentication and data storage.

Live screens use Firestore snapshot listeners where implemented, allowing updates to appear without manually refreshing the screen.

### Main Data Relationships

- One salon owner can manage multiple salons.
- A client can create multiple bookings.
- Each booking is associated with a salon.
- A completed booking can have a review.
- A booking has a linked chat conversation and may be associated with a report.
- Booking documents store client and salon names for display in booking lists.

## Known Limitations

- Payments use a mock system; live payment gateway integration has not been implemented.
- The administrator dashboard is not fully connected to Firebase; some lists still display sample data.
- Push notifications require a configured message-sending service. Storing device tokens alone does not send notifications.
- Some features may require additional Firebase configuration before they can be used in another environment.

## Project Team

HairGo is developed collaboratively as a final-year group project.

## Deliverable 4 Submission

This repository contains the HairGo source-code ZIP and supporting documentation for Deliverable 4. The demonstration video, screenshots, user stories, and references are included or linked as part of the final submission materials.
