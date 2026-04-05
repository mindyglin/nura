# Product Requirements Document
## Nura: The Beautiful Accountability System

---

## 1. Executive Summary

**Product Name:** Nura  
**Tagline:** *"Your life, in motion."*

Nura is a beautiful accountability system for personal wellness. It helps users rebuild momentum through gentle structure, visual progress, and emotionally resonant feedback. Instead of generic streak circles or clinical dashboards, Nura turns progress into an evolving ritual built around energizing drink avatars, guided plans, and clear encouragement.

The current product is a responsive web app with cloud-backed accounts, a four-pillar wellness system, guided starter planning, visible decay and recovery mechanics, encouragement callouts, customizable activities, and account authentication powered by email.

---

## 2. Product Positioning

Nura is not a medical app, not a productivity punishment tool, and not a noisy wellness feed. It is a **beautiful accountability system** for people who want to:

- notice where they feel depleted
- start again without shame
- receive a realistic plan for the week ahead
- see their effort reflected in something visual and alive
- stay consistent through gentle nudges instead of pressure

**Core insight:** people often know what would help them feel better, but they struggle to follow through consistently. Nura makes follow-through feel elegant, visible, and worth returning to.

---

## 3. Audience

### Primary User
**Burned-Out Achiever**
- 25-40 years old
- Knowledge worker or high-responsibility professional
- Feels disconnected from hobbies, vitality, and self-trust
- Wants structure, but rejects harsh or ugly habit trackers
- Responds to emotionally intelligent, aesthetically strong products

### Secondary User
**Accountability Seeker**
- Wants a low-friction system that helps them keep promises to themselves
- Benefits from visible progress, warm reminders, and a sense of ritual

---

## 4. Product Promise

Nura should help users feel:
- supported, not judged
- gently nudged, not nagged
- visually rewarded, not merely measured
- capable of recovery, not punished for inconsistency

The product promise is:
- Help me identify what feels off.
- Help me choose one realistic next step.
- Show me that consistency changes something real.
- Make returning feel natural, even after I drift.

---

## 5. Core Experience

### 5.1 Four Wellness Pillars
Nura organizes progress across four pillars:

- **Physical**
- **Mental**
- **Intellectual**
- **Creative**

Each activity belongs to one pillar in the current implementation. Users can create custom activities, assign them to a pillar, and set their own XP values.

### 5.2 Guided Transformation Plan on Day 0
Onboarding should identify where the user feels depleted and immediately generate a realistic 7-day starter plan.

**Current Day 0 requirements**
- Ask where the user feels most depleted
- Allow multiple depleted pillars to be selected
- Generate a 7-day starter plan with suggested daily focus
- Show the exact visual unlock language tied to the week
- Make the first week feel achievable, not overwhelming

**Starter plan output should include**
- one recommended focus each day
- a minimum viable win
- a stretch suggestion
- a clear visual reward description such as brighter energy, stronger presence, richer color, or softer glow

### 5.3 Encouragement and Accountability
When users enter the tracker, Nura should immediately show a top-level encouragement callout.

**Requirements**
- appears near the top of the dashboard
- recognizes what the user has already done today
- nudges them toward a pillar they have not completed yet
- adapts to current momentum and starter-plan context
- uses warm, non-judgmental language

### 5.4 Visible Progress, Decay, and Recovery
Nura should make consistency visible and lapses honest without feeling punishing.

**Current visual accountability model**
- logging activity improves glow and progression state
- inactivity introduces subtle decay
- one missed day should feel gentle
- multiple missed days should show a more noticeable slump
- progress is never fully erased
- one new win should visibly start recovery

### 5.5 Environment Evolution and Milestones
The dashboard experience should evolve with progress.

**Current system direction**
- low momentum: quieter, softer environment state
- moderate momentum: warmer, more energized environment state
- strong momentum: vibrant, radiant environment state
- milestones should surface as celebration cards or unlock moments

### 5.6 Cosmetic and Visual Unlocks
Unlocks should reinforce consistency.

**Examples**
- richer color and energy states
- environmental polish and atmosphere shifts
- milestone celebration messaging
- additional visual styling around the user’s selected drink avatar

---

## 6. Avatar Direction

