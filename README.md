# /bigtest - Comprehensive Application Testing for Claude Code

A powerful slash command for [Claude Code](https://claude.ai/claude-code) that performs **complete testing** of any web application using Playwright. It tests UI/UX, functionality, console errors, network errors, and user flows - then generates a scored report with prioritized fixes.

**Full QA audit of your entire application - not just UI.**

![Version](https://img.shields.io/badge/Version-2.0-blue)
![Testing](https://img.shields.io/badge/Testing-Everything-brightgreen)
![Claude Code](https://img.shields.io/badge/Claude_Code-Slash_Command-blue)
![Playwright](https://img.shields.io/badge/Powered_by-Playwright-45ba63)

---

## What's New in v2.0

**BREAKING CHANGE:** Now tests EVERYTHING, not just UI/UX!

- **Functionality Testing** - Forms submit, buttons work, features function
- **Scoring System** - 0-100 with explicit rubric
- **Network Error Tracking** - Failed API calls, 404s, 500s
- **User Flow Testing** - Complete journeys work end-to-end
- **Severity Classification** - Critical / Major / Minor

---

## What It Tests

| Category | Points | What's Tested |
|----------|--------|---------------|
| **UI/Visual** | 20 | Layout, images, responsive, overflow |
| **Functionality** | 30 | Forms submit, buttons work, features function |
| **Console Errors** | 20 | JavaScript errors (-4 per error) |
| **Network Errors** | 15 | API calls, 404s, failed requests (-5 per error) |
| **User Flows** | 15 | Complete user journeys work |
| **TOTAL** | **100** | |

---

## Installation

### 1. Copy the command file

```bash
mkdir -p ~/.claude/commands
cp bigtest.md ~/.claude/commands/bigtest.md
```

### 2. Enable Playwright MCP

Add to your `~/.claude/mcp_settings.json`:

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["@playwright/mcp@latest"]
    }
  }
}
```

### 3. Verify installation

```bash
/mcp
# Ensure playwright is enabled
```

---

## Usage

```bash
# Basic - will prompt for URL
/bigtest

# With URL
/bigtest https://myapp.vercel.app
```

---

## How It Works

```
+----------------------------------------------------------+
| PHASE 0: PRE-TEST ASSESSMENT                              |
| Map entire app - pages, forms, buttons, user flows        |
| Output: "Found X pages, Y forms, Z actions to test"       |
+----------------------------------------------------------+
                           |
+----------------------------------------------------------+
| PHASE 1: SETUP                                            |
| Get URL, check auth requirements, initial navigation      |
+----------------------------------------------------------+
                           |
+----------------------------------------------------------+
| PHASE 2: AUTHENTICATION (if required)                     |
| Test login flow, verify session                           |
+----------------------------------------------------------+
                           |
+----------------------------------------------------------+
| PHASE 3: DESKTOP TESTING (1280x720)                       |
| - Navigation: All links, routes                           |
| - Forms: UI + SUBMISSION (functionality!)                 |
| - Buttons: Click + verify action occurs                   |
| - Modals: Open, close, escape key                         |
| - Console monitoring after every action                   |
| - Network monitoring for failed requests                  |
+----------------------------------------------------------+
                           |
+----------------------------------------------------------+
| PHASE 4: MOBILE TESTING (375x667)                         |
| Repeat all Phase 3 tests + responsive checks              |
+----------------------------------------------------------+
                           |
+----------------------------------------------------------+
| PHASE 5: AUDIT                                            |
| Compile console errors, network errors                    |
+----------------------------------------------------------+
                           |
+----------------------------------------------------------+
| PHASE 6: CALCULATE SCORE (0-100)                          |
| UI: 20 | Functionality: 30 | Console: 20                  |
| Network: 15 | Flows: 15                                   |
+----------------------------------------------------------+
                           |
+----------------------------------------------------------+
| PHASE 7: GENERATE REPORT                                  |
| Score breakdown, issues by severity, logs                 |
+----------------------------------------------------------+
                           |
+----------------------------------------------------------+
| PHASE 8: CREATE FIX PLAN                                  |
| Enter plan mode with prioritized fixes                    |
+----------------------------------------------------------+
```

---

## Scoring Rubric

### UI/Visual (20 points)

| Issue | Deduction |
|-------|-----------|
| Major layout break | -4 |
| Missing/broken image | -3 |
| Text overflow | -2 |
| Alignment issue | -1 |
| Mobile layout break | -3 |
| Horizontal scroll | -3 |

### Functionality (30 points)

| Issue | Deduction |
|-------|-----------|
| Form submission fails | -6 |
| Button does nothing | -4 |
| Feature completely broken | -6 |
| Feature partially broken | -3 |
| Data not saving | -5 |
| Redirect not working | -2 |

### Console Errors (20 points)

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

### Network Errors (15 points)

```
networkScore = max(0, 15 - (errorCount * 5))
```

| Errors | Points |
|--------|--------|
| 0 | 15 |
| 1 | 10 |
| 2 | 5 |
| 3+ | 0 |

### User Flows (15 points)

| Issue | Deduction |
|-------|-----------|
| Critical flow broken | -5 |
| Critical flow partial | -3 |
| Secondary flow broken | -2 |

---

## Score Interpretation

| Score | Status | Meaning |
|-------|--------|---------|
| **95-100** | EXCELLENT | Production ready |
| **85-94** | GOOD | Solid, few issues |
| **70-84** | FAIR | Usable, needs work |
| **50-69** | POOR | Significant issues |
| **<50** | CRITICAL | Major problems |

---

## Severity Classification

**CRITICAL** - Must fix before release:
- App crashes
- Data loss
- Core feature broken
- Login/auth broken
- Forms fail to submit

**MAJOR** - Should fix before release:
- Feature partially broken
- Confusing user flow
- Significant UI bugs
- Mobile layout broken

**MINOR** - Nice to fix:
- Small visual inconsistencies
- Polish items
- Slight alignment issues

---

## Report Format

```
===============================================================================
                         /BIGTEST COMPREHENSIVE REPORT
===============================================================================

APPLICATION: https://myapp.vercel.app
TEST DATE: January 5, 2026
FINAL SCORE: 78/100 - FAIR

-------------------------------------------------------------------------------
                              TEST COVERAGE
-------------------------------------------------------------------------------

Pages Tested: 5
Forms Tested: 3
Buttons Tested: 12
User Flows Tested: 4
Total Test Actions: 47

-------------------------------------------------------------------------------
                              SCORE BREAKDOWN
-------------------------------------------------------------------------------

UI/Visual:       18/20   2 mobile layout issues
Functionality:   24/30   1 form fails, 1 button broken
Console Errors:  16/20   1 error found
Network Errors:  10/15   1 failed request
User Flows:      10/15   1 flow partial

-------------------------------------------------------------------------------
                              CRITICAL ISSUES
-------------------------------------------------------------------------------

1. [CRITICAL] Contact form submission fails
   - Location: /contact
   - Steps: Fill form, click Submit
   - Expected: Success message
   - Actual: Nothing happens
   - Console: "TypeError: undefined"

-------------------------------------------------------------------------------
                              MAJOR ISSUES
-------------------------------------------------------------------------------

1. [MAJOR] Mobile nav menu doesn't open
   - Location: Header, all pages
   - Viewport: Mobile only

-------------------------------------------------------------------------------
                              RECOMMENDATIONS
-------------------------------------------------------------------------------

Priority fixes:
1. Fix contact form submission handler
2. Fix mobile navigation toggle
3. Resolve console error on dashboard

===============================================================================
```

---

## /bigtest vs /perfect

| Aspect | /bigtest | /perfect |
|--------|----------|----------|
| **Scope** | Entire application | Single task/feature |
| **Purpose** | Full audit | Implement + fix loop |
| **Loops** | No, one pass | Yes, until 100 |
| **Auto-commit** | No | Yes at 100 |
| **Scoring** | 0-100 | 0-100 |
| **Tests Functionality** | YES (v2.0) | YES |

**Workflow:** `/bigtest` to find all issues -> `/perfect` to fix each one!

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| "Playwright MCP not available" | Run `/mcp` and enable |
| App requires auth | Provide credentials when asked |
| Missing pages | Check navigation is crawlable |
| Too many errors | Focus on Critical first |

---

## License

MIT License - feel free to use, modify, and distribute.

---

**Made with Claude Code by [Matt Johnston](https://mattjohnston.io)**

*Star this repo if you find it useful!*
