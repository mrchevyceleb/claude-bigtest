# Comprehensive Frontend UI/UX Testing

Perform complete UI/UX testing (NOT functionality testing) of an entire website or application using Playwright MCP. This focuses on visual appearance, user experience, layout, responsiveness, and interaction patterns - NOT business logic or data processing.

## Instructions

You are a meticulous QA engineer. Your job is to thoroughly test every aspect of the frontend UI/UX and document all issues found. **Monitor console logs throughout ALL testing phases.**

---

## Phase 0: Pre-Test Assessment (REQUIRED FIRST STEP)

**Before testing anything**, create a comprehensive assessment of every user action possible in the app:

### 0.1 Document All User Actions

Create a checklist listing EVERY action a user could take:

- Navigation Actions (click logo, nav items, footer links, breadcrumbs)
- Page-Specific Actions (list actions per page)
- Form Actions (fill fields, submit, reset)
- Interactive Element Actions (modals, accordions, toggles, dropdowns, tooltips)
- Authentication Actions (login, logout, password reset)

### 0.2 Present Assessment to User

Output the complete user action checklist and confirm before testing.

---

## Phase 1: Setup & Discovery

1. **Get Target URL**: If no URL was provided, ask the user for it
2. **Check Authentication**: Ask if login credentials are needed
3. **Navigate to App**: Use playwright to open the root URL
4. **Take Baseline Screenshot**: Capture initial state
5. **Check Console Logs**: Immediately after page load
6. **Map the Application**: Get DOM structure, identify pages/routes

---

## Phase 2: Authentication (if required)

1. Navigate to login page
2. **Check console logs** before interacting
3. Enter credentials and submit
4. **Check console logs** after submission
5. Verify successful authentication

---

## Phase 3: Desktop Testing (1280px viewport)

**CHECK CONSOLE LOGS AFTER EVERY ACTION.**

- Navigation Testing (visit pages, verify loads, screenshot, check console)
- Button Testing (click all, verify feedback, check console)
- Form Testing (UI/UX only - styling, tab order, placeholders, validation styling)
- Link Testing (internal/external, check console)
- Modal/Dialog Testing (open/close, styling, escape key, check console)
- Dropdown/Select Testing (open, select, verify visual update)
- Input Interaction Testing (focus/blur states, cursor behavior)

---

## Phase 4: Mobile Testing (375px viewport)

Repeat Phase 3 tests plus:
- Verify responsive layouts
- Test hamburger/mobile navigation
- Check touch-target sizes (min 44px)
- Verify no horizontal scrolling
- **Check console logs after each action**

---

## Phase 5: Quality Checks

- Console Error Audit (comprehensive logging)
- Accessibility Quick Audit (alt text, focus states, contrast, keyboard nav)
- Performance Notes (slow pages, laggy interactions)

---

## Phase 6: Generate Detailed Report

Include: Pre-Test Assessment Summary, Executive Summary, Critical/Major/Minor Issues, Console Errors Log, Accessibility Issues, Performance Observations, User Action Test Coverage

---

## Phase 7: Auto-Create Fix Plan

1. Create plan file with issues organized by priority
2. Use EnterPlanMode tool
3. Present fix plan for user approval

---

## Important Notes

- **This is UI/UX testing only** - do NOT test business logic, data validation, or API functionality
- **Monitor console logs after EVERY action** - critical for catching hidden errors
- Take screenshots liberally
- Always complete the Pre-Test Assessment before starting actual testing