### 6.1 Avatar Philosophy
Nura no longer uses a human avatar as the primary representation.

The product now uses **drink-based avatars that symbolize energy, ritual, and momentum**.

This keeps the product visually clean, more universal, and easier to stylize while still making progress feel personal.

### 6.2 Current Avatar Set
Users can currently choose among energizing drink avatars, including:
- matcha
- coffee
- tea
- bubble tea
- water

### 6.3 Water Cup Requirement
A water cup must be available as a selectable avatar option.

### 6.4 Avatar Flexibility
Users can change their drink avatar at any time from inside the app.

### 6.5 Visual Behavior
Drink avatars should reflect progress through fill, glow, atmosphere, and surrounding visual cues.

**Current implementation principles**
- cup state should feel elegant and premium
- water should feel clean, clear, and grounded
- changing the cup should be immediate and lightweight
- the avatar should read clearly at mobile size

---

## 7. Activity System

### 7.1 Activity Library
Nura ships with starter activities across all four pillars.

### 7.2 Custom Activities
Users can:
- create new activities
- name them themselves
- assign a pillar
- assign XP values
- edit or remove them later

### 7.3 Logging Rules
Users may only log:
- today’s date
- historical dates

Users may not log future dates.

**Requirement**
- future-date logging must be blocked in both UI behavior and state validation
- the error message should clearly explain that only today or past dates are allowed

---

## 8. Authentication and Accounts

### 8.1 Current Authentication Model
Nura uses Supabase-backed authentication and cloud storage.

The current supported sign-in paths are:
- email magic link
- email + password
- password reset by email

### 8.2 Account Model
Each account is identified by email address.

The app stores:
- email address for authentication
- auth provider metadata
- wellness profile data
- logs, streaks, XP, unlocks, and related saved product state

### 8.3 Magic Link
Magic link remains supported as a low-friction sign-in option.

**Important note**
Magic link depends on email sending limits and should be treated as a convenience path, not the only path.

### 8.4 Password Login
Password login should be the most reliable repeat-login path.

**Requirements**
- new users can create an account with email + password
- returning users can sign in with email + password
- password length should be at least 8 characters in the product flow

### 8.5 Existing Magic-Link Users
If a user first created their account through magic link, they may already exist without ever having chosen a password.

**Requirement**
- after signing in, the user should be able to set a password from inside the app
- this should not require creating a second account

### 8.6 Password Reset
Users must be able to reset their password.

**Requirements**
- a `Forgot password?` action appears on the password login screen
- Nura sends a password reset email through Supabase
- the reset link should return the user to Nura
- when the user returns from the reset link, Nura should present a `Reset your password` flow directly

### 8.7 Session Behavior
Nura should keep returning users signed in when possible.

**Requirements**
- session recovery should happen on app boot
- callback URLs must be handled explicitly
- sign-out should return the user cleanly to the auth screen
- the app should not get stranded on a loading screen during auth transitions

### 8.8 Email Field Privacy / Fresh Entry
When users open the site, the email field should not be prefilled with a prior user’s address.

**Requirement**
- login fields must open blank for visitors
- saved email values should be cleared on sign-out

---

## 9. Legal and Consent Requirements

The auth screen must include:
- Privacy Policy access
- Terms access
- basic consent copy explaining what data is stored and why

### 9.1 Privacy Copy Requirements
Users should be informed that Nura may store:
- their email for account access
- authentication metadata from the auth provider
- wellness profile and log data needed for cross-device use

### 9.2 Terms Requirements
Users should understand:
- Nura is not medical or emergency care
- use is self-guided
- access depends on supporting infrastructure such as auth and storage providers

### 9.3 Consent Requirements
The app should explain, in plain language, that by continuing the user allows:
- secure sign-in processing
- password or email-based authentication
- storage of profile and wellness data needed to use the app across devices

---

## 10. Notifications and Nudges

### 10.1 In-App Notification Callout
The dashboard should include a warm callout that acts like a notification in-product.

It should:
- congratulate progress already made
- identify missing pillars for the day
- guide the next best action
- remain emotionally supportive

### 10.2 Tone
Nura’s notification language should feel:
- warm
- confident
- non-shaming
- elegant

