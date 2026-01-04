# 🧪 /bigtest - Comprehensive UI/UX Testing for Claude Code

A powerful slash command for [Claude Code](https://claude.ai/claude-code) that performs **complete UI/UX testing** of any web application using Playwright. It systematically tests every user action, monitors console logs throughout, and generates detailed reports with an auto-created fix plan.

**Test your entire frontend like a QA engineer - without being one.**

![UI/UX Testing](https://img.shields.io/badge/Testing-UI%2FUX-blue)
![Claude Code](https://img.shields.io/badge/Claude_Code-Slash_Command-blue)
![Playwright](https://img.shields.io/badge/Powered_by-Playwright-45ba63)

---

## ✨ Features

- **📋 Pre-Test Assessment** - Documents ALL user actions before testing begins
- **🖥️ Dual Viewport Testing** - Desktop (1280px) and Mobile (375px)
- **📊 Console Log Monitoring** - Catches hidden errors after EVERY action
- **♿ Accessibility Checks** - Basic a11y audit included
- **📝 Detailed Reports** - Know exactly what passed, failed, and why
- **🔧 Auto Fix Plans** - Prioritized issues ready for approval

---

## ⚠️ Important: UI/UX Testing Only

This command tests **user interface and user experience** - NOT business logic or functionality.

| ✅ What /bigtest Tests | ❌ What /bigtest Does NOT Test |
|------------------------|--------------------------------|
| Visual appearance | Business logic |
| Layout & spacing | Data validation rules |
| Responsive design | API correctness |
| Hover/focus states | Database operations |
| Console errors | Backend processing |
| Interaction feedback | Authentication logic |
| Button click responses | Form submission handlers |
| Modal open/close | Payment processing |

---

## 📦 Installation

### 1. Copy the command file

```bash
# Create the commands directory if it doesn't exist
mkdir -p ~/.claude/commands

# Copy the command file
cp bigtest.md ~/.claude/commands/bigtest.md
```

### 2. Enable Playwright MCP

Add to your `~/.claude/mcp_settings.json`:

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["@anthropic-ai/claude-code-mcp-adapter", "npx", "@anthropic-ai/mcp-server-playwright@latest"]
    }
  }
}
```

### 3. Verify installation

```bash
# In Claude Code, run:
/mcp
# Ensure playwright is enabled
```

---

## 🚀 Usage

### Basic Usage

```bash
/bigtest
```

You'll be prompted for:
1. The URL to test
2. Whether authentication is needed
3. Login credentials (if applicable)

### With URL Argument

```bash
/bigtest https://myapp.vercel.app
```

---

## 🔄 How It Works

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  PHASE 0: PRE-TEST ASSESSMENT (Required First!)                             │
│  ───────────────────────────────────────────────────────────────────────── │
│  Documents EVERY user action possible in the app:                           │
│  • Navigation actions (logo, menu items, footer links)                      │
│  • Page-specific actions (buttons, forms, interactions per page)            │
│  • Form actions (fill, submit, reset)                                       │
│  • Interactive elements (modals, accordions, toggles, dropdowns)            │
│  • Authentication actions (login, logout, password reset)                   │
│                                                                             │
│  Output: "I've identified [X] user actions across [Y] pages. Proceeding..." │
└─────────────────────────────────────────────────────────────────────────────┘
                                    ↓
┌─────────────────────────────────────────────────────────────────────────────┐
│  PHASE 1: SETUP & DISCOVERY                                                 │
│  ───────────────────────────────────────────────────────────────────────── │
│  • Get target URL                                                           │
│  • Check if authentication needed                                           │
│  • Navigate to app with Playwright                                          │
│  • Take baseline screenshot                                                 │
│  • CHECK CONSOLE LOGS immediately                                           │
│  • Map application structure (pages, routes, elements)                      │
└─────────────────────────────────────────────────────────────────────────────┘
                                    ↓
┌─────────────────────────────────────────────────────────────────────────────┐
│  PHASE 2: AUTHENTICATION (if required)                                      │
│  ───────────────────────────────────────────────────────────────────────── │
│  • Navigate to login page                                                   │
│  • CHECK CONSOLE LOGS before interacting                                    │
│  • Enter credentials                                                        │
│  • Submit login form                                                        │
│  • CHECK CONSOLE LOGS after submission                                      │
│  • Verify authentication succeeded                                          │
└─────────────────────────────────────────────────────────────────────────────┘
                                    ↓
┌─────────────────────────────────────────────────────────────────────────────┐
│  PHASE 3: DESKTOP TESTING (1280px viewport)                                 │
│  ───────────────────────────────────────────────────────────────────────── │
│  For EVERY element, CHECK CONSOLE LOGS after EVERY action:                  │
│                                                                             │
│  • Navigation: Visit pages, verify loads, screenshot, check console         │
│  • Buttons: Click all, verify visual feedback, check console                │
│  • Forms: Test styling, tab order, placeholders, validation UI              │
│  • Links: Click all, verify navigation, check console                       │
│  • Modals: Open/close, verify styling, escape key, check console            │
│  • Dropdowns: Open, select options, verify visual update                    │
│  • Inputs: Test focus/blur states, cursor behavior                          │
└─────────────────────────────────────────────────────────────────────────────┘
                                    ↓
┌─────────────────────────────────────────────────────────────────────────────┐
│  PHASE 4: MOBILE TESTING (375px viewport)                                   │
│  ───────────────────────────────────────────────────────────────────────── │
│  Repeat ALL Phase 3 tests, PLUS:                                            │
│  • Verify responsive layouts                                                │
│  • Test hamburger/mobile navigation menus                                   │
│  • Check touch-target sizes (min 44px)                                      │
│  • Verify no horizontal scrolling                                           │
│  • CHECK CONSOLE LOGS after each action                                     │
└─────────────────────────────────────────────────────────────────────────────┘
                                    ↓
┌─────────────────────────────────────────────────────────────────────────────┐
│  PHASE 5: QUALITY CHECKS                                                    │
│  ───────────────────────────────────────────────────────────────────────── │
│  • Console Error Audit: Comprehensive log review                            │
│  • Accessibility: Alt text, focus states, contrast, keyboard nav            │
│  • Performance: Slow pages, laggy interactions                              │
└─────────────────────────────────────────────────────────────────────────────┘
                                    ↓
┌─────────────────────────────────────────────────────────────────────────────┐
│  PHASE 6: GENERATE DETAILED REPORT                                          │
│  ───────────────────────────────────────────────────────────────────────── │
│  Structured report with:                                                    │
│  • Pre-Test Assessment Summary                                              │
│  • Executive Summary (tests, pass/fail, console errors)                     │
│  • Critical Issues (blocking bugs)                                          │
│  • Major Issues (significant problems)                                      │
│  • Minor Issues (polish items)                                              │
│  • Console Errors Log (with triggering action)                              │
│  • Accessibility Issues                                                     │
│  • User Action Test Coverage table                                          │
└─────────────────────────────────────────────────────────────────────────────┘
                                    ↓
┌─────────────────────────────────────────────────────────────────────────────┐
│  PHASE 7: AUTO-CREATE FIX PLAN                                              │
│  ───────────────────────────────────────────────────────────────────────── │
│  • Organize issues by priority (Critical → Major → Minor)                   │
│  • Group by component/page location                                         │
│  • Enter plan mode for user approval                                        │
│  • Include specific files to modify                                         │
│  • Estimate complexity (simple/medium/complex)                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 📋 Pre-Test Assessment

Before testing anything, `/bigtest` creates a comprehensive checklist:

```markdown
## User Action Assessment for MyApp

### Navigation Actions
- [ ] Click logo to go home
- [ ] Click "Dashboard" nav item
- [ ] Click "Settings" nav item
- [ ] Click "Profile" nav item
- [ ] Click footer "About" link
- [ ] Click footer "Contact" link

### Page-Specific Actions
- [ ] Dashboard: Click "New Project" button
- [ ] Dashboard: Click project card to expand
- [ ] Settings: Toggle notification switch
- [ ] Settings: Click "Save Changes" button
- [ ] Profile: Click "Edit Avatar" button
- [ ] Profile: Submit profile form

### Form Actions
- [ ] Fill login email field
- [ ] Fill login password field
- [ ] Submit login form
- [ ] Fill settings form fields
- [ ] Submit settings form

### Interactive Element Actions
- [ ] Open user dropdown menu
- [ ] Open notification modal
- [ ] Close notification modal (X button)
- [ ] Close notification modal (escape key)
- [ ] Expand FAQ accordion items
- [ ] Toggle dark mode switch

### Authentication Actions
- [ ] Login flow
- [ ] Logout flow
```

**Output:** "I've identified 24 user actions to test across 4 pages. Proceeding with UI/UX testing..."

---

## 📊 Console Log Monitoring

The key differentiator of `/bigtest` is **continuous console monitoring**.

After EVERY action, the command:
1. Checks `browser_console_messages`
2. Documents any errors/warnings
3. Notes which action triggered the error
4. Includes in the final report

### Why This Matters

Many JavaScript errors are "silent" - they don't crash the app but indicate:
- Memory leaks
- Failed event handlers
- Missing dependencies
- Race conditions
- Unhandled promises

`/bigtest` catches them ALL.

---

## 📝 Report Format

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
- Major issues: 5
- Minor issues: 8
- Console errors found: 12

## Critical Issues (Must Fix - Blocking)

### Issue 1: Mobile navigation menu doesn't open
- **Location:** Header component, all pages
- **Steps to Reproduce:**
  1. Set viewport to 375px
  2. Click hamburger menu icon
- **Expected:** Navigation drawer opens
- **Actual:** Nothing happens, button unresponsive
- **Console Errors:** "Cannot read property 'toggle' of undefined"
- **Screenshot:** mobile-nav-broken.png
- **Viewport:** Mobile

### Issue 2: Login button disabled state not visible
- **Location:** /login page
- **Steps to Reproduce:**
  1. Navigate to /login
  2. Leave form empty
  3. Observe submit button
- **Expected:** Button should appear disabled/grayed out
- **Actual:** Button looks active but doesn't respond
- **Console Errors:** None
- **Screenshot:** login-button-disabled.png
- **Viewport:** Both

## Console Errors Log
| Page | Action | Error Message | Severity |
|------|--------|---------------|----------|
| /dashboard | Click "New Project" | Uncaught TypeError: projects.map is not a function | error |
| /settings | Toggle notifications | Warning: Each child should have unique key prop | warning |
| /profile | Load page | Failed to load resource: 404 avatar.png | error |

## User Action Test Coverage
| Action Category | Total | Tested | Passed | Failed |
|-----------------|-------|--------|--------|--------|
| Navigation | 6 | 6 | 5 | 1 |
| Buttons | 8 | 8 | 6 | 2 |
| Forms | 5 | 5 | 4 | 1 |
| Links | 4 | 4 | 4 | 0 |
| Modals | 3 | 3 | 3 | 0 |
| Inputs | 5 | 5 | 3 | 2 |
```

---

## 🖥️ Viewports Tested

| Device | Width | Tests |
|--------|-------|-------|
| Desktop | 1280px | Full test suite |
| Mobile | 375px | Full test suite + responsive checks |

### Mobile-Specific Checks

- Responsive layouts render correctly
- Hamburger/mobile navigation works
- Touch targets are at least 44px
- No horizontal scrolling
- Text is readable without zooming

---

## 🎭 Playwright Tools Used

| Tool | Purpose |
|------|---------|
| `browser_navigate` | Navigate to pages |
| `browser_click` | Click elements |
| `browser_press_key` | Keyboard input |
| `browser_take_screenshot` | Visual evidence |
| `browser_snapshot` | DOM structure |
| `browser_console_messages` | Monitor JS errors |
| `browser_evaluate` | Execute JavaScript |
| `browser_wait_for` | Wait for page loads |

---

## 🔧 Troubleshooting

| Issue | Solution |
|-------|----------|
| "Playwright MCP not available" | Run `/mcp` and enable playwright |
| App requires auth but wasn't asked | Re-run and answer "yes" to auth question |
| Missing pages in test | Check that navigation is crawlable |
| Console errors overwhelming | Focus on "error" level first |
| Mobile tests failing | Ensure responsive CSS is loading |

---

## 🎯 Tips for Best Results

### 1. Start with a Clean State

Run tests on a fresh instance:
- Clear localStorage/cookies
- Use a test account
- Reset any user preferences

### 2. Provide Test Credentials

If your app requires login:
- Have test credentials ready
- Ensure test account has access to all features
- Use an account with representative data

### 3. Review the Pre-Assessment

Before testing begins, review the action checklist:
- Are all important actions captured?
- Any missing pages?
- Any edge cases to add?

### 4. Focus on Critical Issues First

The report prioritizes issues:
1. **Critical** - Fix immediately (blocking)
2. **Major** - Fix soon (significant impact)
3. **Minor** - Fix when possible (polish)

---

## 📁 File Structure

```
~/.claude/
└── commands/
    └── bigtest.md    # The command file
```

---

## 🆚 /bigtest vs /perfect

| Feature | /bigtest | /perfect |
|---------|----------|----------|
| **Purpose** | Comprehensive UI/UX audit | Implement + verify specific task |
| **Scope** | Entire application | Single feature/fix |
| **Pre-assessment** | Yes - lists all actions | No |
| **Looping** | No - single pass | Yes - until score=100 |
| **Auto-commit** | No | Yes (on perfect score) |
| **Best for** | QA before release | Development workflow |

**Use together:** Run `/bigtest` to find all issues, then `/perfect` to fix each one!

---

## 🤝 Contributing

Found a bug? Have an improvement idea?

1. Fork this repo
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📄 License

MIT License - feel free to use, modify, and distribute.

---

## 🙏 Acknowledgments

- Built for [Claude Code](https://claude.ai/claude-code) by Anthropic
- Powered by [Playwright](https://playwright.dev/) for browser automation
- Inspired by the need for comprehensive QA in AI-assisted development

---

**Made with 🤖 by [Matt Johnston](https://mattjohnston.io)**

*Star ⭐ this repo if you find it useful!*
