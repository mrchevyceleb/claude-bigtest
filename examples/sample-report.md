# Sample /bigtest Report

This is an example of a complete `/bigtest` execution report.

## Command Used

```bash
/bigtest https://myapp.vercel.app
```

## Pre-Test Assessment Output

```
## User Action Assessment for MyApp

### Navigation Actions
- [x] Click logo to go home
- [x] Click "Dashboard" nav item
- [x] Click "Settings" nav item
- [x] Click "Profile" nav item
- [x] Click footer "About" link
- [x] Click footer "Contact" link

### Page-Specific Actions
- [x] Dashboard: Click "New Project" button
- [x] Dashboard: Click project card to expand
- [x] Settings: Toggle notification switch
- [x] Settings: Click "Save Changes" button
- [x] Profile: Click "Edit Avatar" button
- [x] Profile: Submit profile form

### Form Actions
- [x] Fill login email field
- [x] Fill login password field
- [x] Submit login form
- [x] Fill settings form fields
- [x] Submit settings form

### Interactive Element Actions
- [x] Open user dropdown menu
- [x] Open notification modal
- [x] Close notification modal (X button)
- [x] Close notification modal (escape key)
- [x] Expand FAQ accordion items
- [x] Toggle dark mode switch

I've identified 24 user actions to test across 4 pages. Proceeding with UI/UX testing...
```

## Full Report

```markdown
# UI/UX QA Test Report: MyApp
**Tested on:** January 4, 2026
**Viewports:** Desktop (1280px), Mobile (375px)
**Test Type:** UI/UX Testing (NOT Functionality)

## Pre-Test Assessment Summary
- Total user actions identified: 24
- Total pages discovered: 4
- Total interactive elements: 37

## Executive Summary
- Total pages tested: 4
- Total elements tested: 37
- Total user actions tested: 24
- Critical issues: 2
- Major issues: 3
- Minor issues: 5
- Console errors found: 7

## Critical Issues (Must Fix - Blocking)

### Issue 1: Mobile navigation menu doesn't open
- **Location:** Header component, all pages
- **Steps to Reproduce:**
  1. Set viewport to 375px
  2. Click hamburger menu icon
- **Expected:** Navigation drawer opens with slide animation
- **Actual:** Nothing happens, button appears unresponsive
- **Console Errors:** "Cannot read property 'toggle' of undefined" at Header.tsx:45
- **Screenshot:** screenshots/mobile-nav-broken.png
- **Viewport:** Mobile

### Issue 2: Dashboard cards not rendering on initial load
- **Location:** /dashboard
- **Steps to Reproduce:**
  1. Login to application
  2. Navigate to /dashboard
  3. Observe content area
- **Expected:** Project cards should display immediately
- **Actual:** Empty state shown for 3+ seconds, then cards appear
- **Console Errors:** "Warning: Cannot update a component while rendering"
- **Screenshot:** screenshots/dashboard-loading.png
- **Viewport:** Both

## Major Issues (Should Fix - Significant Impact)

### Issue 1: Settings form validation errors not styled
- **Location:** /settings
- **Steps to Reproduce:**
  1. Navigate to /settings
  2. Clear email field
  3. Click outside field (trigger blur)
- **Expected:** Error message in red with icon
- **Actual:** Plain black text, no visual distinction
- **Console Errors:** None
- **Screenshot:** screenshots/settings-validation.png
- **Viewport:** Both

### Issue 2: Profile avatar upload button hidden on mobile
- **Location:** /profile
- **Steps to Reproduce:**
  1. Set viewport to 375px
  2. Navigate to /profile
  3. Look for avatar edit button
- **Expected:** Edit button visible below avatar
- **Actual:** Button pushed off-screen, requires horizontal scroll
- **Console Errors:** None
- **Screenshot:** screenshots/profile-mobile-avatar.png
- **Viewport:** Mobile

### Issue 3: Dropdown menu clips behind header on scroll
- **Location:** Header component
- **Steps to Reproduce:**
  1. Scroll down on any page
  2. Click user dropdown in header
  3. Observe dropdown position
- **Expected:** Dropdown appears below header, fully visible
- **Actual:** Dropdown clips behind sticky header
- **Console Errors:** None
- **Screenshot:** screenshots/dropdown-clipping.png
- **Viewport:** Desktop

## Minor Issues (Nice to Fix - Polish)

### Issue 1: Hover state missing on footer links
- **Location:** Footer component
- **Description:** Footer links have no visual feedback on hover
- **Viewport:** Desktop

### Issue 2: Focus ring not visible on dark mode toggle
- **Location:** Settings page
- **Description:** When tabbing to toggle, focus indicator is invisible
- **Viewport:** Both

### Issue 3: Inconsistent button padding
- **Location:** Multiple pages
- **Description:** Primary buttons have 12px padding, secondary have 8px
- **Viewport:** Both

### Issue 4: Accordion animation choppy
- **Location:** FAQ section
- **Description:** Expand/collapse animation stutters, not smooth
- **Viewport:** Both

### Issue 5: Modal close button too small on mobile
- **Location:** All modals
- **Description:** X button is 24px, should be 44px for touch
- **Viewport:** Mobile

## Console Errors Log
| Page | Action | Error Message | Severity |
|------|--------|---------------|----------|
| /dashboard | Page load | Warning: Cannot update component while rendering | warning |
| /dashboard | Click project card | Uncaught TypeError: project.tags is undefined | error |
| /settings | Toggle notifications | Warning: Each child should have unique key | warning |
| /profile | Page load | Failed to load resource: 404 /api/avatar | error |
| Header | Click mobile menu | Cannot read property 'toggle' of undefined | error |
| Header | Open dropdown | z-index warning in console | warning |
| Footer | Page load | Mixed content warning: HTTP image on HTTPS | warning |

## Accessibility Issues
- Focus ring not visible on dark mode toggle (Settings)
- Modal close button below 44px touch target (All modals)
- Footer links missing hover/focus states
- Some images missing alt text (Dashboard cards)

## Performance Observations
- Dashboard initial render takes 3+ seconds
- Accordion animations are not GPU-accelerated
- Large avatar images not optimized (2MB+)

## User Action Test Coverage
| Action Category | Total | Tested | Passed | Failed |
|-----------------|-------|--------|--------|--------|
| Navigation | 6 | 6 | 5 | 1 |
| Buttons | 8 | 8 | 6 | 2 |
| Forms | 5 | 5 | 4 | 1 |
| Links | 6 | 6 | 5 | 1 |
| Modals | 3 | 3 | 3 | 0 |
| Dropdowns | 2 | 2 | 1 | 1 |
| Toggles | 2 | 2 | 2 | 0 |
| **TOTAL** | **32** | **32** | **26** | **6** |
```

