---
description: Comprehensive Frontend UI/UX Testing (NOT functionality). First creates an assessment listing every user action in the app, then systematically tests all actions at desktop (1280px) and mobile (375px) viewports while monitoring console logs. Generates detailed QA report and auto-creates fix plan for approval.
argument-hint: [url]
allowed-tools: Read, Write, Edit, Bash(*), Grep, Glob
---

# /bigtest - Comprehensive Application Testing

You are executing the `/bigtest` command. This command performs a **complete audit** of an entire web application, testing:

1. **UI/UX** - Visual appearance, layout, responsiveness, interaction patterns
2. **Functionality** - Forms work, data flows correctly, features behave as expected
3. **Console Errors** - JavaScript errors, warnings, failed requests
4. **Network** - API calls succeed, no 404s, no failed requests
5. **User Flows** - Complete user journeys work end-to-end

## CRITICAL: This Tests EVERYTHING

Unlike `/perfect` (which tests a single task), `/bigtest` audits the **entire application**. You must test:
- Every page
- Every button
- Every form (including submission and validation)
- Every link
- Every interactive element
- Every user flow
- At BOTH desktop AND mobile viewports

---

## Phase 0: Pre-Test Assessment (REQUIRED FIRST STEP)

**Before testing anything**, create a comprehensive map of the entire application:

### 0.1 Application Discovery

Navigate through the app and document:

```
APPLICATION MAP
===============

Pages/Routes Discovered:
- / (Home)
- /about
- /contact
- /dashboard
- [list all pages]

Navigation Elements:
- Header nav: [items]
- Footer nav: [items]
- Sidebar nav: [items if applicable]
- Breadcrumbs: [yes/no]

Forms Found:
- Login form (page: /login)
- Contact form (page: /contact)
- [list all forms with their pages]

Interactive Elements:
- Modals: [list]
- Dropdowns: [list]
- Accordions: [list]
- Tabs: [list]
- Carousels: [list]
- Toggles/Switches: [list]

User Flows Identified:
- Authentication flow (login -> dashboard)
- Contact submission flow
- [list key user journeys]
```

### 0.2 Create Test Checklist

Generate a comprehensive checklist of EVERY testable action:

```
TEST CHECKLIST
==============

NAVIGATION (X items)
[ ] Click logo -> returns to home
[ ] Click "About" nav item -> loads /about
[ ] Click "Contact" nav item -> loads /contact
[list every nav action]

FORMS (X items)
[ ] Login form - valid credentials -> success
[ ] Login form - invalid credentials -> error message
[ ] Login form - empty submission -> validation
[ ] Contact form - valid submission -> success
[ ] Contact form - invalid email -> validation error
[list every form scenario]

BUTTONS (X items)
[ ] "Submit" button on contact form -> submits
[ ] "Cancel" button on modal -> closes modal
[list every button]

INTERACTIVE ELEMENTS (X items)
[ ] Open user dropdown -> shows menu
[ ] Close modal with X button -> closes
[ ] Close modal with Escape key -> closes
[ ] Close modal clicking outside -> closes
[list every interaction]

USER FLOWS (X items)
[ ] Complete login flow
[ ] Complete contact submission flow
[list every flow]
```

### 0.3 Present Assessment to User

Output the complete Application Map and Test Checklist. Ask:
> "I've identified [X] pages, [Y] forms, and [Z] total test actions. Ready to begin comprehensive testing?"

Wait for confirmation before proceeding.

---

## Phase 1: Setup

### 1.1 Get Target URL
- If URL provided in arguments: use it
- If no URL: ask user for the target URL

### 1.2 Check Authentication Requirements
Ask: "Does this app require authentication? If yes, provide credentials."

### 1.3 Initial Navigation
1. Navigate to the root URL
2. Take baseline screenshot
3. Check console for errors on initial load
4. Check network for failed requests

### 1.4 Record Baseline Metrics
```
BASELINE METRICS
================
Initial Load:
- Console errors: [count]
- Network errors: [count]
- Page load time: [if observable]
```

---

## Phase 2: Authentication Testing (if required)

