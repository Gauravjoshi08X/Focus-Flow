# FocusFlow

**Structured deep work for professionals and students — offline, private, no fluff.**

FocusFlow is an offline-first productivity app that combines project planning with the Pomodoro technique. Instead of being just another countdown timer, it understands the structure of your work: projects, sections, subsections, deadlines, and focus sessions.

No accounts. No analytics. No cloud sync. Your data stays on your device.

## Features

### Fully Offline

* No network permissions
* No accounts or sign-ins
* No analytics or tracking
* Designed with F-Droid compliance in mind

### Pomodoro Focus Sessions

* 25-minute focus sessions
* 5-minute short breaks
* 20-minute long breaks after 4 completed rounds
* Pause and stop controls from notifications
* Sessions continue while the device is locked

### Project-Based Organization

* Create projects with deadlines
* Organize work into sections and subsections
* One-level nesting for a clean mobile experience
* Track progress across entire projects

### Deadline Tracking

* Nearest deadline highlighted on the home screen
* Live countdowns
* Color-coded urgency indicators
* View all deadlines sorted chronologically

### Session History

* Every focus session is logged
* Track where your time is actually spent
* Review completed and abandoned sessions
* Associate focus time with specific project sections

### Home Screen Widget

* Displays the nearest deadline
* Live countdown updates
* Opens directly into the related project
* Background refresh using WorkManager

### Material You Design

* Dynamic Android theming
* Native Android experience
* Clean and distraction-free interface

---

## Why FocusFlow?

Most productivity apps are either:

* Bloated with features you'll never use
* Dependent on cloud services
* Focused on a single workflow
* Filled with ads, analytics, or subscriptions

FocusFlow takes a different approach.

Whether you're building software, writing a thesis, drafting a book, or managing a project, the workflow is fundamentally the same:

1. Break work into manageable pieces
2. Focus on one piece at a time
3. Track progress consistently
4. Meet deadlines

FocusFlow is designed around that principle.

---

## User Flow

### 1. Onboarding

* Quick introduction to the app
* Optional explanation of the workflow
* Set a nickname and role
* One-time setup

### 2. Create a Project

Create a project with:

* Title
* Description
* Deadline

Then add:

* Sections
* Subsections (one level deep)
* Optional descriptions
* Optional deadlines

### 3. Track Upcoming Work

The home screen highlights:

* Nearest deadline
* Remaining time
* Project progress
* Active focus session

### 4. Start a Focus Session

Select any section or subsection and start focusing.

Sessions are automatically linked to the selected work item and recorded in the session history.

---

## Tech Stack

### Flutter

Cross-platform UI framework used for the application layer.

### Android Components

* Room Database — local persistence
* DataStore — user preferences
* WorkManager — scheduled background updates
* Glance API — home screen widget
* Foreground Service — reliable timer execution

### Design

* Material 3
* Material You dynamic color support

---

## Privacy

FocusFlow is built around privacy by default.

* No accounts
* No cloud sync
* No analytics
* No telemetry
* No advertising SDKs
* No Firebase
* No Crashlytics
* No proprietary tracking libraries

All project data, session logs, and settings remain on your device.

---

## F-Droid Compliance

FocusFlow is designed to meet F-Droid requirements.

* No network permission
* No proprietary SDKs
* Reproducible builds
* Public source repository
* Background work handled through WorkManager

---

## Data Model

```text
User
 └── Projects
      └── Sections
           └── Subsections
                └── Sessions
```

### Project Nodes

Each project, section, and subsection contains:

* Title
* Description
* Deadline (optional)
* Completion status
* Creation timestamp

### Session Logs

Each focus session contains:

* Section reference
* Start time
* Duration
* Completion status

---

## Use Cases

### Developers

Break software projects into:

* Features
* Components
* Tasks

Track focus time per area of work.

### Students

Structure:

* Thesis
* Chapters
* Sections

Stay aware of deadlines and study consistently.

### Writers

Organize:

* Books
* Parts
* Chapters

Measure writing effort over time.

### Professionals

Manage:

* Projects
* Deliverables
* Subtasks

Keep everything local and available offline.

---

## Roadmap

* Statistics dashboard
* CSV export of session logs
* Backup and restore
* Additional widget sizes
* Custom Pomodoro durations
* Project archiving

---

## License

This project is licensed under the MIT License.

---

**FocusFlow — Built for focus. Designed for privacy.**