## Auto-Generated Fix Plan

After the report, `/bigtest` enters plan mode with a prioritized fix plan:

```markdown
# Fix Plan for MyApp UI/UX Issues

## Priority 1: Critical (Fix Immediately)

### Fix 1: Mobile Navigation
- **File:** src/components/Header/MobileNav.tsx
- **Issue:** Toggle function undefined
- **Fix:** Initialize state and bind toggle handler
- **Complexity:** Simple

### Fix 2: Dashboard Rendering
- **File:** src/pages/Dashboard.tsx
- **Issue:** Component update during render
- **Fix:** Move state update to useEffect
- **Complexity:** Medium

## Priority 2: Major (Fix Soon)

### Fix 3: Settings Validation Styling
- **File:** src/components/Forms/ValidationError.tsx
- **Issue:** Missing error styles
- **Fix:** Add red color, error icon, proper spacing
- **Complexity:** Simple

### Fix 4: Profile Mobile Layout
- **File:** src/pages/Profile.module.css
- **Issue:** Avatar button overflow
- **Fix:** Add responsive breakpoint, stack layout on mobile
- **Complexity:** Simple

### Fix 5: Dropdown Z-Index
- **File:** src/components/Header/Dropdown.tsx
- **Issue:** Z-index lower than header
- **Fix:** Increase z-index to 1001 (header is 1000)
- **Complexity:** Simple

## Priority 3: Minor (Fix When Possible)

### Fixes 6-10: Polish items
- Footer hover states
- Focus ring visibility
- Button padding consistency
- Accordion animation
- Modal touch targets
```

## What Happens Next

After reviewing the fix plan:
1. **Approve** to start fixing issues
2. Use `/perfect` for each fix to ensure quality
3. Re-run `/bigtest` to verify all issues resolved