If credentials were provided:

### 2.1 Login Flow Testing
1. Navigate to login page
2. Screenshot the login form
3. Test empty submission -> expect validation errors
4. Test invalid credentials -> expect error message
5. Test valid credentials -> expect successful login
6. Check console after each action
7. Verify redirect to authenticated area

### 2.2 Session Testing
1. Verify user appears logged in (name displayed, etc.)
2. Test accessing protected routes
3. Test logout functionality
4. Verify redirect after logout

---

## Phase 3: Desktop Testing (1280x720 viewport)

Set viewport to **1280x720** before starting.

**For EVERY action, follow this protocol:**
1. Take screenshot before action
2. Perform the action
3. Check console for new errors
4. Check network for failed requests
5. Verify expected result occurred
6. Take screenshot after action
7. Record pass/fail with details

### 3.1 Navigation Testing

Test every navigation element:

| Test | Expected Result | Pass/Fail |
|------|-----------------|-----------|
| Click logo | Returns to home | |
| Click nav item 1 | Loads correct page | |
| Click nav item 2 | Loads correct page | |
| [continue for all nav items] | | |

### 3.2 Page Content Testing

For each page, verify:
- [ ] Page loads without error
- [ ] All text is readable (no overflow, no truncation)
- [ ] All images load (no broken images)
- [ ] Layout matches expected design
- [ ] No horizontal scrolling
- [ ] Console has no errors

### 3.3 Form Testing (UI + Functionality)

For each form, test:

**UI/UX Checks:**
- [ ] Form layout is correct
- [ ] Labels are associated with inputs
- [ ] Placeholder text is helpful
- [ ] Tab order is logical
- [ ] Focus states are visible
- [ ] Error states are styled correctly
- [ ] Success states are styled correctly

**Functionality Checks:**
- [ ] Empty submission shows validation errors
- [ ] Invalid data shows appropriate errors
- [ ] Valid submission succeeds
- [ ] Success message/redirect occurs
- [ ] Data is actually saved (if verifiable)
- [ ] Console has no errors during submission
- [ ] Network requests succeed

### 3.4 Button Testing

For each button:
- [ ] Button is clickable
- [ ] Hover state works
- [ ] Click triggers expected action
- [ ] Loading state appears (if applicable)
- [ ] Success/error feedback shown
- [ ] Console has no errors

### 3.5 Interactive Element Testing

**Modals/Dialogs:**
- [ ] Opens correctly
- [ ] Content displays properly
- [ ] Close button (X) works
- [ ] Escape key closes modal
- [ ] Click outside closes modal (if expected)
- [ ] Form inside modal works (if applicable)

**Dropdowns:**
- [ ] Opens on click
- [ ] Options display correctly
- [ ] Selection updates correctly
- [ ] Closes after selection
- [ ] Closes when clicking outside

**Accordions:**
- [ ] Expand/collapse works
- [ ] Content displays correctly
- [ ] Animation is smooth (if applicable)

**Tabs:**
- [ ] Tab switching works
- [ ] Content updates correctly
- [ ] Active tab is highlighted

**Carousels/Sliders:**
- [ ] Navigation arrows work
- [ ] Dots/indicators work
- [ ] Auto-play works (if applicable)
- [ ] Touch/swipe works (test in mobile phase)

### 3.6 Link Testing

For each link:
- [ ] Internal links navigate correctly
- [ ] External links open in new tab (if expected)
- [ ] No broken links (404s)
- [ ] Console has no errors

### 3.7 User Flow Testing

Test complete user journeys:

**Example: Contact Form Flow**
1. Navigate to contact page
2. Fill out form with valid data
3. Submit form
4. Verify success message
5. Verify data was sent (check network)
6. Check console for errors throughout

**Record each flow:**
```
FLOW: [Flow Name]
Steps completed: [X/Y]
Console errors: [count]
Network errors: [count]
Result: PASS / FAIL
Notes: [any issues]
```

---

## Phase 4: Mobile Testing (375x667 viewport)

Set viewport to **375x667** before starting.

Repeat ALL Phase 3 tests, plus:

### 4.1 Mobile-Specific Checks

- [ ] Hamburger menu appears
- [ ] Mobile nav opens/closes correctly
- [ ] Touch targets are adequate (min 44x44px)
- [ ] No horizontal scrolling on any page
- [ ] Text is readable without zooming
- [ ] Forms are usable on mobile
- [ ] Modals fit on screen
- [ ] Buttons are tappable

### 4.2 Responsive Layout Checks

For each page:
- [ ] Layout adapts correctly
- [ ] Images scale appropriately
- [ ] Text doesn't overflow
- [ ] No overlapping elements
- [ ] Spacing is appropriate

---

## Phase 5: Console & Network Audit

### 5.1 Console Error Summary

Compile all console errors found during testing:

```
CONSOLE ERROR LOG
=================

Error 1:
- Message: [error message]
- Page: [where it occurred]
- Action: [what triggered it]
- Severity: Critical / Major / Minor

Error 2:
[continue for all errors]

TOTAL: [X] console errors
- Critical: [count]
- Major: [count]
- Minor: [count]
```

### 5.2 Network Error Summary

```
NETWORK ERROR LOG
=================

Failed Request 1:
- URL: [endpoint]
- Status: [404/500/etc]
- Page: [where it occurred]
- Action: [what triggered it]

TOTAL: [X] network errors
```

---

## Phase 6: Calculate Score

**Scoring Rubric (100 points total):**

| Category | Max Points | Criteria |
|----------|------------|----------|
| UI/Visual | 20 | Layout correct, no visual bugs, responsive works |
| Functionality | 30 | All features work, forms submit, data flows correctly |
| Console Errors | 20 | No JS errors (deduct 4 per error, min 0) |
| Network Errors | 15 | No failed requests (deduct 5 per error, min 0) |
| User Flows | 15 | Complete user journeys work end-to-end |

### 6.1 UI/Visual Score (20 points)

Start at 20, deduct for issues:

| Issue Type | Deduction |
|------------|-----------|
| Major layout break | -4 |
| Missing/broken image | -3 |
| Text overflow/truncation | -2 |
| Alignment issue | -1 |
| Mobile layout break | -3 |
| Horizontal scroll | -3 |

### 6.2 Functionality Score (30 points)

Start at 30, deduct for issues:

| Issue Type | Deduction |
|------------|-----------|
| Form submission fails | -6 |
| Button does nothing | -4 |
| Feature completely broken | -6 |
| Feature partially broken | -3 |
| Data not saving | -5 |
| Redirect not working | -2 |

### 6.3 Console Errors Score (20 points)

```
consoleScore = max(0, 20 - (errorCount * 4))
```

| Errors | Points |
|--------|--------|
| 0 | 20 |
| 1 | 16 |
| 2 | 12 |
| 3 | 8 |
| 4 | 4 |
| 5+ | 0 |

### 6.4 Network Errors Score (15 points)

```
networkScore = max(0, 15 - (errorCount * 5))
```

| Errors | Points |
|--------|--------|
| 0 | 15 |
| 1 | 10 |
| 2 | 5 |
| 3+ | 0 |

### 6.5 User Flows Score (15 points)

Start at 15, deduct based on flow completion:

| Issue | Deduction |
|-------|-----------|
| Critical flow completely broken | -5 |
| Critical flow partially broken | -3 |
| Secondary flow broken | -2 |

### 6.6 Calculate Total

```
totalScore = uiScore + functionalityScore + consoleScore + networkScore + flowScore
```

### 6.7 Score Interpretation

| Score Range | Status | Meaning |
|-------------|--------|---------|
| **95-100** | EXCELLENT | Production ready, minor polish at most |
| **85-94** | GOOD | Solid, a few issues to address |
| **70-84** | FAIR | Usable but needs work |
| **50-69** | POOR | Significant issues, not ready for users |
| **Below 50** | CRITICAL | Major problems, needs substantial fixes |

---

## Phase 7: Generate Report

Output this comprehensive report:

```
===============================================================================
                         /BIGTEST COMPREHENSIVE REPORT
===============================================================================

APPLICATION: [URL]
TEST DATE: [date]
FINAL SCORE: [X]/100 - [STATUS]

-------------------------------------------------------------------------------
                              TEST COVERAGE
-------------------------------------------------------------------------------

Pages Tested: [X]
Forms Tested: [X]
Buttons Tested: [X]
Interactive Elements: [X]
User Flows Tested: [X]
Total Test Actions: [X]

Viewports Tested:
- Desktop (1280x720): COMPLETE
- Mobile (375x667): COMPLETE

-------------------------------------------------------------------------------
                              SCORE BREAKDOWN
-------------------------------------------------------------------------------

UI/Visual:       [X]/20   [brief summary]
Functionality:   [X]/30   [brief summary]
Console Errors:  [X]/20   [X] errors found
Network Errors:  [X]/15   [X] errors found
User Flows:      [X]/15   [X/Y] flows working

-------------------------------------------------------------------------------
                              CRITICAL ISSUES
-------------------------------------------------------------------------------

Issues that MUST be fixed before release:

1. [CRITICAL] [Issue title]
   - Location: [page/component]
   - Description: [what's broken]
   - Steps to reproduce: [how to see it]
   - Expected: [what should happen]
   - Actual: [what happens]
   - Console error: [if applicable]
   - Viewport: Desktop / Mobile / Both

[Continue for all critical issues]

-------------------------------------------------------------------------------
                              MAJOR ISSUES
-------------------------------------------------------------------------------

Issues that significantly impact user experience:

1. [MAJOR] [Issue title]
   - Location: [page/component]
   - Description: [the problem]
   - Viewport: Desktop / Mobile / Both

[Continue for all major issues]

-------------------------------------------------------------------------------
                              MINOR ISSUES
-------------------------------------------------------------------------------

Polish items and small improvements:

1. [MINOR] [Issue description]
2. [MINOR] [Issue description]

-------------------------------------------------------------------------------
                              CONSOLE ERROR LOG
-------------------------------------------------------------------------------

[List all console errors with context]

-------------------------------------------------------------------------------
                              NETWORK ERROR LOG
-------------------------------------------------------------------------------

[List all failed requests with context]

-------------------------------------------------------------------------------
                              USER FLOW RESULTS
-------------------------------------------------------------------------------

| Flow | Steps | Result | Notes |
|------|-------|--------|-------|
| Login | 5/5 | PASS | |
| Contact Form | 4/5 | FAIL | Submit fails |
| [continue] | | | |

-------------------------------------------------------------------------------
                              RECOMMENDATIONS
-------------------------------------------------------------------------------

Priority order for fixes:
1. [Most critical fix]
2. [Second priority]
3. [Third priority]
[continue]

===============================================================================
```

---

## Phase 8: Create Fix Plan

After generating the report:

1. Create a prioritized fix list based on findings
2. Use the `EnterPlanMode` tool to enter planning mode
3. Present the fix plan for user approval

---

## Severity Classification Guide

**CRITICAL** - Must fix before release:
- App crashes
- Data loss
- Security issues
- Core feature completely broken
- Login/auth broken
- Forms fail to submit
- Payment flow broken (if applicable)

**MAJOR** - Should fix before release:
- Feature partially broken
- Confusing user flow
- Significant UI bugs
- Mobile layout broken
- Multiple console errors on key pages
- Slow/broken loading states

**MINOR** - Nice to fix:
- Small visual inconsistencies
- Polish items
- Slight alignment issues
- Non-critical hover states
- Minor responsive tweaks

---

## Important Rules

1. **Test EVERYTHING** - UI/UX AND functionality
2. **Both viewports mandatory** - Desktop (1280px) AND Mobile (375px)
3. **Console monitoring** - Check after EVERY action
4. **Network monitoring** - Watch for failed requests
5. **Screenshots liberally** - Visual evidence for every issue
6. **Complete flows** - Test entire user journeys, not just individual elements
7. **Verify data** - Don't just check UI, verify forms actually submit
8. **Be thorough** - Miss nothing, this is the "big" test
9. **Accurate scoring** - Be honest, don't inflate scores