Examples:
- "You already showed up today. One more gentle win would round this out beautifully."
- "Creative is still quiet today. A small act of expression is enough."
- "You have been carrying a lot. Let’s keep today light and real."

---

## 11. Technical Architecture

### 11.1 Platform
**Current phase:** Web app with responsive design and GitHub Pages deployment support.

### 11.2 Frontend
- React in a single HTML deployment artifact
- Tailwind-style utility classes for styling
- lightweight SVG/CSS-based drink avatar rendering

### 11.3 Backend / Auth / Storage
- Supabase Auth
- Supabase database
- cloud-backed user state

### 11.4 Hosting
- static deployment compatible with GitHub Pages
- auth callbacks configured through Supabase URL configuration

### 11.5 Current Data Model (Simplified)

```text
User
- id
- email
- created_at
- auth metadata

Profile Data (stored as JSON)
- user name
- selected drink avatar
- onboarding selections
- starter plan
- activities
- logs
- streaks
- XP
- glow score
- avatar state
- achievements
- current app view data
```

### 11.6 Persistence Notes
The current web app persists state per signed-in user through Supabase.

Key stored categories include:
- profile state
- activities
- log history
- streaks and unlocks
- avatar and environment state

---

## 12. UX Flows

### 12.1 Onboarding
1. User lands on Nura auth screen.
2. User signs in with password or magic link.
3. If no profile exists yet, onboarding begins.
4. User selects where they feel depleted.
5. User chooses a drink avatar.
6. Nura generates a 7-day starter plan.
7. User enters the dashboard with a personalized first-week path.

### 12.2 Returning User Flow
1. User opens Nura.
2. Existing session is restored when possible.
3. Dashboard opens with encouragement, current progress, and next best action.

### 12.3 Magic-Link-First User Upgrades to Password
1. User signs in with magic link.
2. User opens `Set password` inside the app.
3. User saves a password.
4. Next login can use email + password.

### 12.4 Password Reset Flow
1. User chooses `Forgot password?`
2. Nura sends reset email.
3. User clicks reset link.
4. Nura opens reset-password mode on return.
5. User saves a new password.
6. User signs in again with the updated password.

### 12.5 Logging Flow
1. User chooses an activity.
2. User selects a valid date.
3. If the date is in the future, logging is blocked.
4. User receives XP, progress updates, and any applicable milestone feedback.

---

## 13. Success Metrics

### North Star Metric
**Weekly active users who complete at least 4 activities across at least 2 pillars**

### Supporting Metrics
- D1 retention
- D7 retention
- D30 retention
- average activities logged per week
- weekly pillar balance
- percentage of users completing onboarding
- percentage of users setting a password after initial auth
- password reset completion rate
- sign-in success rate

---

## 14. Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Magic-link rate limits disrupt onboarding | High | High | Provide password login, password reset, and custom SMTP |
| Auth callback failures strand the user | Medium | High | Explicit session recovery and loading-state fallback |
| Users misunderstand account state after magic-link signup | Medium | Medium | Clear copy explaining existing account vs. password setup |
| Future-date logging undermines trust | Medium | Medium | Enforce validation in UI and reducer |
| Data privacy concerns | Medium | High | Clear consent, privacy policy, minimal collection framing |
| Encouragement feels naggy | Medium | Medium | Keep tone warm, specific, and non-judgmental |

---

## 15. Roadmap Alignment

### Current Implemented Foundation
- cloud-backed user accounts
- password and magic-link login
- password reset flow
- privacy, terms, and consent copy
- drink avatar selection
- water avatar option
- change-cup control
- guided starter plan
- encouragement callout
- visible decay and milestone cards
- future-date logging guard

### Next High-Value Enhancements
- custom SMTP for production email delivery
- richer drink-avatar animations and unlock states
- push or scheduled notifications
- deeper stats and weekly review
- social accountability features
- native mobile packaging or PWA hardening

---

## 16. Document Info

**Version:** 2.0  
**Product:** Nura  
**Last Updated:** April 2026  
**Status:** Consolidated with current HTML implementation

---

*The goal of Nura is not perfect performance. It is helping people return to themselves, one visible win at a time.*
