```mermaid
sequenceDiagram
    participant User
    participant UI as FocusFlow UI
    participant Timer as Timer Service
    participant DB as Room Database
    participant DS as DataStore
    participant WM as WorkManager
    participant Widget as Home Widget

    Note over User,Widget: ONBOARDING FLOW
    
    User->>UI: Launch app (first time)
    UI->>DS: Check onboarding status
    DS-->>UI: Not completed
    UI->>User: Show onboarding screens
    User->>UI: Enter nickname & role
    UI->>DS: Save user preferences
    DS-->>UI: Confirmation
    UI->>User: Navigate to home screen

    Note over User,Widget: PROJECT CREATION FLOW
    
    User->>UI: Tap "New Project"
    UI->>User: Show project form
    User->>UI: Enter title, description, deadline
    UI->>DB: Insert project
    DB-->>UI: Project ID returned
    
    User->>UI: Add section
    UI->>User: Section form
    User->>UI: Section details
    UI->>DB: Insert section
    
    User->>UI: Add subsection
    UI->>User: Subsection form
    User->>UI: Subsection details
    UI->>DB: Insert subsection
    DB-->>UI: Complete tree structure

    Note over User,Widget: HOME SCREEN & DEADLINE TRACKING
    
    UI->>DB: Query nearest deadline
    DB-->>UI: Deadline + time remaining
    UI->>User: Display countdown
    
    UI->>DB: Calculate project progress
    DB-->>UI: Completion percentage
    UI->>User: Show progress bars
    
    WM->>UI: Periodic refresh (15 min)
    UI->>DB: Re-query deadlines
    UI->>User: Update display
    
    Widget->>WM: Request update
    WM->>DB: Query nearest deadline
    DB-->>WM: Deadline data
    WM->>Widget: Update widget display
    Widget->>User: Show live countdown

    Note over User,Widget: POMODORO FOCUS SESSION
    
    User->>UI: Select section/subsection
    User->>UI: Tap "Start Focus"
    UI->>Timer: Initialize session (25 min)
    Timer->>DB: Create session log (pending)
    Timer->>User: Show foreground notification
    
    loop Every minute
        Timer->>Timer: Update timer countdown
        Timer->>UI: Send tick update
        UI->>User: Update displayed time
    end
    
    alt Session Completed
        Timer->>Timer: Reach 25 minutes
        Timer->>DB: Mark session completed
        Timer->>UI: Session complete signal
        UI->>DB: Update section progress
        UI->>User: Show break suggestion
        User->>UI: Start break
        UI->>Timer: Start break timer (5 min)
        Timer->>User: Break notification
    else User Pauses
        User->>UI: Tap pause
        UI->>Timer: Pause session
        Timer->>DB: Save paused state
        Timer->>User: Paused notification
        User->>UI: Tap resume
        UI->>Timer: Resume countdown
    else User Abandons
        User->>UI: Tap stop
        UI->>Timer: Stop session
        Timer->>DB: Mark session abandoned
        Timer->>User: Session ended notification
    end
    
    alt Break Sessions
        loop After 4 focus sessions
            Timer->>User: Long break (20 min)
        end
    end

    Note over User,Widget: SESSION HISTORY
    
    User->>UI: Navigate to History
    UI->>DB: Query all sessions
    DB-->>UI: Session list with metadata
    UI->>User: Display:
    Note right of UI: - Date & time<br/>- Duration<br/>- Section path<br/>- Completion status
    
    User->>UI: Filter by project
    UI->>DB: Query filtered sessions
    DB-->>UI: Project-specific sessions
    UI->>User: Show filtered history

    Note over User,Widget: DEADLINE MANAGEMENT
    
    User->>UI: View deadlines
    UI->>DB: Query all deadlines
    DB-->>UI: Sorted deadlines
    UI->>User: Color-coded urgency list
    
    User->>UI: Edit deadline
    UI->>User: Date picker
    User->>UI: New date
    UI->>DB: Update deadline
    DB-->>UI: Confirmation
    UI->>User: Updated display
    
    WM->>DB: Check approaching deadlines
    alt Deadline within 24 hours
        DB-->>WM: Urgent deadlines
        WM->>User: Show notification
    end

    Note over User,Widget: DATA PERSISTENCE
    
    Note over UI,DB: All operations are offline
    Note over UI,DB: No network calls made
    Note over UI,DB: No cloud sync
    
    User->>UI: Close app
    UI->>DB: Final flush (if needed)
    DB-->>UI: All data saved locally
    
    User->>UI: Reopen app
    UI->>DB: Load all data
    DB-->>UI: Complete state restored